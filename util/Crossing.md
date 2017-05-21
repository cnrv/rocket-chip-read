[Rocket](../Readme.md)/[util](../util.md)/[Crossing](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/util/Crossing.scala)
========================


**********************

class CrossingIO
---------------------
*The IO used for cross clock domain interface.*

~~~scala
class CrossingIO[T <: Data](gen: T) extends Bundle
~~~

+ I/O, type and Paramter

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| T                      | Data             | type       | payload type                          |
| gen                    | T                | param      | type parameter                        |
| enq\_clock             | Clock            | I          | source side clock                     |
| enq\_reset             | Bool             | I          | source side reset                     |
| enq                    | DecoupledIO[T]   | I          | source side write port                |
| deq\_clock             | Clock            | I          | sink side clock                       |
| deq\_reset             | Bool             | I          | sink side reset                       |
| deq                    | DecoupledIO[T]   | O          | sink side write port                  |


class Crossing
---------------
*Base module of cross clock domain modules.*

~~~scala
abstract class Crossing[T <: Data] extends Module {
  val io: CrossingIO[T]
}
~~~


<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 17/04/2017</sub></p>

