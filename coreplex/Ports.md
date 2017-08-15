[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[Ports](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/Ports.scala)
========================
*Provide various traits to add ports to the system, in some cases converting to different interconnect standards.*

************************

- [Parameters](#parameters)
- [AXI4 Memory Master](#axi4-memory-master)
- [AXI4 MMIO Master](#axi4-mmio-master)
- [AXI4 Slave](#axi4-slave)
- [TileLink MMIO Master](#tilelink-mmio-master)
- [TileLink Slave](#tilelink-slave)
- [Simulation](#simulation)

************************

## Parameters

### case class MasterPortParams
*Specifies the size and width of external memory ports.*

~~~scala
case class MasterPortParams(
  base: Long,
  size: Long,
  beatBytes: Int,
  idBits: Int,
  maxXferBytes: Int = 256,
  executable: Boolean = true)
~~~

+ **base** `Long` (param) the base address of this bus. (gradually replace BigInt with Long?)
+ **size** `Long` (param) the size of the address space on this bus.
+ **beatBytes** `Int` (param) number of bytes per single beat on this bus.
+ **idBits** `Int` (param) size of ID field.
+ **maxXferBytes** `Int` (param) the maximal number of bytes per a burst.
+ **executable** `Boolean` (param) whether any data fetched from this bus are executable (instructions).

## AXI4 Memory Master

### trait HasMasterAXI4MemPort
*Adds a port to the system intended to master an AXI4 DRAM controller.*

~~~scala
trait HasMasterAXI4MemPort extends HasMemoryBus {
  val module: HasMasterAXI4MemPortModuleImp
  private val params = p(ExtMem)
  private val device = new MemoryDevice
}
~~~

+ **module** `HasMasterAXI4MemPortModuleImp` (virtual) pointer to the module implementation.
+ **device** `MemoryDevice` (private) a memory device descriptor.
+ **mem_axi** `AXI4BlindOutputNode` the output port for the memory block.
+ **converter** `TLToAXI4` TileLink to AXI converter.
+ **trim** `AXI4IdIndexer` ??
+ **yank** `AXI4UserYanker` ??
+ **buffer** `AXI4Buffer` an AXI buffer.

Internal connection:
~~~
MemoryBus.toDRAMCrontroller ==> TLToAXI4 ==> AXI4IdIndexer ==> AXI4UserYanker ==> AXI4Buffer ==> AXI4BlindOutputNode ==> AXI memory
~~~

### trait HasMasterAXI4MemPortBundle
*Common io name and methods for propagating or tying off the port bundle.*

+ **mem_AXI4** `HeterogeneousBag[AXI4Bundle]` the AXI4 ports.
+ **nMemoryChannels** `Int` (virtual) number of memory channels.
+ **connectSimAXIMem** `() => Unit` connect the memory port `mem_axi4` with simulation model `SimAXIMem`.

### trait HasMasterAXI4MemPortModuleImp
*Actually generates the corresponding IO in the concrete Module*

~~~scala
trait HasMasterAXI4MemPortModuleImp extends LazyMultiIOModuleImp with HasMasterAXI4MemPortBundle {
  val outer: HasMasterAXI4MemPort
  val mem_axi4 = IO(outer.mem_axi4.bundleOut)
  val nMemoryChannels = outer.nMemoryChannels
}
~~~

+ **outer** `HasMasterAXI4MemPort` pointer to the LazyModule.
+ **mem_axi4** `HeterogeneousBag[AXI4Bundle]` the actual AXI4 ports.
+ **nMemoryChannels** `Int` number of memory channels.

## AXI MMIO Master

### trait HasMasterAXI4MMIOPort
*Adds a AXI4 port to the system intended to master an MMIO device bus.*

~~~scala
trait HasMasterAXI4MMIOPort extends HasSystemBus {
  private val params = p(ExtBus)
  private val device = new SimpleBus("mmio", Nil)
}
~~~

+ **device** `SimpleBus` (private) an AXI master port is a bus.
+ **mmio_axi** `AXI4BlindOutputNode` the output port for the AXI4 bus.

Internal connection:
~~~
SystemBus.toFixedWidthPorts ==> TLToAXI4 ==> AXI4IdIndexer ==> AXI4Deinterleaver ==> AXI4UserYanker ==> AXI4Buffer ==> AXI4BlindOutputNode ==> AXI bus
~~~

### trait HasMasterAXI4MMIOPortBundle
*Common io name and methods for propagating or tying off the port bundle.*

+ **mmio_axi4** `HeterogeneousBag[AXI4Bundle]` the AXI4 ports.
+ **connectSimAXIMMIO** `() => Unit` connect the MMIO port `mmio_axi4` with simulation module `SimAXIMem`.

### trait HasMasterAXI4MMIOPortModuleImp
*Actually generates the corresponding IO in the concrete Module*/

~~~scala
trait HasMasterAXI4MMIOPortModuleImp extends LazyMultiIOModuleImp with HasMasterAXI4MMIOPortBundle {
  val outer: HasMasterAXI4MMIOPort
  val mmio_axi4 = IO(outer.mmio_axi4.bundleOut)
}
~~~

+ **outer** `HasMasterAXI4MMIOPort` pointer to the LazyModule.
+ **mmio_axi4** `HeterogeneousBag[AXI4Bundle]` the actual AXI4 ports.

## AXI Slave

### trait HasSlaveAXI4Port
*Adds an AXI4 port to the system intended to be a slave on an MMIO device bus.*
**_Note: Read/write from this port comply with IO coherency (uncached)._**
~~~scala
trait HasSlaveAXI4Port extends HasSystemBus {
  private val params = p(ExtIn)
}
~~~

+ **l2FrontendAXI4Node** `AXI4BlindInputNode` the input port from the AXI4 bus.

Internal connection:
~~~
AXI4 bus ==> AXI4IdIndexer ==> AXI4Fragmenter ==> AXI4UserYanker ==> AXI4ToTL ==> TLWidthWidget ==> SystemBus.fromSyncPorts
~~~

### trait HasSlaveAXI4PortBundle
*Common io name and methods for propagating or tying off the port bundle.*

+ **l2_frontend_bus_axi4** `HeterogeneousBag[AXI4Bundle]` the AXI4 port.
+ **tieOffAXI4SlavePort** `() => Unit` tie the AXI4 input port for simulation.

### trait HasSlaveAXI4PortModuleImp
*Actually generates the corresponding IO in the concrete Module.*

~~~scala
trait HasSlaveAXI4PortModuleImp extends LazyMultiIOModuleImp with HasSlaveAXI4PortBundle {
  val outer: HasSlaveAXI4Port
  val l2_frontend_bus_axi4 = IO(outer.l2FrontendAXI4Node.bundleIn)
}
~~~

## TileLink MMIO Master

### trait HasMasterTLMMIOPort
*Adds a TileLink port to the system intended to master an MMIO device bus.*

~~~scala
trait HasMasterTLMMIOPort extends HasSystemBus {
  private val params = p(ExtBus)
  private val device = new SimpleBus("mmio", Nil)
}
~~~

+ **device** `SimpleBus` (private) an AXI master port is a bus.
+ **mmio_tl** `AXI4BlindOutputNode` the output port for the external TileLink bus.

Internal connection:
~~~
SystemBus.toFixedWidthPorts ==> TLSourceShrinker ==> TLBuffer ==> TileLink bus
~~~

### trait HasMasterTLMMIOPortBundle
*Common io name and methods for propagating or tying off the port bundle.*

+ **mmio_tl** `HeterogeneousBag[TLBundle]` the port to the external TileLink bus.
+ **tieOffTLMMIO** `() => Unit` tie the master port for simulation.

### trait HasMasterTLMMIOPortModuleImp
*Actually generates the corresponding IO in the concrete Module.*

~~~scala
trait HasMasterTLMMIOPortModuleImp extends LazyMultiIOModuleImp with HasMasterTLMMIOPortBundle {
  val outer: HasMasterTLMMIOPort
  val mmio_tl = IO(outer.mmio_tl.bundleOut)
}
~~~

## TileLink Slave

### trait HasSlaveTLPort
*Adds an TL port to the system intended to be a slave on an MMIO device bus.*
**_NOTE: this port is NOT allowed to issue Acquires. Read/write from this port comply with IO coherency (uncached)._**

~~~scala
trait HasSlaveTLPort extends HasSystemBus {
  private val params = p(ExtIn)
}
~~~

+ **l2FrontendTLNode** `TLBlindInputNode` the input port from the external TileLink bus.

Internal connection:
~~~
TileLink bus ==> TLWidthWidget ==> TLSourceShrinker ==> SystemBus.fromSyncPorts
~~~

### trait HasSlaveTLPortBundle
*Common io name and methods for propagating or tying off the port bundle.*

+ **l2FrontendTLNode** `TLBlindInputNode` the input port from the external TileLink bus.
+ **tieOffSlaveTLPort** `() => Unit` tie the slave port for simulation.


### trait HasSlaveTLPortModuleImp
*Actually generates the corresponding IO in the concrete Module.*

~~~scala
trait HasSlaveTLPortModuleImp extends LazyMultiIOModuleImp with HasSlaveTLPortBundle {
  val outer: HasSlaveTLPort
  val l2_frontend_bus_tl = IO(outer.l2FrontendTLNode.bundleIn)
}
~~~

## Simulation

### class SimAXIMem
*Memory with AXI port for use in elaboratable test harnesses.*

+ **node** `AXI4BlindInputNode` the input port of the simulation RAM.
+ **module** `LazyModuleImp` (lazy) the actual module implementation.
  - **io.axi4** `HeterogeneousBag[TLBundle]` the IO Bundle.

Internal connection:
~~~
AXI RAM input ==> AXI4Fragmenter ==> AXI4Buffer ==> AXI4RAM
~~~

<br><br><br><p align="right">
<sub>
Last updated: 15/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
