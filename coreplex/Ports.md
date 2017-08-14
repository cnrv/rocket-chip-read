[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[Ports](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/Ports.scala)
========================
*Provide various traits to add ports to the system, in some cases converting to different interconnect standards.*

************************

- [Parameters](#parameters)
- [AXI4 Memory](#axi4-memory)

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

## AXI4 Memory

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


<br><br><br><p align="right">
<sub>
Last updated: 14/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
