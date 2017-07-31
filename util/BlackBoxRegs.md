[Rocket](../Readme.md)/[util](../util.md)/[BlackBoxRegs](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/util/BlackBoxRegs.scala)
========================
*Asynchronous reset registers.*

**********************

class AsyncResetReg
------------
*A register with an asynchronous reset.*

~~~scala
class AsyncResetReg extends BlackBox
~~~

This is a Verilog blackbox of the following:

~~~verilog
module AsyncResetReg(input clk, rst, en, d, output reg q);
  always @(posedge clk or posedge rst)
    if (rst)     q <= 1'b0;
    else if (en) q <= d;
endmodule // AsyncResetReg
~~~

class AsyncResetRegVec
------------
*An asynchronously reset register vector.*

~~~scala
class AsyncResetRegVec(val w: Int, val init: BigInt) extends Module
~~~

This is a Verilog blackbox of the following:

~~~verilog
module AsyncResetRegVec#(w,init) (input clk, rst, en, input [w-1:0] d, output reg [w-1:0] q);
  always @(posedge clk or posedge rst)
    if (rst)     q <= init;
    else if (en) q <= d;
endmodule // AsyncResetRegVec
~~~

object AsyncResetReg
-------------
*Asynchronously reset register generators.*

Arguments:

| name       |  type          |  description                    |
| :--        | :--:           | :--                             |
| clk        | Clock          | clock                           |
| rst        | Bool           | positive active reset           |
| d          | Bool           | 1-bit register input            |
| q          | Bool           | 1-bit register output           |
| init       | Boolean        | 1-bit register initial value    |
| updateData | UInt           | register input                  |
| outputData | UInt           | register output                 |
| resetData  | BigInt         | register initial value          |
| enable     | Bool           | register enable                 |
| name       | Option[String] | Verilog entity name             |

+ 1-bit register generators:<br>
  **apply** `(d, clk, rst, init, name) => q`<br>
  **apply** `(d, clk, rst) => q`<br>
  **apply** `(d, clk, rst, name) => q`

+ register generators:<br>
  **apply** `(updateData, resetData, enable) => outputData`<br>
  **apply** `(updateData, resetData, enable, name) => outputData`<br>
  **apply** `(updateData, resetData) => outputData`<br>
  **apply** `(updateData, resetData, name) => outputData`<br>
  **apply** `(updateData, enable) => outputData`<br>
  **apply** `(updateData, enable, name) => outputData`<br>
  **apply** `(updateData) => outputData`<br>
  **apply** `(updateData, name) => outputData`<br>


<br><br><br><p align="right">
<sub>
Last updated: 09/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
