[Rocket](../Readme.md)/[util](../util.md)/[AsyncBundle](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/util/AsyncBundle.scala)
========================
*Unified cross clock-domain queue interface.*
*Utilizing the Chisel2 compatability layer.*

************************

final class AsyncBundle
-------------------
*The unified cross clock-domain queue interface.*

~~~scala
final class AsyncBundle[T <: Data](val depth: Int, gen: T) extends Bundle
~~~

+ I/O, type and Paramter

| name                   | type             | direction  | description                          |
| :---                   | :--:             | :--:       | :---                                 |
| T                      | Data             | type       | payload type                         |
| depth                  | Int              | param      | size of queue                        |
| gen                    | T                | param      | type parameter                       |
| mem                    | Vec[T]           | U          | queue content for sink to read       |
| ridx                   | UInt             | U.flip     | read pointer from sink (grey code)   |
| widx                   | UInt             | U          | write pointer for source (grey code) |
| ridx\_valid            | Bool             | U.flip     | sink side read pointer valid         |
| widx\_valid            | Bool             | U          | source side write pointer valid      |
| source_reset_n         | Bool             | U          | source side reset (active low)       |
| sink_reset_n           | Bool             | U.flip     | sink side reset (active low)         |

object FromAsyncBundle
------------------
*Function to convert an `AsyncBundle` input interface to a `DecoupledIO` output.*

+ **apply** `[T <: Data](AsyncBundle[T], sync: Int = 3) => DecoupledIO[T]`

object ToAsyncBundle
--------------------
*Function to convert a `ReadyValudIO` input to an `AsyncBundle` output.*

+ **apply** `[T <: Data](ReadyValidIO[T], depth: Int = 8, sync: Int = 3) => AsyncBundle[T]`







<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 25/05/2017</sub></p>

