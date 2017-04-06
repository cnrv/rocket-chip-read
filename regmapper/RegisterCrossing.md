[Rocket](../Readme.md)/[regmapper](../regmapper.md)/[RegisterCrossing](https://github.com/ucb-bar/rocket-chip/tree/master/src/main/scala/regmapper/RegisterCrossing.scala)
========================


**********************

class BusyRegisterCrossing
----------------

~~~scala
class BusyRegisterCrossing extends Module
~~~

+ I/O

| name                   | type   | direction  | description                       |
| :---                   | :--:   | :--:       | :---                              |
| bypass                 | Bool   | I          |                                   |
| master_request_valid   | Bool   | I          |                                   |
| master_request_ready   | Bool   | O          |                                   |
| master_response_valid  | Bool   | O          |                                   |
| master_response_ready  | Bool   | I          |                                   |
| crossing_request_valid | Bool   | O          |                                   |
| crossing_request_ready | Bool   | I          |                                   |

+ Signals

| name                   | type      | initial    | description                       |
| :---                   | :--:      | :--:       | :---                              |
| busy                   | Reg(Bool) | false      |                                   |
| bypass                 | Reg(Bool) |            |                                   |






**********************

```scala
last_modified = 06/04/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
