[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[SystemBus](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/SystemBus.scala)
========================
*The coherent bus between tiles and coherent hubs (also split memory and I/O spaces).*

**********************

## case class SystemBusParams
*Parameters used by the system bus.*

~~~scala
case class SystemBusParams(
  beatBytes: Int,
  blockBytes: Int,
  masterBuffering: BufferParams = BufferParams.default,
  slaveBuffering: BufferParams = BufferParams.flow // TODO should be BufferParams.none on BCE
) extends TLBusParams
~~~

+ **beatBytes** `Int` number of bytes per beat.
+ **blockBytes** `Int` number of bytes per burst.
+ **masterBuffering** `BufferParams.default` buffer depth on the master (inner) side.
+ **slaveBuffering** `BufferParams.flow` buffer depth on the slave (outer) side.

## class SystemBus

~~~scala
class SystemBus(params: SystemBusParams)(implicit p: Parameters) extends TLBusWrapper(params)
~~~

## trait HasSystemBus
*Provides buses that serve as attachment points, for use in traits that connect individual devices or external ports.*


<br><br><br><p align="right">
<sub>
Last updated: 09/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
