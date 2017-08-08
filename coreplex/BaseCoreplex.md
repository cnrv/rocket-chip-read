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

### abstract class BaseCoreplex
### abstract class BaseCoreplexModule

<br><br><br><p align="right">
<sub>
Last updated: 08/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>


