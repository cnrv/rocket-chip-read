[Rocket](../Readme.md)/[util](../util.md)/[Arbiters](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/util/Arbiters.scala)
========================
*Rocket extended arbiters.*
*Utilizing the Chisel2 compatability layer.*

************************

class HellaPeekingArbiter
----------------------
*A arbiter support bursts of variable length.*

~~~scala
class HellaPeekingArbiter[T <: Data](
      typ: T, arbN: Int,
      canUnlock: T => Bool,
      needsLock: Option[T => Bool] = None,
      rr: Boolean = false)
    extends HellaLockingArbiter(typ, arbN, rr)
~~~

+ I/O, type and Paramter

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| T                      | Data             | type       | payload type                          |
| typ                    | T                | param      | type parameter                        |
| arbN                   | Int              | param      | number of ports                       |
| canUnlock              | T => Bool        | param      | function to detect tail               |
| needsLock              | Option[T => Bool] = None | param | function to detect burst           |
| rr                     | Boolean = false  | param      | whether to use round-robin (static by default) |
| in                     | Vec[DecoupledIO[T]] | I       | arbiter input ports                   |
| out                    | DecoupledIO[T]   | O          | arbiter output port                   |


class HellaCountingArbiter
-----------------------
*A arbiter support bursts of constant length.*

~~~scala
class HellaCountingArbiter[T <: Data](
      typ: T, arbN: Int, count: Int,
      val needsLock: Option[T => Bool] = None,
      rr: Boolean = false)
    extends HellaLockingArbiter(typ, arbN, rr)
~~~

+ I/O, type and Paramter

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| T                      | Data             | type       | payload type                          |
| typ                    | T                | param      | type parameter                        |
| arbN                   | Int              | param      | number of ports                       |
| count                  | Int              | param      | number of beat in a burst             |
| needsLock              | Option[T => Bool] = None | param | function to detect burst           |
| rr                     | Boolean = false  | param      | whether to use round-robin (static by default) |
| in                     | Vec[DecoupledIO[T]] | I       | arbiter input ports                   |
| out                    | DecoupledIO[T]   | O          | arbiter output port                   |


<br><br><br><p align="right">
<sub>
Last updated: 09/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
