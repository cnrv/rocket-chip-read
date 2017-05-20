[Rocket](../../Readme.md)/[uncore](../../uncore.md)/[tilelink2](../tilelink2.md)/[Arbiter](https://github.com/ucb-bar/rocket-chip/blob/master/src/main/scala/uncore/tilelink2/Arbiter.scala)
=====================
*Tilelink arbiter.*

**********************

object TLArbiter
--------------------------

+ **lowestIndexFirst** `(Seq[Bool], Bool) => Seq[Bool]`<br>
  The default arbitration policy.
+ **lowestFromSeq** `[T <: TLChannel](edge: TLEdge, sink: DecoupledIO[T], sources: Seq[DecoupledIO[T]]) => Unit`<br>
  Connect sources and the sink using the lowestIndexFirst policy.
+ **lowest**`[T <: TLChannel](edge: TLEdge, sink: DecoupledIO[T], sources: DecoupledIO[T]*) => Unit`<br>
  Connect sources and the sink using the lowestIndexFirst policy.
+ **apply** `[T <: Data](policy: Policy)(sink: DecoupledIO[T], sources: (UInt, DecoupledIO[T])*) => Unit`<br>
  Use the specified policy to arbitrate sources. Support bursts.


<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 19/04/2017</sub></p>

