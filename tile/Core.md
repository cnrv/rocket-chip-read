[Rocket](../Readme.md)/[tile](../tile.md)/[BaseTile](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tile/BaseTile.scala)
========================
*Generic core class.*

**********************

## trait CoreParams
*The parameter needed by all core implementaions.*

+ **useVM** `Boolean` (param) whether to support virtual memory.
+ **useUser** `Boolean` (param) whether to support user mode.
+ **useDebug** `Boolean` (param) whether to support the run-control debug.
+ **useAtomics** `Boolean` (param) whether to support the RISC-V A extension.
+ **useCompressed** `Boolean` (param) whether to support the RISC-V C extension.
+ **mulDiv** `Option[MulDivParams]` (param) (optional) the parameter class for the integer multiplier (divider).
+ **fpu** `Option[FPUParams]` (param) (optional) the parameter class for the floating point unit.
+ **fetchWidth** `Int`<br>
  Set the instruction fetcher's data width to `fetchWidth * instBits` bits (currently fixed to 32 for Rocket).
+ **decodeWidth** `Int` number of instructions to be decoded per cycle.
+ **retireWidth** `Int` number of instructions to be commited per cycle.
+ **instBits** `Int` the size of the smallest instruction (16 for RVC otherwise 32).
+ **nLocalInterrupts** `Int`<br>
  Number of local interrupt lines (which are directly fed to the MIP CSR). (is this spec compatible or Rocket special?)
+ **nL2TLBEntries** `Int` number of L2 TLB entries (added by PR #849, not exactly sure what is this L2 TLB and PTW).

## trait HasCoreParameters
*Apply CoreParam to local variables.*

~~~scala
trait HasCoreParameters extends HasTileParameters {
  val coreParams: CoreParams = tileParams.core
~~~

Content omitted.

## abstract class CoreModule
*Generic core implementation.*

~~~scala
abstract class CoreModule(implicit val p: Parameters) extends Module
  with HasCoreParameters
~~~

## abstract class CoreBundle
*Base bundle for core IO.*

~~~scala
abstract class CoreBundle(implicit val p: Parameters) extends ParameterizedBundle()(p)
  with HasCoreParameters
~~~

## trait HasCoreIO
*Core IO specific to Rocket-like.*

~~~scala
trait HasCoreIO extends HasTileParameters {
  implicit val p: Parameters
  val io = new CoreBundle()(p) with HasExternallyDrivenTileConstants {
    val interrupts = new TileInterrupts().asInput
    val imem  = new FrontendIO
    val dmem = new HellaCacheIO
    val ptw = new DatapathPTWIO().flip
    val fpu = new FPUCoreIO().flip
    val rocc = new RoCCCoreIO().flip
  }
}
~~~

- port inherited from `HasExternallyDrivenTileConstants`
  + **hartid** `UInt` the hartid.<br>
  + **resetVector** `UInt` the reset pc address.
- **interrupts** `TileInterrupts` interrupts input.
- **imem** `FrontendIO` instruction fetch interface with the instruction cache.
- **dmem** `HellaCacheIO` data interface with the data cache / scratchpad.
- **ptw** `DatapathPTWIO` interface with the hardware page table walker.
- **fpu** `FPUCoreIO` interface with the floating point unit.
- **rocc** `RoCCoreIO` interface with the Rocket custom coprocessor.



<br><br><br><p align="right">
<sub>
Last updated: 27/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
