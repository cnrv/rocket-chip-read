[Rocket](../Readme.md)/[rocket](../rocket.md)/[Arbiters](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/rocket/Arbiter.scala)
========================
*The Arbiters used in the Rocket core.*

*****************

class HellaCacheArbiter
-------------------------
*The arbiter used to arbitate DCache requests from core, ROCC, FPU, PTW, etc.*

~~~scala
class HellaCacheArbiter(n: Int)(implicit p: Parameters) extends Module
~~~

+ I/O, type and Paramter

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| n                      | Int              | param      | number of requestors                  |
| p                      | Parameters       | param      | configuration                         |
| requestor              | Vec[HellaCacheIO] | I         | requestors from core, rocc, fpu, etc. |
| mem                    | HellaCacheIO     | O          | arbitrated request to DCache.         |

+ Notes:
  + Static priority with 0 the highest.
  + Core is connected to lowest priority?
  + 3 cycles:<br>
    cycle 0: arbitrate requests<br>
    cycle 1: send out kill and write data<br>
    cycle 2: collect response from DCache

class InOrderArbiter
-------------------------
*Legacy arbiter used in ROCC.*

~~~scala
class InOrderArbiter[T <: Data, U <: Data](reqTyp: T, respTyp: U, n: Int)
    (implicit p: Parameters) extends Module
~~~


<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 21/05/2017</sub></p>
