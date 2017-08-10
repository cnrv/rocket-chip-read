[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[MemoryBus](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/MemoryBus.scala)
========================
*The memory bus after LLC.*

**********************

## case class BroadcastParams
*L2 Broadcast Hub configuration*

~~~scala
case class BroadcastParams(
  nTrackers:  Int     = 4,
  bufferless: Boolean = false)
~~~

+ **nTrackers** `Int` (param) number of transaction trackers.
+ **bufferless** `Boolean` (param)

## case class BankedL2Params
*L2 memory subsystem configuration*

~~~scala
case class BankedL2Params(
  nMemoryChannels:  Int = 1,
  nBanksPerChannel: Int = 1,
  coherenceManager: (Parameters, HasMemoryBus) => (TLInwardNode, TLOutwardNode) = { case (q, _) =>
    implicit val p = q
    val MemoryBusParams(_, blockBytes, _, _) = p(MemoryBusParams)
    val BroadcastParams(nTrackers, bufferless) = p(BroadcastParams)
    val bh = LazyModule(new TLBroadcast(blockBytes, nTrackers, bufferless))
    (bh.node, bh.node)
  }) {
  val nBanks = nMemoryChannels*nBanksPerChannel
}
~~~

+ **nMemoryChannels** `Int` (param) number of parallel memory channels (parameter from the memory controller).
+ **nBanksPerChannel** `Int` (param) number of banks per memory cahnnel.
+ **coherenceManager** `(Parameters, HasMemoryBus) => (TLInwardNode, TLOutwardNode)`<br>
  (param) a coherence hub generation function, return the inwards and outwards ports of the hub.
+ **nBanks** `Int` (param) the total number of banks.

## case class MemoryBusParams
*Parameterization of the memory-side bus created for each memory channel*

~~~scala
case class MemoryBusParams(
  beatBytes: Int,
  blockBytes: Int,
  masterBuffering: BufferParams = BufferParams.none,
  slaveBuffering: BufferParams = BufferParams.none
) extends TLBusParams
~~~

+ **beatBytes** `Int` (param) number of bytes per beat.
+ **blockBytes** `Int` (param) number of bytes per burst.
+ **masterBuffering** `BufferParams.none` (param) buffer depth on the master (inner) side.
+ **slaveBuffering** `BufferParams.none` (param) buffer depth on the slave (outer) side.

## class MemoryBus
*Wrapper for creating TL nodes from a bus connected to the back of each mem channel*

~~~scala
class MemoryBus(params: MemoryBusParams)(implicit p: Parameters) extends TLBusWrapper(params)(p)
~~~

## trait HasMemoryBus

~~~scala
trait HasMemoryBus extends HasSystemBus with HasPeripheryBus with HasInterruptBus
~~~



<br><br><br><p align="right">
<sub>
Last updated: 10/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
