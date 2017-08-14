[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[RocketTiles](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/RocketTiles.scala)
========================
*Extending coreplex with Rocket tiles.*

**********************

## Rocket Tiles
*Negotiate the interrupt, clock and reset connections for Rocket Tiles.*
*Allow for synchronous, asynchronous and rational connections.*

> Local Interrupts must be synchronized to the core clock
> before being passed into this module.
> This allows faster latency for interrupts which are already synchronized.
> The CLINT (coreplex local interrupts) and PLIC (platform level interrupt controller)
> outputs interrupts that are synchronous to the periphery clock,
> so may or may not need to be synchronized depending on the Tile's
> synchronization type.
> Debug interrupt is definitely asynchronous in all cases.


### trait HasRocketTiles
*Trait of the Rocket Tiles.*

~~~scala
trait HasRocketTiles extends HasSystemBus
    with HasPeripheryBus
    with HasPeripheryPLIC
    with HasPeripheryClint
    with HasPeripheryDebug {
  val module: HasRocketTilesModuleImp
}
~~~

+ **module** `HasRocketTilesModule` (virtual) pointer to the generated module.
+ **crossing** `CoreplexClockCrossing` (private) define the clock domain crossing.
+ **tileParams** `Seq[RocketTileParams]` (private) parameters of individual tiles.
+ **localIntCounts** `Seq[Int]` number of interrupt sources of each tile.
+ **localIntNodes** `Seq[Option[IntInputNode]` interrupt port for local interrupt sources.
+ **wiringTuple** `Seq[(Option[IntInputNode], RocketTileParams, Int)]` tuple of (intrrupt, tile, index).
+ **rocket_tiles** `Seq[RocketTileWrapper]` initialize Rocket tiles and produce connection callback functions.
  - **asyncIntXbar** `IntXbar` a per tile crossbar for asycnhronous interrupts, including debug.
  - **periphIntXbar** `IntXbar` a per tile crossbar for peripheral interrupts, including clint (msip+mtip), plic (meip+seip).
  - **coreIntXbar** `IntXbar` a per tile crossbar for local interrupts.

### class ClockedRocketTileInputs
*Base IO bundle for Rocket tiles, which has only the external interrupt lines and constants.*

~~~scala
class ClockedRocketTileInputs(implicit val p: Parameters) extends ParameterizedBundle
    with HasExternallyDrivenTileConstants
    with Clocked
~~~

### trait HasRocketTilesBundle
*Bundle trait of Rocket Tiles.*

~~~scala
trait HasRocketTilesBundle{
  val rocket_tile_inputs: Vec[ClockedRocketTileInputs]
}
~~~

+ **rocket_tile_inputs** `Vec[ClockedRocketTileInputs]` generic IO bundles for tiles, allowing for specialization.

### trait HasRocketTilesModuleImp
*Module implementation trait of Rocket Tiles.*

~~~scala
trait HasRocketTilesModuleImp extends LazyMultiIOModuleImp
    with HasRocketTilesBundle
    with HasResetVectorWire
    with HasPeripheryDebugModuleImp {
  val outer: HasRocketTiles
  val rocket_tile_inputs = Wire(Vec(outer.nRocketTiles, new ClockedRocketTileInputs))
}
~~~

Provide a base trait for all Rocket tile implementations.
Connect the clock, the reset and the constants IO connections.

### class RocketCoreplex
*A Rocket coreplex with Rocket tiles.*

~~~scala
class RocketCoreplex(implicit p: Parameters) extends BaseCoreplex
    with HasRocketTiles {
  override lazy val module = new RocketCoreplexModule(this)
}
~~~

### class RocketCoreplexModule

~~~scala
class RocketCoreplexModule[+L <: RocketCoreplex](_outer: L) extends BaseCoreplexModule(_outer)
    with HasRocketTilesModuleImp
~~~


<br><br><br><p align="right">
<sub>
Last updated: 14/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
