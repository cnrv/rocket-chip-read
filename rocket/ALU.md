[Rocket](../Readme.md)/[rocket](../rocket.md)/[ALU](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/rocket/ALU.scala)
========================
*Rocket ALU implementation.*

*****************

class ALU
-------------------
*Rocket ALU*

+ I/O, type and Paramter

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| p                      | Parameters       | param      | configuration                         |
| dw                     | Bits             | I          | datawidth: `DW_64` `DW_32`           |
| fn                     | Bits             | I          | ALU function                          |
| in1                    | UInt             | I          | ALU input 1                           |
| in2                    | UInt             | I          | ALU input 2                           |
| out                    | UInt             | O          | ALU output                            |
| adder\_out             | UInt             | O          | address for D$                        |
| cmp\_out               | Bool             | O          | compare result                        |



<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 20/05/2017</sub></p>
