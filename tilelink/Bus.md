[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[Bus](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/Bus.scala)
=====================
*Generic TileLink bus implementation.*

**********************

## trait TLBusParams
*Specifies widths of various attachement points in the SoC*

~~~scala
trait TLBusParams {
  val beatBytes: Int
  val blockBytes: Int
  val masterBuffering: BufferParams
  val slaveBuffering: BufferParams
}
~~~

+ **beatBytes** `Int` number of bytes per beat.
+ **blockBytes** `Int` number of bytes per burst.
+ **masterBuffering** `BufferParams` buffer depth on the master (inner) side.
+ **slaveBuffering** `BufferParams` buffer depth on the slave (outer) side.
+ **beatBits** `() => Int` get the bit size of a beat.
+ **blockBits** `() => Int` get the bit size of a burst.
+ **blockBeats** `() => Int` get the number of beats in a burst.
+ **blockOffset** `() => Int` get the width of byte index inside a burst.

## abstract class TLBusWrapper
*Wrap a TLXbar into a bus.*

~~~scala
abstract class TLBusWrapper(params: TLBusParams)(implicit p: Parameters) extends TLBusParams
~~~

+ **xbar** `TLXbar` (private) the internal crossbar.
+ **master_buffer** `TLBuffer` (private) buffer on the master side.
+ **slave_buffer** `TLBuffer` (private) buffer on the slave side.
+ **slave_frag** `TLFragmenter` (private) fragmenter, tune the size of beats.
+ **slave_ww** `TLWidthWidget` (private) fix width mismatch between client and manager.
+ **outwardNode** `() => TLOutwardNode` (protected) get the crossbar output.
+ **outwardBufNode** `() => TLOutwardNode` (protected) get the outer buffer output.
+ **outwardFragNode** `() => TLOutwardNode` (protected) get the fragmenter output.
+ **outwardWWNode** `() => TLOutwardNode` (protected) get the width fixer output.
+ **inwardNode** `() => TLInwardNode` (protected) get the crossbar input.
+ **inwardBufNode** `() => TLInwardNode` (protected) get the inner buffer input.
+ **bufferFromMasters** `() => TLInwardNode` get the inner buffer input.
+ **bufferToSlaves** `() => TLOutwardNode` get the outer buffer output.
+ **toAsyncSlaves** `(Int) => TLAsyncOutwardNode` get the crossbar output with an asynchronous synchronizer.
+ **toRationalSlaves** `(Int) => TLRationalOutwardNode` get the crossbar output with a rational synchronizer.
+ **toVariableWidthSlaves** `() => TLOutwardNode` get the fragmenter output.
+ **toAsyncVariableWidthSlaves** `() => TLAsyncOutwardNode` get the fragmenter output with an asynchronous synchronizer.
+ **toRationalVariableWidthSlaves** `() => TLRationalOutwardNode` get the fragmenter output with a rational synchronizer.
+ **toFixedWidthSlaves** `() => TLOutwardNode` get the width fixer output.
+ **toAsyncFixedWidthSlaves** `() => TLAsyncOutwardNode` get the width fixer output with an asynchronous synchronizer.
+ **toRationalFixedWidthSlaves** `() => TLRationalOutwardNode` get the width fixer output with a rational synchronizer.


The internal connections:
~~~
master_buffer       xbar       slave_buffer        slave_ww
------------- *===> ---- ===>* ------------ ===>* -----------
     Buffer         Xbar          Buffer   |      WidthWidget
                                           |
                                           |      slave_frage
                                           \===>* -----------
                                                  Fragmenter
~~~


<br><br><br><p align="right">
<sub>
Last updated: 09/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
