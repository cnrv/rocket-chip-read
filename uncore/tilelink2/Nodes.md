[Rocket](../../Readme.md)/[uncore](../../uncore.md)/[tilelink2](../tilelink2.md)/[Nodes](https://github.com/ucb-bar/rocket-chip/blob/master/src/main/scala/uncore/tilelink2/Nodes.scala)
=====================


**********************

object TLImp
---------------
*General TileLink module generator object.*

~~~scala
object TLImp
    extends NodeImp[TLClientPortParameters, TLManagerPortParameters,
                    TLEdgeOut, TLEdgeIn, TLBundle]
~~~

### Implementation of abstract methods defined in [`abstract class NodeImp`](../../diplomacy/Nodes.md).

+ **edgeO** `(TLClientPortParameters, TLManagerPortParameters) => TLEdgeOut`

    Get parameters for the TileLink output channel.

+ **edgeI** `(TLClientPortParameters, TLManagerPortParameters) => TLEdgeIn`

    Get parameters for the TileLink input channel.

+ **bundleO** `(TLEdgeOut) => TLBundle`

    Generate the output channel bundle.

+ **bundleI** `(TLEdgeIn) => TLBundle`

    Generate the input channel bundle.

+ **colour** `_ => "#000000"` black

+ **connect** `(() => Seq[(TLEdgeIn, TLBundle, TLBundle)]) => (Option[LazyModule], () => Unit)`

    Callback to set the bus monitor and port connections.
    Depending on parameter [`TLMonitorBuilder`](../../rocketchip/Configs.md), `Option[LazyModule]` is a `TLMonitor`.

case class TLIdentityNode
--------------

~~~scala
case class TLIdentityNode() extends IdentityNode(TLImp)
~~~

case class TLClientNode
------------

~~~scala
case class TLClientNode(portParams: Seq[TLClientPortParameters])
    extends SourceNode(TLImp)(portParams)
~~~

case class TLManagerNode
-------------

~~~scala
case class TLManagerNode(portParams: Seq[TLManagerPortParameters])
    extends SinkNode(TLImp)(portParams)
~~~

**********************

```scala
last_modified = 28/03/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
