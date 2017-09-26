[Rocket](../../Readme.md)/[devices](../../devices.md)/[tilelink](../tilelink.md)/[Plic](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/devices/tilelink/Plic.scala)
========================
*platform-level interrupt controller*

**********************

### class LevelGateway
*Gateway components for level interrupts.*

+ I/O, type and Paramter

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| interrupt              | Bool             | I          | level interrupt line.                 |
| plic.valid             | Bool             | O          | interrupt pending to PLIC.            |
| plic.ready             | Bool             | I          | PLIC ready for new interrupts.        |
| plic.complete          | Bool             | I          | the inflight interrupt served by PLIC.|

The incoming `interrupt` is edged into a pulse to `plic.valid` whenever PLIC is `ready`.
When PLIC finishes serving an interrupt, it sets `plic.complete` to reset the current inflight interrupt, allowing for new interrupt.

*Question: it seems if the last interrupt is stuck, the incoming interrupt can be lost if its level signal is not edged early enough.*

### object PLICConsts
*Constants used by PLIC.*

+ **maxDevices** `() => 1023`    the maximal number of devices that can be supported.
+ **maxHarts** `() => 15872`     the maximal number of harts that can be supported.
+ **priorityBase** `() => 0x0`   the register base address for interrupt priorities.
+ **pendingBase** `() => 0x1000` the register base address for interrupt pending registers.
+ **enableBase** `() => 0x2000`
+ **hartBase** `() => 0x200000`
+ **claimOffset** `() => 4`
+ **priorityBytes** `() => 4`
+ **enableOffset** `(i:Int) => Int`
+ **hartOffset** `(i:Int) => i * 0x1000`
+ **enableBase** `(i:Int) => Int`
+ **hartBase** `(i:Int) => Int`
+ **size** `() => Int`

### case class PLICParams

~~~scala
case class PLICParams(baseAddress: BigInt = 0xC000000, maxPriorities: Int = 7)
~~~

+ **baseAddress** `BigInt` (param) the base address of the PLIC
+ **maxPriorities** `Int` (param) the maximal number of priority levels
+ **address** `() => AddressSet` get the address space of the PLIC

### class TLPLIC
*The platform level interrupt controller*

~~~scala
class TLPLIC(params: PLICParams)(implicit p: Parameters) extends LazyModule {
  val device = new SimpleDevice("interrupt-controller", Seq("riscv,plic0"))
  val node = TLRegisterNode
  val intnode = IntNexusNode
}
~~~

+ **params** `PLICParams` (param) the parameter for the PLIC.
+ **device** `SimpleDevice` the device descriptor.
  - `"interrupt-controller" -> Nil`  identify this is an interrupt controller
  - `"riscv,ndev" -> nDevices` identify the number of interrupts controlled by this PLIC
  - `"riscv,max-priority" -> maxPriorities` identify the maximal priority levels
  - `"#interrupt-cells" -> 1` set the number size to 32b
+ **node** `TLRegisterNode` the diplomacy node description.
+ **intnode** `IntNexusNode` the interrupt crossbar
+ **nDevice** `() => Int` get the number of devices (interrupt inputs) by counting the `intnode.edgesIn`
+ **nPriorities** `() => Int` the number of actual priority levels: `min(nDevices, maxPriorities)`
+ **nHarts** `() => Int` the number of connected harts by counting `intnode.edgesOut`
+ **module** `LazyModuleImp` the actual module implementation
  - io:<br>
    **tl_in** `HeterogeneousBag[TLBundle]` tilelink input ports.<br>
    **devices** `Vec[Bool]` interrupts from devices.<br>
    **harts** `Vec[Bool]` interrupts to harts
  - **interrupts** `Seq[Bool]` group interrupts
  - **harts** `Seq[Bool]` group harts as well
  - **gateways** `Seq[GatewayPLICIO]` implement the level gateways and get the PLICIOs
  - **priority** `Reg[Vec[UInt]]` the priority of all interrupts
  - **threshold** `Reg[Vec[UInt]]` the threshold of all interrupts
  - **pending** `Reg[Vec[Bool]]` whether any interrupts are pending
  - **enables** `Reg[Vec[Bool]]` whether a hart accepts interrupts
  - **maxDevs** `Reg[Vec[UInt]]` record the pending interrupt with the largest priority for each hart
  - **priorityRegFields** `Int -> Seq[RegField]` define the _interrupt source priorities_: `priorityBase -> priority.map(p => priorityRegField(p))`
  - **pendingRegFields** `Int -> Seq[RegField]` define the _interrupt pending_ bits: `pendingBase -> Vec[Bool]`
  - **enableRegFields** `Int -> Seq[RegField]` define the _target interrupt enable_ registers: `enableBase(i) -> RegField(1, Vec[Bool])`
  - **hartRegFields** `Int -> Seq[RegField]` define hart interrupt control registers: `hartBase(i) -> RegField`
    For the register field: When read, claim the interrupt source with the maximal priority.
    When write, write {_target completion_, _target priority threshold_}.

### trait HasPeripheryPLIC
*Trait that will connect a PLIC to a coreplex*

~~~scala
trait HasPeripheryPLIC extends HasInterruptBus with HasPeripheryBus {
  val plic  = LazyModule(new TLPLIC(p(PLICParams)))
  plic.node := pbus.toVariableWidthSlaves
  plic.intnode := ibus.toPLIC
}
~~~


<br><br><br><p align="right">
<sub>
Last updated: 26/09/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
