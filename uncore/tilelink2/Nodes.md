[Rocket](../../Readme.md)/[uncore](../../uncore.md)/[tilelink2](../tilelink2.md)/[Nodes](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/uncore/tilelink2/Nodes.scala)
=====================
*TileLink nodes.*

**********************

*TileLink Nodes*

* [Synchronous TileLink Nodes](#synchronous-tilelink-nodes)
* [Asynchronous TileLink Nodes](#object-tlasyncimp)
* [Rational TileLink Nodes](#object-tlrationalimp)

**********************

Synchronous TileLink Nodes
----------------

### object TLImp

*General TileLink module generator.*

~~~scala
object TLImp
    extends NodeImp[
        TLClientPortParameters,  // D
        TLManagerPortParameters, // U
        TLEdgeOut,               // EO
        TLEdgeIn,                // EI
        TLBundle                 // B
        ]
~~~

#### Implementation of abstract methods defined in [`abstract class NodeImp`](../../diplomacy/Nodes.md).

+ **edgeO** `(TLClientPortParameters, TLManagerPortParameters) => TLEdgeOut`<br>
  Function to get the downwards packet generator (channel A/C/E).
+ **edgeI** `(TLClientPortParameters, TLManagerPortParameters) => TLEdgeIn`<br>
  Function to get the upwards packet generator (channel B/D).
+ **bundleO** `(TLEdgeOut) => TLBundle`
  Function to get the downwrads channel bundle (channel A/C/E).
+ **bundleI** `(TLEdgeIn) => TLBundle`
  Function to get the upwards channel bundle (channel B/D).
+ **colour** `_ => "#000000"` black
+ **connect** `(bindings:() => Seq[(TLEdgeIn, TLBundle, TLBundle)]) => (monitor:Option[LazyModule], bind:() => Unit)`<br>
  _bindings_: (packet generator for monitor, input TileLink port, output TileLink port) get the TileLink channel pairs that needs to be connected.<br>
  _monitor_: The monitor to be connected. Depending on parameter [`TLMonitorBuilder`](../../rocketchip/Configs.md)<br>
  _bind_: The actual port binding procedure to be processed later.

### case class TLIdentityNode extends [IdentityNode](../../diplomacy/Nodes.md#class-identitynoded-u-eo-ei-b--data)

~~~scala
case class TLIdentityNode() extends IdentityNode(TLImp)
~~~

### case class TLClientNode extends [SourceNode](../../diplomacy/Nodes.md#class-sourcenoded-u-eo-ei-b-data)

~~~scala
case class TLClientNode(portParams: Seq[TLClientPortParameters]) extends SourceNode(TLImp)(portParams)
~~~

#### object TLClientNode

+ **apply** `(TLClientParameters) => TLClientNode`

### case class TLManagerNode extends [SinkNode](../../diplomacy/Nodes.md#class-sinknoded-u-eo-ei-b-data)

~~~scala
case class TLManagerNode(portParams: Seq[TLManagerPortParameters]) extends SinkNode(TLImp)(portParams)
~~~

#### object TLManagerNode

+ **apply** `(beatBytes: Int, TLManagerParameters) => TLManagerNode`<br>
  _minLatency_ is set to 0.

### case class TLAdapterNode extends [AdapterNode](../../diplomacy/Nodes.md#class-adapternoded-u-eo-ei-b-data)

~~~scala
case class TLAdapterNode(
  clientFn:  TLClientPortParameters  => TLClientPortParameters,
  managerFn: TLManagerPortParameters => TLManagerPortParameters,
  num:       Range.Inclusive = 0 to 999)
  extends AdapterNode(TLImp)(clientFn, managerFn, num)
~~~

### case class TLNexusNode extends [NexusNode](../../diplomacy/Nodes.md#class-nexusnoded-u-eo-ei-b-data)

~~~scala
case class TLNexusNode(
  clientFn:        Seq[TLClientPortParameters]  => TLClientPortParameters,
  managerFn:       Seq[TLManagerPortParameters] => TLManagerPortParameters,
  numClientPorts:  Range.Inclusive = 1 to 999,
  numManagerPorts: Range.Inclusive = 1 to 999)
  extends NexusNode(TLImp)(clientFn, managerFn, numClientPorts, numManagerPorts)
~~~

### case class TLOutputNode extends [OutputNode](../../diplomacy/Nodes.md#class-outputnoded-u-eo-ei-b-data)
### case class TLInputNode extends [InputNode](../../diplomacy/Nodes.md#class-inputnoded-u-eo-ei-b-data)
### case class TLBlindOutputNode extends [BlindOutputNode](../../diplomacy/Nodes.md#class-blindoutputnoded-u-eo-ei-b-data)
### case class TLBlindInputNode extends [BlindInputNode](../../diplomacy/Nodes.md#class-blindinputnoded-u-eo-ei-b-data)
### case class TLInternalOutputNode extends [InternalOutputNode](../../diplomacy/Nodes.md#class-internaloutputnoded-u-eo-ei-b-data)
### case class TLInternalInputNode extends [InternalOutputNode](../../diplomacy/Nodes.md#class-internalinputnoded-u-eo-ei-b-data)

object TLAsyncImp
------------
*Asynch TileLink module generator.*

~~~scala
object TLAsyncImp
    extends NodeImp[
        TLAsyncClientPortParameters,  // D
        TLAsyncManagerPortParameters, // U
        TLAsyncEdgeParameters,        // EO
        TLAsyncEdgeParameters,        // EI
        TLAsyncBundle                 // B
        ]
~~~

### Implementation of abstract methods defined in [`abstract class NodeImp`](../../diplomacy/Nodes.md).

+ **edgeO** `(TLAsyncClientPortParameters, TLAsyncManagerPortParameters) => TLAsyncEdgeParameters`
+ **edgeI** `(TLAsyncClientPortParameters, TLAsyncManagerPortParameters) => TLAsyncEdgeParameters`
+ **bundleO** `(TLAsyncEdgeParameters) => TLAsyncBundle`
+ **bundleI** `(TLAsyncEdgeParameters) => TLAsyncBundle`
+ **colour** `_ => "#ff0000"` red


### Asynchronous TileLink Extension of basic Nodes

+ **case class TLAsyncIdentityNode extends IdentityNode(TLAsyncImp)**
+ **case class TLAsyncOutputNode extends OutputNode(TLAsyncImp)**
+ **case class TLAsyncInputNode extends InputNode(TLAsyncImp)**
+ **case class TLAsyncSourceNode extends MixedAdapterNode(TLImp, TLAsyncImp)**
+ **case class TLAsyncSinkNode extends MixedAdapterNode(TLAsyncImp, TLImp)**

object TLRationalImp
------------
*Rational TileLink module generator*

~~~scala
object TLRationalImp
    extends NodeImp[
        TLRationalClientPortParameters,  // D
        TLRationalManagerPortParameters, // U
        TLRationalEdgeParameters,        // EO
        TLRationalEdgeParameters,        // EI
        TLRationalBundle                 // B
        ]
~~~

### Implementation of abstract methods defined in [`abstract class NodeImp`](../../diplomacy/Nodes.md).

+ **edgeO** `(TLRationalClientPortParameters, TLRationalManagerPortParameters) => TLRationalEdgeParameters`
+ **edgeI** `(TLRationalClientPortParameters, TLRationalManagerPortParameters) => TLRationalEdgeParameters`
+ **bundleO** `(TLRationalEdgeParameters) => TLRationalBundle`
+ **bundleI** `(TLRationalEdgeParameters) => TLRationalBundle`
+ **colour** `_ => "#00ff00"` green

### Rational TileLink Extension of basic Nodes

+ **case class TLRationalIdentityNode extends IdentityNode(TLRationalImp)**
+ **case class TLRationalOutputNode extends OutputNode(TLRationalImp)**
+ **case class TLRationalInputNode extends InputNode(TLRationalImp)**
+ **case class TLRationalSourceNode extends MixedAdapterNode(TLImp, TLRationalImp)**
+ **case class TLRationalSinkNode extends MixedAdapterNode(TLRationalImp, TLImp)**


<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 21/04/2017</sub></p>
