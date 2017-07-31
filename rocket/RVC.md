[Rocket](../Readme.md)/[rocket](../rocket.md)/[RVC](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/rocket/RVC.scala)
========================
*RVC decoder.*

*****************

class ExpandedInstruction
------------------
*Norm form of instruction after RVC decoding.*


+ Bundle component

| name                   | type             | description                           |
| :---                   | :--:             | :---                                  |
| bits                   | UInt             | the decoded 32-bit instruction        |
| rd                     | UInt             | index of the destination register     |
| rs1                    | UInt             | index of the source register 1        |
| rs2                    | UInt             | index of the source register 2        |
| rs3                    | UInt             | index of the source register 3        |

class RVCExpander
-------------------------
*RVC decoder unit.*

+ I/O, type and parameters

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| p                      | Parameters       | param      | configuration                         |
| in                     | UInt             | I          | raw instruction                       |
| out                    | [ExpandedInstruction](#class-expandedinstruction) | O | decoded instruction |
| rvc                    | Bool             | O          | whether the output instruction is compressed |

<br><br><br><p align="right">
<sub>
Last updated: 08/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
