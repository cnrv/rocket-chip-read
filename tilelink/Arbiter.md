[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[Arbiter](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/Arbiter.scala)
=====================
*Tilelink arbiter.*

**********************

object TLArbiter
--------------------------

+ **Policy** `type: (Integer, UInt, Bool) => UInt` arbitration function used in the arbiter.
+ **lowestIndexFirst** `Policy` the default arbitration policy, lowest index first.
+ **rounRobin** `Policy` round robine policy.
+ **lowestFromSeq** `[T <: TLChannel](edge: TLEdge, sink: DecoupledIO[T], sources: Seq[DecoupledIO[T]]) => Unit`<br>
  Connect sources and the sink using the lowestIndexFirst policy. Support for static sized bursts.
+ **lowest**`[T <: TLChannel](edge: TLEdge, sink: DecoupledIO[T], sources: DecoupledIO[T]*) => Unit`<br>
  Connect sources and the sink using the lowestIndexFirst policy. Support for static sized bursts.
+ **robin**`[T <: TLChannel](edge: TLEdge, sink: DecoupledIO[T], sources: DecoupledIO[T]*) => Unit`<br>
  Connect sources and the sink using the round-robin policy. Support for static sized bursts.
+ **apply** `[T <: Data](policy: Policy)(sink: DecoupledIO[T], sources: (UInt, DecoupledIO[T])*) => Unit`<br>
  Use the specified policy to arbitrate sources. Support variable sizes of bursts.


<br><br><br><p align="right">
<sub>
Last updated: 17/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
