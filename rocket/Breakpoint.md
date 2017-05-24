[Rocket](../Readme.md)/[rocket](../rocket.md)/[Breakpoint](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/rocket/Breakpoint.scala)
========================
*Breakpoint unit.*

*****************

class BPControl
-----------------------
*Definitions of the breakpoint trigger control (tdata1, mcontrol).*

+ Field definition

| name                   | type             | description                           |
| :---                   | :--:             | :---                                  |
| ttype                  | UInt             | trigger type (currently fixed to address/data match)  |
| dmode                  | Bool             | whether M can write trigger data (0 for yes) |
| maskmax                | UInt             | address alignment used in match       |
| action                 | Bool             | action when trigger matches (incompliant)  |
| chain                  | Bool             | match triggers sequentially           |
| tmatch                 | UInt             | match mode (incompliant)              |
| m                      | Bool             | enable this trigger in M              |
| h                      | Bool             | enable this trigger in H              |
| s                      | Bool             | enable this trigger in S              |
| u                      | Bool             | enable this trigger in U              |
| x                      | Bool             | fire this trigger on EX               |
| w                      | Bool             | fire this trigger on store            |
| r                      | Bool             | fire this trigger on load             |

class BreakpointUnit
-----------------------------
*Breakpoint unit*


+ I/O, type and parameters

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| p                      | Parameters       | param      | configuration                         |
| status                 | MStatus          | I          | system status                         |
| bp                     | Vec[BP]          | I          | breakpoint configuration from CSR     |
| pc                     | UInt             | I          | pc from IF                            |
| ea                     | UInt             | I          | load/store address                    |
| xcpt\_if               | Bool             | O          | breakpoint triggered from mtaching pc |
| xcpt\_ld               | Bool             | O          | breakpoint triggered from load addr   |
| xcpt\_st               | Bool             | O          | breakpoint triggered from store addr  |
| debug\_if              | Bool             | O          | debug action for IF                   |
| debug\_ld              | Bool             | O          | debug action for load                 |
| debug\_st              | Bool             | O          | debug action for store                |


<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 24/05/2017</sub></p>


