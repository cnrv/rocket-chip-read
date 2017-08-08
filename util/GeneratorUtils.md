[Rocket](../Readme.md)/[util](../util.md)/[GeneratorUtils](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/util/GeneratorUtils.scala)
========================
*Utilities used when generating FIRRTL for a LazyModule.*

**********************

## case class ParsedInputNames
*Representation of the information this Generator needs to collect from external sources.*

~~~scala
case class ParsedInputNames(
    targetDir: String,
    topModuleProject: String,
    topModuleClass: String,
    configProject: String,
    configs: String)
~~~

+ **targetDir** `String` (param) the target file directory for the generated FIRRTL code.
+ **topModuleProject** `String` (param) name of the scala package that the target design (LazyModule) belongs to.
+ **topModuleClass** `String` (param) name of the target design (LazyModule) to be compiled into FIRRTL.
+ **configProject** `String` (param) name of the scala package that the configure parameter class belings to.
+ **configs** `String` (param) names of the configure parameter classes used for the target design.
+ **fullConfigClasses** `Seq[String]` a list of the configure classes.
+ **fullTopModuleClass** `String` the full name of the target design.

## trait GeneratorApp
*The scala trait acting as the main entry point of FIRRTL generation.*

~~~scala
trait GeneratorApp extends App with HasGeneratorUtilities
~~~

+ **names** `ParsedInputNames` (lazy) the names of the target design, configure classes and file directoy from user input.
  >~~~
  >#sbt example
  >run TargetDir TopModuleProjectName TopModuleName ConfigProjectName ConfigNameString
  >~~~

+ **generateArtefacts** `() => Unit` execute all callbacks to generate the files defined in `ElaborationArtefacts`.

## object ElaborationArtefacts
*Record the files that will be generated beside the FIRRTL during the Chisel compilation process.*

+ **files** `Seq[(ext:String, func:() => String)]` list of callback functions.
  - **ext** `String` the file extension used by this generated file.
  - **func** `() => String` the callback that will be executed by the code generator.
+ **add** `(ext:String, content: => String)` push `(ext, ()=>content)` to the callback list `files`.


<br><br><br><p align="right">
<sub>
Last updated: 08/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
