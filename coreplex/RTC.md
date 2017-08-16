[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[RTC](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/RTC.scala)
========================
*Real-time counter.*

**********************

## HasRTCModuleImp

~~~scala
trait HasRTCModuleImp extends LazyMultiIOModuleImp {
  val outer: HasPeripheryClint
}
~~~

+ **outer** `HasPeripheryClint` (virtual) pointer to the outer LazyModule extended with `HasPeripheryClint`.
+ **pbusFreq** `BigInt` (private) the frequency of the peripheral bus.
+ **rtcFreq** `BigInt` (private) the frequency of the RTC.
+ **internalPeriod** `BigInt = pbusFreq / rtcFreq` (private) internal counter period.

`outer.clint.module.io.rtcTick` is set to high for one peripheral clock cycle at the frequency of `rtcFreq`.

<br><br><br><p align="right">
<sub>
Last updated: 16/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
