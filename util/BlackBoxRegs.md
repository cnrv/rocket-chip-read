[Rocket](../Readme.md)/[util](../util.md)/[BlackBoxRegs](https://github.com/ucb-bar/rocket-chip/tree/master/src/main/scala/util/BlackBoxRegs.scala)
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


**********************

```scala
last_modified = 18/04/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
