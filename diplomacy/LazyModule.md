[Rocket](../Readme.md)/[diplomacy](../diplomacy.md)/[LazyModule](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/diplomacy/LazyModule.scala)
=====================

**********************

abstract class LazyModule
----------------------
*Module generator. Allow run-time module configuration and generation.*

+ **bindings** `List[() => Unit]` A list of port connection functions called during instantiation.
+ *children: List[LazyModule]*: list of inner components (LazyModules).
+ **nodes** `List[BaseNode]` the nodes inside this module (think about ports of a crossbar)
+ *info: SourceInfo*: source information (line number, etc.) for better error/warning messages.
+ *parent: Option[LazyModule]*: parent module.
+ *suggestName: (x:String) => Unit*: set the suggested module name?
+ *moduleName: _ => String*: ??
+ *instanceName: _ => String*: ??
+ *name: _ => String*: ??
+ *line: _ => String*: get source line string.
+ *module: _ => LazyModuleImp*: get the actual chisel Module implementation.
+ *instantiate: _ => Unit*: instantiate all children after run-time configuration. (called by LazyModuleImp)
+ *graphML: String*: node connection graph in graphML.
+ *nodeIterator: (iterfunc: (LazyModule) => Unit) => Unit*: a cross hierarchy module traveller.

object LazyModule
------------------------
*Companion object for LazyModule.*

+ *stack: List[LazyModule]*: A list of all LazyModules remaining to be processed (recursively).
+ *apply[T <: LazyModule]: (bc:T) => bc*: LazyModule wrapper to enforce the LazyModule process order.

abstract class LazyModuleImp
------------------------
    abstract class LazyModuleImp(outer: LazyModule) extends Module

*The actual Module implementation of a LazyModule.*

+ *val p: Parameters*: configuration from the paired LazyModule.








<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 21/04/2017</sub></p>
