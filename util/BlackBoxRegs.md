[Rocket](../Readme.md)/[util](../util.md)/[BlackBoxRegs](https://github.com/ucb-bar/rocket-chip/tree/master/src/main/scala/util/BlackBoxRegs.scala)
========================


**********************

class AsyncResetReg
------------
*A register with an asynchronous reset.*

~~~scala
class AsyncResetReg extends BlackBox
~~~

This is a Verilog blackbox of the following:

~~~verilog
always @(posedge clk or posedge rst)
  if (rst)     q <= 1'b0;
  else if (en) q <= d;
~~~

class AsyncResetRegVec
------------
*An asynchronously reset register vector.*

~~~scala
class AsyncResetRegVec(val w: Int, val init: BigInt) extends Module
~~~

This is a Verilog blackbox of the following:

~~~verilog
logic [w-1:0] q;

always @(posedge clk or posedge rst)
  if (rst)     q <= init;
  else if (en) q <= d;
~~~




**********************

```scala
last_modified = 10/04/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
