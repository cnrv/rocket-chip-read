[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[Xbar](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/Xbar.scala)
=====================
*Generic Tilelink crossbar.*

**********************

### class TLXbar

~~~scala
class TLXbar(policy: TLArbiter.Policy = TLArbiter.roundRobin)(implicit p: Parameters) extends LazyModule
~~~

+ **policy** `TLArbiter.Policy` (param) the arbitration algorithm used in arbiters.
+ **node** `TLNexusNode` the diplomacy object to record port connections for module generation.
+ **module** `LazyModuleImp`
  - **io** `Bundle` module I/O ports:<br>
    **in** `HeterogeneousBag[TLBundle]` input ports.<br>
    **out** `HeterogeneousBag[TLBundle]` output ports.<br>
  - **inputIdRanges** `Seq[IdRange]` ranges of input (client) ports. **_Resolved at module generation time._**
  - **outputIdRanges** `Seq[IdRange]` ranges of output (manager) ports. **_Pre-assigned._**
  - **outputPorts** `Seq[(addr: UInt) => Bool]` address route functions.
  - **wide_bundle** `TLBundleParameters`<br>
    A Bundle parameter wide enough to represent all input and output ports. **_Resolved at module generation time._**
  - **addressA, addressC** `Seq[UInt]` target addresses of channel A and C.
  - **requestAIO, requestCIO** `Seq[Bool]` client to manager (I to O) one-hot route result for channel A and C.
  - **requestBOI, requestDOI** `Seq[Bool]` manager to client (O to I) one-hot route result for channel B and D.
  - **requestEIO** `Seq[Bool]` client to manager (I to O) one-hot route result for channel E.
  - **beatsAI, beatsBO, beatsCI, beatsDO, beatsEI** `Seq[UInt]` number of beats in the busrt (AXI style, N-1).
  - **portsAOI, portsBIO, portsCOI, portsDIO, portsEOI**, `Seq[Seq[TLBundleX]]`<br>
    Demulplexed connections from input to outputs.

The data-width of all ports must be equal.
The sourceId and fifoId are reordered to reduce their range.
This range shrink is defined in the case variables of `node`: `clientFn` and `managerFn`.


### object TLXbar

+ **mapInputIds** `(Seq[TLClientPortParameters]) => Seq[IdRange]`<br>
  Resolve id range of input ports at binding time. **_All input port should have a non-zero range, otherwise exception!_**
+ **mapOutputIds** `(Seq[TLClientPortParameters]) => Seq[IdRange]`<br>
  Get the assigned output id range of all managers.
+ **assignRanges** `(Seq[Int] => Seq[IdRange])` Internal function used by mapInputIds() and mapOutputIds().
+ **relabeler** `(Int) => Int` shrink the range of fifoId. Internal function used by TLXbar.node.managerFn().
+ **fanout** `(DecoupledIO[T], Seq[Bool]) => Vec[DecoupledIO[T]]` demultiplexing input port for output connection.


<br><br><br><p align="right">
<sub>
Last updated: 18/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
