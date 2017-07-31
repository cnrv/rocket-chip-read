[Rocket](../Readme.md)/[rocket](../rocket.md)/[HellaCacheArbiter](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/rocket/HellaCacheArbiter.scala)
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


<br><br><br><p align="right">
<sub>
Last updated: 08/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
