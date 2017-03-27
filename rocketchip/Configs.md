[Rocket](../Readme.md)/[rocketchip](../rocketchip.md)/[Configs](https://github.com/ucb-bar/rocket-chip/blob/master/src/main/scala/rocketchip/Configs.scala)
=====================

*Available configuration parameters for the Rocket-Chip generator.*

class BasePlatformConfig
----------------
*Basic configuration parameters*

+ **TLCombinationalCheck** `Boolean = false`

    Adding connections between valid and ready to form a loop is `valid` depends on `ready`.
    This will cause combinational loop check failures in synthesis tools.
    Also test components are added to dump garabage to check corrupt data during `!valid` is safe.


**********************

```scala
last_modified = 27/03/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
