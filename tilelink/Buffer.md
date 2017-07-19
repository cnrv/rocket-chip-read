[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[Buffer](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/Buffer.scala)
=====================
*Buffer for TileLink channels.*

**********************


## class TLBuffer

~~~scala
class TLBuffer(
  a: BufferParams,
  b: BufferParams,
  c: BufferParams,
  d: BufferParams,
  e: BufferParams)(implicit p: Parameters) extends LazyModule
~~~

+ **a,b,c,d,e** `BufferParams` (param) buffer parameters specific to each sub-channel.
+ **this** `(ace:BufferParams, bd:BufferParams) => TLBuffer`<br>
  A constructor with separate parameters for A/C/E and B/D.
+ **this** `(BufferParams) => TLBuffer` A constructor with a parameter set to all channels.
+ **this** `() => TLBuffer`<br>
  A constructor use the `BufferParams.default` parameter set to all channels (`BufferParams(2, false, false)`).
+ **node** `TLAdapterNode` the diplomacy object to record port connections for module generation.
+ **module** `LazyModuleImp`
  - **io** `Bundle` module I/O ports:<br>
    **in** `HeterogeneousBag[TLBundle]` input ports.<br>
    **out** `HeterogeneousBag[TLBundle]` output ports.<br>

## object TLBuffer

+ **apply()** `() => TLBuffer`<br>
  Generate a buffer using `BufferParams.default` (`BufferParams(2, false, false)`).
+ **apply** `(BufferParams) => TLBuffer` generate a buffer using the same parameter.
+ **apply** `(ace:BufferParams, bd:BufferParams) => TLBuffer`<br>
  Generate a buffer using separate parameters for A/C/E and B/D.
+ **apply** `(BufferParams, BufferParams, BufferParams, BufferParams, BufferParams) => TLBuffer`<br>
  Generate a buffer using individual parameters.


<br><br><br><p align="right">
<sub>
Last updated: 19/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
