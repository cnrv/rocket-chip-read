[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[Arbiter](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/Arbiter.scala)
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


<br><br><br><p align="right">
<sub>
Last updated: 12/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
