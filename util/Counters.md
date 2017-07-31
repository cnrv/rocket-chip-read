[Rocket](../Readme.md)/[util](../util.md)/[Counters](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/util/Counters.scala)
========================
*Counters.*
*Utilizing the Chisel2 compatability layer.*

************************

object TwoWayCounter
-------------------
*A two way counter*

+ **apply** `(up: Bool, down: Bool, max: Int) => UInt`<br>
  Count up when `up && !down`, down when `down && !up`, width of output is `log2Up(max+1)`.

case class WideCounter
------------------
*a counter that clock gates most of its MSBs using the LSB carry-out*

~~~scala
case class WideCounter(width: Int, inc: UInt = UInt(1), reset: Boolean = true)
~~~
+ **width** `Int` the width of the counter.
+ **inc** `UInt` the increment value.
+ **reset** `Boolean` reset to 0.
+ **value** `UInt` the counter value.
+ **:=** `(x: UInt) => Unit` set counter value to `x`.

<br><br><br><p align="right">
<sub>
Last updated: 09/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
