[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[IntNodes](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/IntNodes.scala)
=====================

**********************

## case class IntRange
*a range for interrupt lines [start, end)*

~~~scala
case class IntRange(start: Int, end: Int)
~~~

+ **start**`Int` start of the range, inclusive.
+ **end** `Int` end of the range, exclusive.
+ **size** `() => Int` the size of the range.
+ **overlaps** `(IntRange) => Boolean` whether two ranges overlaps.
+ **offset** `(x:Int) => IntRange(start+x, end+x)` shift a range.

### object IntRange
+ **apply** `(end:Int) => IntRange(0,end)` (implicit)  generate a range.





<br><br><br><p align="right">
<sub>
Last updated: 21/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>

