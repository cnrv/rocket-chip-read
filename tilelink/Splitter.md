[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[Splitter](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/Splitter.scala)
=====================
*Demultiplexer for TileLink channels.*

**********************

## class TLSplitter

~~~scala
class TLSplitter(policy: TLArbiter.Policy = TLArbiter.roundRobin)(implicit p: Parameters) extends LazyModule
~~~

+ **policy** `TLArbiter.Policy` (param) the arbitration algorithm used in arbiters.
+ **node** `TLSplitterNode` the diplomacy object to record port connections for module generation.
+ **module** `LazyModuleImp`
  - **io** `Bundle` module I/O ports:<br>
    **in** `HeterogeneousBag[TLBundle]` input ports.<br>
    **out** `HeterogeneousBag[TLBundle]` output ports.<br>
  - **outputIdRanges** `Seq[IdRange]` ranges of output (manager) ports. **_Pre-assigned._**
  - **outputPorts** `Seq[(addr: UInt) => Bool]` address route functions.
  - **wide_bundle** `TLBundleParameters`<br>
    A Bundle parameter wide enough to represent all input and output ports. **_Resolved at module generation time._**

<br><br><br><p align="right">
<sub>
Last updated: 20/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
