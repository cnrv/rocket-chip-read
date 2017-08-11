[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[BaseCoreplex](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/BaseCoreplex.scala)
========================
*The base class of a Rocket-chip.*

**********************

+ [BareCoreplex](#barecoreplex)
+ [BaseCoreplex](#basecoreplex)

**********************


## BareCoreplex
*BareCoreplex is the root class for creating a coreplex sub-system.*

### abstract class BareCoreplex
*Bare-metal coreplex.*
**_Herre the trait `BindingScope` denotes that all coreplex may generate a device tree description._**

~~~scala
abstract class BareCoreplex(implicit p: Parameters) extends LazyModule with BindingScope {
  lazy val dts = DTS(bindingTree)
  lazy val dtb = DTB(dts)
  lazy val json = JSON(bindingTree)
}
~~~

+ **dts** `String` (lazy) the device tree in human readable format generated from `BindingScope.bindingTree`.
+ **dtb** `Seq[Byte]` (lazy) the binary formated device tree.
+ **json** `String` (lazy) the JSON formated device tree records.

### abstract class BareCoreplexModule
*Bare-metal module implementation for all coreplexes.*

~~~scala
abstract class BareCoreplexModule[+L <: BareCoreplex](_outer: L) extends LazyMultiIOModuleImp(_outer) {
  val outer = _outer
}
~~~

+ **\_outer** `BareCoreplex` (param) provide the parent coreplex LazyModule.
+ **outer** `BareCoreplex` point to the coreplex LazyModule.

Register the callbacks to generate files for node connection graph (.graphml) and device tree in plain (.dts) and JSON (.json) formats.
Also print out device tree in compilation stdout.

## BaseCoreplex
*Base Coreplex class with no peripheral devices or ports added.*

~~~
      +------+       +------+      +------+       +-------+
      | Tile |       | Tile |      | port |       | master|
      +------+       +------+      +------+       +-------+
          |*             |*            |*             |*
          |              |             |              |
     +----+----+    +----+----+   +----+----+    +----+----+
     |FIFOFixer|    |FIFOFixer|   |FIFOFixer|    |FIFOFixer|
     +---------+    +---------+   +---------+    +---------+
             |*          |*         |*                |*
             |           |          |                 |
            ++-----------+----------++                |
            |        Splitter        |                |
            +------------------------+                |
                         |*                           |
                         |   system-bus               |
      +-----+------------+----------------------------+-------+---------+
            |                                                 |
            |*                                                |*
        +------+                                          +------+
        |Buffer|                                          |Buffer|
        +------+                                          +---+--+
            |*                                                |
            |  memory-bus                                     |*
   +---+----+--------------+----+                       +-----------+
       |                   |                            |WidthWidget|
       |*                  |*                           +-----+-----+
   +------+            +------+                               |
   |Buffer|            |Buffer|                        +------+-------+
   +---+--+            +---+--+                        |AtomicAutomata|
       |                   |                           +------+-------+
       |                   |*                                 |
       |             +-----------+                         +--+---+
       |             | Fragmenter|                         |Buffer|
       |             +-----+-----+                         +------+
       |                   |                                  |*
       |                   |*                                 |  periphery-bus
+------+-------+   +----------------+           +----+--------+---------+----+
|    DRAM      |   | variable width |                |                  |
+--------------+   |     slave      |                |*                 |*
                   +----------------+            +------+           +------+
                                                 |Buffer|           |Buffer|
                                                 +---+--+           +---+--+
                                                     |                  |
                                                     |                  |
                                                     |            +-----+-----+
                                                     |            |WidthWidget|
                                                     |            +-----+-----+
                                                     |                  |
                                               +-----+-----+      +-----+-----+
                                               | Fragmenter|      | Fragmenter|
                                               +-----+-----+      +-----+-----+
                                                     |                  |
                                               +-----+-----+      +-----+-----+
                                               |Single Beat|      |Large Burst|
                                               |   Slave   |      |  Slave    |
                                               +-----------+      +-----------+
~~~


### abstract class BaseCoreplex
*Base coreplex.*

~~~scala
abstract class BaseCoreplex(implicit p: Parameters) extends BareCoreplex
    with HasInterruptBus
    with HasSystemBus
    with HasPeripheryBus
    with HasMemoryBus {
  override val module: BaseCoreplexModule[BaseCoreplex]
}
~~~

+ **root** `Device` the top of device tree (why define root here, assuming coreplex is always the top or the big cores?).
+ **soc** `Device` the system on chip entry of the device tree.
+ **cpus** `Device` the processors in the device tree.
+ **topManagers** `Option[Seq[TLManagerParameters]]` (lazy) unified manager parameters.

### abstract class BaseCoreplexModule

+ **ranges** `Seq[AddressRange]` (private) the address spaces of all components on the system bus.
+ **jason** `Seq[String]` intermediate string list describing the address ranges.

What does this module do:
- Generate memory map file `memmap.jason`.
- Check that all address spaces have been described by the device tree.

<br><br><br><p align="right">
<sub>
Last updated: 11/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
