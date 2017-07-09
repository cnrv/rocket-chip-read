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



<br><br><br><p align="right">
<sub>
Last updated: 08/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
