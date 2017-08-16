[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[ResetVector](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/ResetVector.scala)
========================
*Constants to define the reset addresses.*

**********************

## trait HasResetVectorWire
*A single place for all tiles to find out the reset vector.*

~~~scala
trait HasResetVectorWire {
  implicit val p: Parameters
  val resetVectorBits = p(ResetVectorBits)
  val global_reset_vector = Wire(UInt(width = resetVectorBits))
}
~~~

+ **resetVectorBits** `Int` the bit size of the reset vector.
+ **global_reset_vector** `UInt` the reset address come from BootROM, and now this is a port rather than a compile time constant.


<br><br><br><p align="right">
<sub>
Last updated: 16/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
