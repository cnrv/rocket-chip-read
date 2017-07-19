[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[FIFOFixer](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/FIFOFixer.scala)
=====================


**********************

## class TLFIFOFixer

~~~scala
class TLFIFOFixer(implicit p: Parameters) extends LazyModule
~~~

+ **node** `TLAdapterNode` the diplomacy object to record port connections for module generation.
+ **module** `LazyModuleImp`
  - **io** `Bundle` module I/O ports:<br>
    **in** `HeterogeneousBag[TLBundle]` input ports.<br>
    **out** `HeterogeneousBag[TLBundle]` output ports.<br>
  - **a_id** `Seq[UInt]` get the target `fifoId` using the address for channel A.
  - **a_nid** `UInt` high when no `fifoId` is found.
  - **a_first** `Bool` whether it is the first beat in a burst.
  - **d_first** `Bool` whether it is the first beat in a burst.



## object TLFIFOFixer



<br><br><br><p align="right">
<sub>
Last updated: 19/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
