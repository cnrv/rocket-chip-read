[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[Xbar](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/Xbar.scala)
=====================
*Generic Tilelink crossbar.*

**********************

### class TLXbar

~~~scala
class TLXbar(policy: TLArbiter.Policy = TLArbiter.roundRobin)(implicit p: Parameters) extends LazyModule
~~~

+ **node** `TLNexusNode`
+ **module** `LazyModuleImp`
  - **io** `Bundle` module I/O ports:<br>
    **in** `HeterogeneousBag[AXI4Bundle]` input ports.<br>
    **out** `HeterogeneousBag[AXI4Bundle]` output ports.<br>
  - **inputIdRanges** `Seq[IdRange]` ranges of input (client) ports. **_Resolved at module generation time._**
  - **outputIdRanges** `Seq[IdRange]` ranges of output (manager) ports. **_Pre-assigned._**
  - **outputPorts** `(addr: UInt) => Seq[Bool]` one-hot address route function.
  - **wide_bundle** `TLBundleParameters`<br>
    A Bundle parameter wide enough to represent all input and output ports. **_Resolved at module generation time._**


### object TLXbar

+ **mapInputIds** `(Seq[TLClientPortParameters]) => Seq[IdRange]`<br>
  Resolve id range of input ports at binding time. **_All input port should have a non-zero range, otherwise exception!_**
+ **mapOutputIds** `(Seq[TLClientPortParameters]) => Seq[IdRange]`<br>
  Get the assigned output id range of all managers.
+ **assignRanges** `(Seq[Int] => Seq[IdRange])` Internal function used by mapInputIds().


<br><br><br><p align="right">
<sub>
Last updated: 13/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
