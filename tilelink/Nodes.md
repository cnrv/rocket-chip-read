[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[Nodes](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/Nodes.scala)
=====================
*TileLink nodes.*

**********************

*TileLink Nodes*

* [Synchronous TileLink Nodes](#synchronous-tilelink-nodes)
* [Asynchronous TileLink Nodes](#asynchronous-tilelink-nodes)
* [Rational TileLink Nodes](#rational-tilelink-nodes)

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

#### Implementation of abstract methods defined in NodeImp

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
  _monitor_: The monitor to be connected. Depending on parameter TLMonitorBuilder
  _bind_: The actual port binding procedure to be processed later.

### TileLink extension of basic Nodes

+ case class **TLIdentityNode**       extends IdentityNode
+ case class **TLClientNode**         extends SourceNode
+ object     **TLClientNode**
+ case class **TLManagerNode**        extends SinkNode
+ object     **TLManagerNode**
+ case class **TLAdapterNode**        extends AdapterNode
+ case class **TLNexusNode**          extends NexusNode
+ case class **TLOutputNode**         extends OutputNode
+ case class **TLInputNode**          extends InputNode
+ case class **TLBlindOutputNode**    extends BlindOutputNode
+ case class **TLBlindInputNode**     extends BlindInputNode
+ case class **TLInternalOutputNode** extends InternalOutputNode
+ case class **TLInternalInputNode**  extends InternalOutputNode

Asynchronous TileLink Nodes
----------------

### object TLAsyncImp
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

### Implementation of abstract methods defined in NodeImp

+ **edgeO** `(TLAsyncClientPortParameters, TLAsyncManagerPortParameters) => TLAsyncEdgeParameters`
+ **edgeI** `(TLAsyncClientPortParameters, TLAsyncManagerPortParameters) => TLAsyncEdgeParameters`
+ **bundleO** `(TLAsyncEdgeParameters) => TLAsyncBundle`
+ **bundleI** `(TLAsyncEdgeParameters) => TLAsyncBundle`
+ **colour** `_ => "#ff0000"` red


### Asynchronous TileLink Extension of basic Nodes

+ case class **TLAsyncIdentityNode** extends IdentityNode
+ case class **TLAsyncOutputNode**   extends OutputNode
+ case class **TLAsyncInputNode**    extends InputNode
+ case class **TLAsyncSourceNode**   extends MixedAdapterNode
+ case class **TLAsyncSinkNode**     extends MixedAdapterNode

Rational TileLink Nodes
----------------

### object TLRationalImp
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

### Implementation of abstract methods defined in NodeImp

+ **edgeO** `(TLRationalClientPortParameters, TLRationalManagerPortParameters) => TLRationalEdgeParameters`
+ **edgeI** `(TLRationalClientPortParameters, TLRationalManagerPortParameters) => TLRationalEdgeParameters`
+ **bundleO** `(TLRationalEdgeParameters) => TLRationalBundle`
+ **bundleI** `(TLRationalEdgeParameters) => TLRationalBundle`
+ **colour** `_ => "#00ff00"` green

### Rational TileLink Extension of basic Nodes

+ case class **TLRationalIdentityNode** extends IdentityNode
+ case class **TLRationalOutputNode**   extends OutputNode
+ case class **TLRationalInputNode**    extends InputNode
+ case class **TLRationalSourceNode**   extends MixedAdapterNode
+ case class **TLRationalSinkNode**     extends MixedAdapterNode


<br><br><br><p align="right">
<sub>
Last updated: 21/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
