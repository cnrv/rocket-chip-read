[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[IntNodes](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/IntNodes.scala)
=====================

**********************

## case class IntRange
*a range for interrupt lines [start, end)*

~~~scala
case class IntRange(start: Int, end: Int)
~~~

+ **start**`Int` (param) start of the range, inclusive.
+ **end** `Int` (param) end of the range, exclusive.
+ **size** `() => Int` the size of the range.
+ **overlaps** `(IntRange) => Boolean` whether two ranges overlaps.
+ **offset** `(x:Int) => IntRange(start+x, end+x)` shift a range.

### object IntRange
+ **apply** `(end:Int) => IntRange(0,end)` (implicit)  generate a range.

## case class IntSourceParameters
*Parameter for a shared interrupt port (downwards).*

~~~scala
case class IntSourceParameters(
  range:     IntRange,
  resources: Seq[Resource] = Seq(),
  nodePath:  Seq[BaseNode] = Seq())
~~~

+ **range** `IntRange` (param) the interrupt range of this source.
+ **resources** `Seq[Resource]` (param)
+ **nodePath** `Seq[BaseNode]` (param)
+ **name** `String` use the lazyModule's name as name.

## case class IntSinkParameters
*Parameter for a shared interrupt port (upwards).*

~~~scala
case class IntSinkParameters(
  nodePath:  Seq[BaseNode] = Seq())
~~~

+ **nodePath** `Seq[BaseNode]` (param)
+ **name** `String` use the lazyModule's name as name.

## case class IntSourcePortParameters
*U type used for interrupt node.*

~~~scala
case class IntSourcePortParameters(sources: Seq[IntSourceParameters])
~~~

+ **source** `Seq[IntSourceParameters]` (param) parameters of the transactions sharing the same port
+ **num** `Int` the number ofinterrupt lines.

### object IntSourcePortSimple
+ **apply** `(num:Int = 1, ports:Int = 1, sources:Int = 1, resources:Seq[Resource] = Nil) => Seq[IntSourceParameters]`<br>
  A simple function to generate inital `IntSourcePortParameters`. **Note: the generated ranges need legalization.**

## case class IntSinkPortParameters

*D type used for interrupt node.*

~~~scala
case class IntSinkPortParameters(sinks: Seq[IntSinkParameters])
~~~
+ **sink** `Seq[IntSinkParameters]` (param) parameters of the transactions sharing the same port

### IntSinkPortSimple
+ **apply** `(ports:Int = 1, sinks:Int = 1) => Seq[IntSinkParameters]`<br>
  A simple function to generate inital `IntSinkPortParameters`. **Note: the generated ranges need legalization.**

## case class IntEdge
*E type used for interrupt node.*
~~~scala
case class IntEdge(source: IntSourcePortParameters, sink: IntSinkPortParameters)
~~~

## object IntImp

~~~scala
object IntImp extends NodeImp[IntSourcePortParameters, IntSinkPortParameters, IntEdge, IntEdge, Vec[Bool]]
~~~

+ **edgeI** `(IntSourcePortParameters, IntSinkPortParameters) => IntEdge` get the input edge parameter.
+ **edgeO** `(IntSourcePortParameters, IntSinkPortParameters) => IntEdge` get the output edge parameter.
+ **bundleI** `(IntEdge) => Vec[Bool]` get input bundle.
+ **bundleO** `(IntEdge) => Vec[Bool]` get output bundle.
+ **color** `() => "#0000ff"` blue.
+ **reverse** `() => true` reverse IO direction.
+ **labelI** `(IntEdge) => String` label input edge with the number of interrupts.
+ **labelO** `(IntEdge) => String` label output edge with the number of interrupts.
+ **connect** `(bo: => Vec[Bool], bi: => Vec[Bool], ei: => IntEdge) => (m:Option[LazyModule], bind:()=>Unit)`<br>
  Connect inputs with outputs.
+ **mixO** `(IntSinkPortParameters, InwardNode[IntSourcePortParameters, IntSinkPortParameters, Vec[Bool]]) => IntSourcePortParameters`<br>
  Insert node into parameters.
+ **mixI** `(IntSinkPortParameters, InwardNode[IntSourcePortParameters, IntSinkPortParameters, Vec[Bool]]) => IntSourcePortParameters`<br>
  Insert node into parameters.

## Interrupt extension of basic Nodes

+ case class **IntIdentityNode**       extends IdentityNode
+ case class **IntSourceNode**         extends SourceNode
+ case class **IntSinkNode**           extends SinkNode
+ case class **IntNexusNode**          extends NexusNode
+ case class **IntOutputNode**         extends OutputNode
+ case class **IntInputNode**          extends InputNode
+ case class **IntBlindOutputNode**    extends BlindOutputNode
+ case class **IntBlindInputNode**     extends BlindInputNode
+ case class **IntInternalOutputNode** extends InternalOutputNode
+ case class **IntInternalInputNode**  extends InternalInputNode

## class IntXbar
*A crossbar for interrupts.*

The interrupt range are rearranged.

~~~scala
class IntXbar()(implicit p: Parameters) extends LazyModule
~~~

+ **intnode** `IntNexusNode` the diplomacy object to record port connections for module generation.
+ **module** `LazyModuleImp`
  - **io** `Bundle` module I/O ports:<br>
    **in** `Vec[Bool]` input ports.<br>
    **out** `Vec[Bool]` output ports.<br>

## class IntXing
*Interrupt input synchronizer.*

~~~scala
class IntXing(sync: Int = 3)(implicit p: Parameters) extends LazyModule
~~~

+ **sync** `Int` number of pipeline needed to synchronize the interrupt signal.
+ **intnode** `IntIdentityNode` the diplomacy object to record port connections for module generation.
+ **module** `LazyModuleImp`
  - **io** `Bundle` module I/O ports:<br>
    **in** `Vec[Bool]` input ports.<br>
    **out** `Vec[Bool]` output ports.<br>

For each `out`, it is sync pipelined of `in`.

~~~scala
out := (0 to sync).foldLeft(in) { case (a, _) => RegNext(a) }
~~~



<br><br><br><p align="right">
<sub>
Last updated: 21/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>

