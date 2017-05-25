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

<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 25/05/2017</sub></p>
