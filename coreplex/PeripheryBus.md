[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[PeripheryBus](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/PeripheryBus.scala)
========================
*The periphery bus for IO devices.*

**********************

## case class PeripheryBusParams
*Parameters used by the peripherial bus.*

~~~scala
case class PeripheryBusParams(
  beatBytes: Int,
  blockBytes: Int,
  masterBuffering: BufferParams = BufferParams.default,
  slaveBuffering: BufferParams = BufferParams.none,
  arithmetic: Boolean = true,
  frequency: BigInt = BigInt(100000000) // 100 MHz as default bus frequency
) extends TLBusParams {
}
~~~

+ **beatBytes** `Int` (param) number of bytes per beat.
+ **blockBytes** `Int` (param) number of bytes per burst.
+ **masterBuffering** `BufferParams.default` (param) buffer depth on the master (inner) side.
+ **slaveBuffering** `BufferParams.none` (param) buffer depth on the slave (outer) side.
+ **arithmetic** `true` (param) support arithmetic atomic operations.
+ **frequency** `BigInt(100000000)` (param) 100MHz as default bus frequency.

## class PeripheryBus

~~~scala
class PeripheryBus(params: PeripheryBusParams)(implicit p: Parameters) extends TLBusWrapper(params)
~~~

+ **toFixedWidthSingleBeatSlave** `(w:Int) => TLOutwardNode` attach a fragmenter to change beat size to `w`.
+ **toLargeBurstSlave** `(m:Int) => TLOutwardNode` attach a fragmenter to change block size to `m`.
+ **fromSystemBus** `() => TLInwardNode` get the peripheral bus inward port attached with an atomic automata.

The internal connections:
~~~
                 [atomics]       master_buffer      xbar      slave_buffer       slave_ww           []
systemBus ==> -------------- ==> ------------- *==> ---- ==>* ------------ ==>* ----------- ==> ---------- ==> FixWidthSlave
              AtomicAutomata         Buffer         Xbar          Buffer  |     WidthWidget     Fragmenter
                                                                          |
                                                                          |                         []
                                                                          \---------------- ==> ---------- ==> LargeBurstSlave
                                                                                                Fragmenter
~~~

## trait HasPeripheryBus
*Provides buses that serve as attachment points, for use in traits that connect individual devices or external ports.*

+ **pbus** `PeripheryBus` the peripheral bus.


<br><br><br><p align="right">
<sub>
Last updated: 10/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
