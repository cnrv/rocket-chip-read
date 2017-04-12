[Rocket](../Readme.md)/[util](../util.md)/[AsyncQueue](https://github.com/ucb-bar/rocket-chip/tree/master/src/main/scala/util/AsyncQueue.scala)
========================


**********************

object GrayCounter
-----------------------
*A gray counter*

+ **apply** `(bits: Int, increment: Bool = Bool(true), clear: Bool = Bool(false), name: String = "binary") => UInt`<br>
  The actual register is binary formated.

object UIntSyncChain
-----------------------
*A register FIFO chain.*

+ **apply** `(in: UInt, sync: Int, name: String = "gray") => UInt`<br>
  `sync`: the depth of the FIFO.




**********************

```scala
last_modified = 12/04/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
