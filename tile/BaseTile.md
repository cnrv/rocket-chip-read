[Rocket](../Readme.md)/[tile](../tile.md)/[BaseTile](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tile/BaseTile.scala)
========================
*The set of base classes for tiles.*

**********************

- **[BareTile](#baretile)** The base tile definition of all tiles, even the BaseTile.
- **[BaseTile](#basetile)** The tile used by Rocket, which has a TileLink master port.

**********************

## BareTile

### abstract class BareTile
*The base class of all tiles, even the BaseTile.*

~~~scala
abstract class BareTile(implicit p: Parameters) extends LazyModule
~~~

### abstract class BareTileBundle
*The base bundle class of all tiles, even the BaseTile.*

~~~scala
abstract class BareTileBundle[+L <: BareTile](_outer: L) extends GenericParameterizedBundle(_outer) {
  val outer = _outer
  implicit val p = outer.p
}
~~~

### abstract class BareTileModule
*The base tile implementation for all tiles, including BaseTile.*

~~~scala
abstract class BareTileModule[+L <: BareTile, +B <: BareTileBundle[L]](_outer: L, _io: () => B) extends LazyModuleImp(_outer) {
  val outer = _outer
  val io = _io ()
}
~~~

## BaseTile

### trait HasTileLinkMasterPort
*The Tilelink node definition for a base tile.*
~~~scala
trait HasTileLinkMasterPort {
  implicit val p: Parameters
  val module: HasTileLinkMasterPortModule
  val masterNode = TLOutputNode()
  val tileBus = LazyModule(new TLXbar) // TileBus xbar for cache backends to connect to
  masterNode := tileBus.node
}
~~~

- **module** pointer to the implementation.
- **masterNode** `TLOutputNode` a Tile is a TileLink output node, a master on the system bus.
- **tileBus** `LazModule[TLXbar]` the internal TileLink bus for the I$, D$, RoCC, etc.

### trait HasTileLinkMasterPortBundle
*The bundle for the base tile (TileLink master port) (cake pattern).*

~~~scala
trait HasTileLinkMasterPortBundle {
  val outer: HasTileLinkMasterPort
  val master = outer.masterNode.bundleOut
}
~~~

### trait HasTileLinkMasterPortModule
*The base implementation for the base tile's master port (cake pattern).*

~~~scala
trait HasTileLinkMasterPortModule {
  val outer: HasTileLinkMasterPort
  val io: HasTileLinkMasterPortBundle
}
~~~

### trait HasExternallyDrivenTileConstants
*The constant value driven as input ports.*

~~~scala
trait HasExternallyDrivenTileConstants extends Bundle {
  implicit val p: Parameters
  val hartid = UInt(INPUT, p(MaxHartIdBits))
  val resetVector = UInt(INPUT, p(ResetVectorBits))
}
~~~

- **hartid** `UInt` the hartid.<br>
  **_If the hartid is an input port, why there are some modules still take hartid as a parameter?_**
- **resetVector** `UInt` the reset pc address.

### abstract class BaseTile
*Base tile.*

~~~scala
abstract class BaseTile(tileParams: TileParams)(implicit p: Parameters) extends BareTile
    with HasTileParameters
    with HasTileLinkMasterPort {
  override lazy val module = new BaseTileModule(this, () => new BaseTileBundle(this))
}
~~~

### class BaseTileBundle
*Bundle for a base tile.*

~~~scala
class BaseTileBundle[+L <: BaseTile](_outer: L) extends BareTileBundle(_outer)
    with HasTileLinkMasterPortBundle
    with HasExternallyDrivenTileConstants
~~~

### class BaseTileModule
*Base implemenation of a tile.*

~~~scala
class BaseTileModule[+L <: BaseTile, +B <: BaseTileBundle[L]](_outer: L, _io: () => B) extends BareTileModule(_outer, _io)
    with HasTileLinkMasterPortModule
~~~


<br><br><br><p align="right">
<sub>
Last updated: 27/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
