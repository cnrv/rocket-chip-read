[Rocket](../../Readme.md)/[uncore](../../uncore.md)/[tilelink2](../tilelink2.md)/[Edges](https://github.com/ucb-bar/rocket-chip/blob/master/src/main/scala/uncore/tilelink2/Edges.scala)
=====================

**********************

class TLEdge
--------------
*Base class of TileLink edges.*

~~~scala
class TLEdge(
  client:  TLClientPortParameters,
  manager: TLManagerPortParameters)
  extends TLEdgeParameters(client, manager)
~~~

+ **isAligned** `(address: UInt, lgSize: UInt) => Bool`

    Whether `address` is aligned to `1 << lgSize`.






**********************

```scala
last_modified = 29/03/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```

