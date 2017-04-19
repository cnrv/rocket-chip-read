[Rocket](../../Readme.md)/[uncore](../../uncore.md)/[tilelink2](../tilelink2.md)/[Nodes](https://github.com/ucb-bar/rocket-chip/blob/master/src/main/scala/uncore/tilelink2/Nodes.scala)
=====================

**********************

*TileLink Nodes*

* [Synchronous TileLink Nodes](#object-tlimp)
* [Asynchronous TileLink Nodes](#object-tlasyncimp)
* [Rational TileLink Nodes](#object-tlrationalimp)

**********************

object TLImp
---------------
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

### Implementation of abstract methods defined in [`abstract class NodeImp`](../../diplomacy/Nodes.md).

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

### TileLink Extension of basic Nodes

+ **case class TLIdentityNode extends IdentityNode(TLImp)**
+ **case class TLClientNode extends SourceNode(TLImp)**
+ **case class TLManagerNode extends SinkNode(TLImp)**
+ **case class TLAdapterNode extends AdapterNode(TLImp)**
+ **case class TLNexusNode extends NexusNode(TLImp)**

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


**********************

```scala
last_modified = 19/04/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
