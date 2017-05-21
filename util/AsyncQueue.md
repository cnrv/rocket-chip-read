[Rocket](../Readme.md)/[util](../util.md)/[AsyncQueue](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/util/AsyncQueue.scala)
========================


**********************

class AsyncQueue extends [Crossing](Crossing.md#class-crossing)
------------------
*A cross clock domain queue.*

~~~scala
class AsyncQueue[T <: Data](gen: T, depth: Int = 8, sync: Int = 3, safe: Boolean = true) extends Crossing[T]
~~~

+ I/O, type and Paramter

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| T                      | Data             | type       | payload type                          |
| gen                    | T                | param      | type parameter                        |
| depth                  | Int = 8          | param      | size of queue                         |
| sync                   | Int = 3          | param      | depth of clock synchronizer           |
| safe                   | Boolean = true   | param      | whether enforce self-satble           |
| enq\_clock             | Clock            | I          | source side clock                     |
| enq\_reset             | Bool             | I          | source side reset                     |
| enq                    | DecoupledIO[T]   | I          | source side write port                |
| deq\_clock             | Clock            | I          | sink side clock                       |
| deq\_reset             | Bool             | I          | sink side reset                       |
| deq                    | DecoupledIO[T]   | O          | sink side write port                  |

It is better to set `safe` to true if source and sink do not share the same reset.

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

class AsyncValidSync
----------------------
*A 1-bit FIFO chain.*

~~~scala
class AsyncValidSync(sync: Int, desc: String) extends Module
~~~

+ I/O and Paramter

| name                   | type   | direction  | description                       |
| :---                   | :--:   | :--:       | :---                              |
| sync                   | Int    | param      | depth of the FIFO                 |
| desc                   | String | param      | name of the FIFO                  |
| in                     | Bool   | I          | input                             |
| out                    | Bool   | O          | output                            |

class AsyncQueueSource
----------------
*A corss clock-domain queue, the part on the soruce side.*

~~~scala
class AsyncQueueSource[T <: Data](gen: T, depth: Int, sync: Int, safe: Boolean = true) extends Module
~~~

+ I/O, type and Paramter

| name                   | type             | direction  | description                          |
| :---                   | :--:             | :--:       | :---                                 |
| T                      | Data             | type       | payload type                         |
| gen                    | T                | param      | type parameter                       |
| depth                  | Int              | param      | size of queue                        |
| sync                   | Int              | param      | depth of clock synchronizer          |
| safe                   | Boolean          | param      | whether enforce self-satble          |
| enq                    | DecoupledIO[T]   | I          | write port for source                |
| ridx                   | UInt             | I          | read pointer from sink (grey code)   |
| widx                   | UInt             | O          | write pointer for source (grey code) |
| mem                    | Vec[T]           | O          | queue content for sink to read       |
| sink_reset_n           | Bool             | I          | sink side reset (active low)         |
| ridx\_valid            | Bool             | I          | sink side read pointer valid         |
| widx\_valid            | Bool             | O          | source side write pointer valid      |

When safe is set high, source side is able to write when the read pointer is valid and synchronoized
(sync+1 cycle delay).

class AsyncQueueSink
-------------------------
*A corss clock-domain queue, the part on the sink side.*

~~~scala
class AsyncQueueSink[T <: Data](gen: T, depth: Int, sync: Int, safe: Boolean = true) extends Module
~~~

+ I/O, type and Paramter

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| T                      | Data             | type       | payload type                          |
| gen                    | T                | param      | type parameter                        |
| depth                  | Int              | param      | size of queue                         |
| sync                   | Int              | param      | depth of clock synchronizer           |
| safe                   | Boolean          | param      | whether enforce self-satble           |
| deq                    | DecoupledIO[T]   | O          | read port for sink                    |
| ridx                   | UInt             | O          | read pointer for sink (grey code)     |
| widx                   | UInt             | I          | write pointer from source (grey code) |
| mem                    | Vec[T]           | I          | queue content for sink to read        |
| source_reset_n         | Bool             | I          | sink side reset (active low)          |
| ridx\_valid            | Bool             | O          | sink side read pointer valid          |
| widx\_valid            | Bool             | I          | source side write pointer valid       |

When safe is set high, sink side is able to read when the write pointer is valid and synchronoized
(sync+1 cycle delay).


<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 16/04/2017</sub></p>

