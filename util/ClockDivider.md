[Rocket](../Readme.md)/[util](../util.md)/[ClockDivider](https://github.com/ucb-bar/rocket-chip/tree/master/src/main/scala/util/ClockDivider.scala)
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



<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 18/04/2017</sub></p>

