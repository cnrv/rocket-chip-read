[Rocket](../Readme.md)/[regmapper](../regmapper.md)/[RegisterCrossing](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/regmapper/RegisterCrossing.scala)
========================
*Register interface for crossing power domains.*

**********************

class BusyRegisterCrossing
----------------
*A cross domain register interface.*
*When `io.bypass` is asserted, it ignores the next request with an immediated response.*
*Used as the control logic for an actual data crossing.*

~~~scala
class BusyRegisterCrossing extends Module
~~~

+ I/O

| name                   | type   | direction  | description                       |
| :---                   | :--:   | :--:       | :---                              |
| bypass                 | Bool   | I          | ignore the next request           |
| master_request_valid   | Bool   | I          | request valid from master         |
| master_request_ready   | Bool   | O          | ready for a request from master   |
| master_response_valid  | Bool   | O          | a request is sent                 |
| master_response_ready  | Bool   | I          | master ready for response         |
| crossing_request_valid | Bool   | O          | a request forwarded to slave      |
| crossing_request_ready | Bool   | I          | a request is received by slave    |

class RegisterWriteCrossing
-----------------
*Register crossing write interface module.*

~~~scala
class RegisterWriteCrossing[T <: Data](gen: T, sync: Int = 3) extends Module
~~~

+ I/O

| name                   | type                  | direction  | description                       |
| :---                   | :--:                  | :--:       | :---                              |
|||||
| master\_clock          | Clock                 | I          | clock of the master domain        |
| master\_reset          | Bool                  | I          | reset of the master domain        |
| master\_port.request   | DecoupledIO\[T\]      | I          | request from master               |
| master\_port.response  | IrrevocableIO\[Bool\] | O          | response for master               |
| master\_bypass         | Bool                  | I          | ignore the next request           |
|||||
| slave\_clock           | Clock                 | I          | clock of the slave domain         |
| slave\_reset           | Bool                  | I          | reset of the slave domain         |


<br><br><br><p align="right">
<sub>
Last updated: 08/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
