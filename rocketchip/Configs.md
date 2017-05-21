[Rocket](../Readme.md)/[rocketchip](../rocketchip.md)/[Configs](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/rocketchip/Configs.scala)
=====================

*Available configuration parameters for the Rocket-Chip generator.*

class BasePlatformConfig
----------------
*Basic configuration parameters*

+ **TLCombinationalCheck** `Boolean = false`

    Adding connections between valid and ready to form a loop is `valid` depends on `ready`.
    This will cause combinational loop check failures in synthesis tools.
    Also test components are added to dump garabage to check corrupt data during `!valid` is safe.


<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 27/03/2017</sub></p>

