[Rocket](../Readme.md)/[util](../util.md)/[Counters](https://github.com/ucb-bar/rocket-chip/tree/master/src/main/scala/util/Counters.scala)
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

**********************

```scala
last_modified = 18/04/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
