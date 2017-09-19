[Rocket](../../Readme.md)/[devices](../../devices.md)/[tilelink](../tilelink.md)/[Plic](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/devices/tilelink/Plic.scala)
========================
*platform-level interrupt controller*

**********************

### class LevelGateway
*Gateway components for level interrupts.*

+ I/O, type and Paramter

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| interrupt              | Bool             | I          | level interrupt line.                 |
| plic.valid             | Bool             | O          | interrupt pending to PLIC.            |
| plic.ready             | Bool             | I          | PLIC ready for new interrupts.        |
| plic.complete          | Bool             | I          | the inflight interrupt served by PLIC.|

The incoming `interrupt` is edged into a pulse to `plic.valid` whenever PLIC is `ready`.
When PLIC finishes serving an interrupt, it sets `plic.complete` to reset the current inflight interrupt, allowing for new interrupt.

*Question: it seems if the last interrupt is stuck, the incoming interrupt can be lost if its level signal is not edged early enough.*

### object PLICConsts
*Constants used by PLIC.*

+ **maxDevices** `() => 1023`
+ **maxHarts** `() => 15872`
+ **priorityBase** `() => 0x0`
+ **pendingBase** `() => 0x1000`
+ **enableBase** `() => 0x2000`
+ **hartBase** `() => 0x200000`
+ **claimOffset** `() => 4`
+ **priorityBytes** `() => 4`
+ **enableOffset** `(i:Int) => Int`
+ **hartOffset** `(i:Int) => i * 0x1000`
+ **enableBase** `(i:Int) => Int`
+ **hartBase** `(i:Int) => Int`
+ **size** `() => Int`



<br><br><br><p align="right">
<sub>
Last updated: 19/09/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
