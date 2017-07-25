[Rocket](../Readme.md)/[tile](../tile.md)/[Interrupts](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tile/Interrupts.scala)
========================


**********************

## class TileInterrupts
*The interrupt ports for a Rocket core (CSRFile).*

~~~scala
class TileInterrupts(implicit p: Parameters) extends CoreBundle()(p)
~~~

- **debug** `Bool` debug interrupt.
- **mtip** `Bool` timer interrupt pending for machine mode.
- **msip** `Bool` software interrupt pending for machine mode.
- **meip** `Bool` external interrupt pending for machine mode.
- **seip** `Option[Bool]` external interrupt pending for supervisor mode (only when VM is enabled, why?).
- **lip** `Vec[Bool]` local interrupt lines. (what for?)

## trait HasExternalInterrupts
*Use diplomatic interrupts to external interrupts from the coreplex into the tile.*

~~~scala
trait HasExternalInterrupts extends HasTileParameters {
  implicit val p: Parameters
  val module: HasExternalInterruptsModule
}
~~~

+ **module** `HasExternalInterruptsModule` pointer to the module implementation.
+ **intNode** `IntSinkNode(IntSinkPortSimple())`
+ **csrIntMap** `() => List[Int]` map interrupt to their pin in CSR: mip.<br>
  List(debug:65535, msip:3, mtip:7, meip:11, Option[seip:9], Option[local interrupts:\_+16])

## trait HasExternalInterruptsBundle

~~~scala
trait HasExternalInterruptsBundle {
  val outer: HasExternalInterrupts
  val interrupts = outer.intNode.bundleIn
}
~~~

## trait HasExternalInterruptsModule

~~~scala
trait HasExternalInterruptsModule {
  val outer: HasExternalInterrupts
  val io: HasExternalInterruptsBundle
}
~~~

+ **outer** `HasExternalInterrupts` pointer to the LazyModule.
+ **io** `HasExternalInterruptsBundle` IO ports, inputs only.
+ **decodeCoreInterrupts** `(core:TileInterrupts) => Unit` assign input signals to internal interrupt lines `core`.

<br><br><br><p align="right">
<sub>
Last updated: 25/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
