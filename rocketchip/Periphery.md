[Rocket](../Readme.md)/[rocketchip](../rocketchip.md)/[Periphery](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/rocketchip/Periphery.scala)
=====================

**********************

## HasPeripheryParameters
*Parameters for peripherials.*

+ **peripheryBusConfig** `() => TLBusConfig`
+ **peripheryBusBytes** `() => Int` byte width of peripheral bus.
+ **socBusConfig** `() => TLBusConfig`
+ **socBusBytes** `() => Int` byte width of SoC bus.
+ **cacheBlockBytes** `() => Int` byte size of a cache block.
+ **peripheryBusArithmetic** `() => Boolean`
+ **nMemoryChannels** `() => Int` number of memory channels.
+ **nExtInterrupts** `() => Int` number of external interrupt lines.



<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 29/06/2017</sub></p>
