[Rocket](../Readme.md)/[chip](../chip.md)/[Periphery](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/chip/Periphery.scala)
=====================

**********************

### trait HasPeripheryParameters
*Parameters for peripherials.*

+ **peripheryBusConfig** `() => TLBusConfig`
+ **peripheryBusBytes** `() => Int` byte width of peripheral bus.
+ **socBusConfig** `() => TLBusConfig`
+ **socBusBytes** `() => Int` byte width of SoC bus.
+ **cacheBlockBytes** `() => Int` byte size of a cache block.
+ **peripheryBusArithmetic** `() => Boolean`
+ **nMemoryChannels** `() => Int` number of memory channels.
+ **nExtInterrupts** `() => Int` number of external interrupt lines.

### trait HasSystemNetworks
*HasSystemNetworks provides buses that will serve as attachment points,*
*for use in child traits that connect individual agents or external ports.*

~~~scala
trait HasSystemNetworks extends HasPeripheryParameters
~~~

+ **socBus** `LazyModule(new TLXbar)` Wide or unordered-access slave devices (TL-UH).
+ **peripheryBus** `LazyModule(new TLXbar)` Narrow and ordered-access slave devices (TL-UL).
+ **intBus** `LazyModule(new IntXbar)` Device and global external interrupts.
+ **fsb** `LazyModule(new TLBuffer(BufferParams.none))` Master devices talking to the frontside of the L2.
+ **bsb** `LazyModule(new TLBuffer(BufferParams.none))` Slave devices talking to the backside of the L2.
+ **mem** `Seq[LazyModule(new TLXbar)]` Ports out to DRAM.

## HasPeripheryExtInterrupts

### abstract trait HasPeripheryExtInterrupts
*This trait adds externally driven interrupts to the system.*
*However, it should not be used directly; instead one of the below*
*synchronization wiring child traits should be used.*

~~~scala
abstract trait HasPeripheryExtInterrupts extends HasSystemNetworks
~~~

+ **extInterrupts** `IntInternalInputNode` External interrupt input ports.

### trait HasPeripheryAsyncExtInterrupts
*This trait should be used if the External Interrupts have NOT*
*already been synchronized to the Periphery (PLIC) Clock.*

~~~scala
trait HasPeripheryAsyncExtInterrupts extends HasPeripheryExtInterrupts
~~~

Adding a `LazyModule(new IntXing)` in between of `intBus.intnode` and `extInterrupts`.

### trait HasPeripherySyncExtInterrupts
*This trait can be used if the External Interrupts have already been synchronized*
*to the Periphery (PLIC) Clock.*

~~~scala
trait HasPeripherySyncExtInterrupts extends HasPeripheryExtInterrupts
~~~

Directly connect `intBus.intnode` and `extInterrupts`.

### trait HasPeripheryExtInterruptsBundle
*Common io name and methods for propagating or tying off the port bundle.*

~~~scala
trait HasPeripheryExtInterruptsBundle extends HasPeripheryParameters
~~~

+ **interrupts** `UInt` The value of external interrupt
+ **tieOffInterrupts** `() => Unit` tie all interupts to zeros.

### trait HasPeripheryExtInterruptsModuleImp
*This trait performs the translation from a UInt IO into Diplomatic Interrupts.*
*The wiring must be done in the concrete LazyModuleImp.*

~~~scala
trait HasPeripheryExtInterruptsModuleImp extends LazyMultiIOModuleImp
    with HasPeripheryExtInterruptsBundle
~~~

+ **outer** `HasPeripheryExtInterrupts` pointer to parent LazyModule.
+ **interrupts** `IO(UInt(INPUT, width = outer.nExtInterrupts))` The actual external interrupt ports.

## HasPeripheryMasterAXI4MemPort

### trait HasPeripheryMasterAXI4MemPort
*Adds a port to the system intended to master an AXI4 DRAM controller.*

~~~scala
trait HasPeripheryMasterAXI4MemPort extends HasSystemNetworks {
    val module: HasPeripheryMasterAXI4MemPortModuleImp
}
~~~

+ **module** `HasPeripheryMasterAXI4MemPortModuleImp` pointer to the module implementation.
+ **mem_axi4** `AXI4BlindOutputNode` The AXI memory ports.

For every TileLink port to a memory channel:<br>
AXI4BlindOutputNode <- AXI4Buffer <- AXI4UserYanker <- AXI4IdIndexer <- TLToAXI4 <- TLXbar

### trait HasPeripheryMasterAXI4MemPortBundle
*Common io name and methods for propagating or tying off the port bundle.*

~~~scala
trait HasPeripheryMasterAXI4MemPortBundle extends HasPeripheryParameters {
  val mem_axi4: HeterogeneousBag[AXI4Bundle]
}
~~~

+ **connectSimAXIMem** `() => Unit` connect memory AXI ports in simulation.

### trait HasPeripheryMasterAXI4MemPortImp
*Actually generates the corresponding IO in the concrete Module.*

~~~scala
trait HasPeripheryMasterAXI4MemPortModuleImp extends LazyMultiIOModuleImp
    with HasPeripheryMasterAXI4MemPortBundle
{
  val outer: HasPeripheryMasterAXI4MemPort
}
~~~

+ **outer** `HasPeripheryMasterAXI4MemPort` pointer to the LazyModule.
+ **mem_axi4** `HeterogeneousBag[AXI4Bundle]` the actual I/O ports.




<br><br><br><p align="right">
<sub>
Last updated: 11/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>

