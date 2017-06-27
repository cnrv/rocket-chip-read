[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[RocketTiles](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/RocketTiles.scala)
========================


**********************

### Rocket Tiles

#### HasRocketTiles
*Trait of the Rocket Tiles.*

~~~scala
trait HasRocketTiles extends CoreplexRISCVPlatform {
  val module: HasRocketTilesModule
}
~~~

+ Derived from [CoreplexRISCVPlatform](RISCVPlatform.md#coreplexriscvplatform)
+ **module** `HasRocketTilesModule` pointer to the generated module.
+ **tileParams** `Seq[RocketTileParams] = p(RocketCrossing)` parameters of individual tiles.
+ **localIntNodes** `Seq[Option[IntInputNode]` interrupt port for local interrupt sources.
+ **wiringTuple** `Seq[(Option[IntInputNode], RocketTileParams, Int)]` tuple of (intrrupt, tile, index).
+ **rocketWires** `Seq[HasRocketTilesBundle => Unit]` <TODO>






<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 28/06/2017</sub></p>
