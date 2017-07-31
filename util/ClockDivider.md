[Rocket](../Readme.md)/[util](../util.md)/[ClockDivider](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/util/ClockDivider.scala)
========================
*Verilog blackbox of clock divider.*
*Utilizing the Chisel2 compatability layer.*

************************

class ClockDivider2
---------------------
*Blockbox of dividing clock by 2.*

~~~verilog
module ClockDivider2 (output reg clk_out, input clk_in);
   initial clk_out = 1'b0;
   always @(posedge clk_in) begin
      clk_out = ~clk_out; // Must use =, NOT <=
   end
endmodule // ClockDivider2
~~~

class Pow2ClockDivider
-----------------
*A configurable clock divider.*

~~~scala
class Pow2ClockDivider(pow2: Int) extends Module
~~~

+ I/O, type and Paramter

| name                   | type             | direction  | description                          |
| :---                   | :--:             | :--:       | :---                                 |
| pow2                   | Int              | param      | set divide ratio to 2^pow2           |
| clock\_out             | Clock            | O          | divided clock                        |



<br><br><br><p align="right">
<sub>
Last updated: 09/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
