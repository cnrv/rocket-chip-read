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

+ **mask** `(address: UInt, lgSize: UInt) => UInt`

    Generate mask for a TileLink transaction.

+ **statucHasData** `(TLChannel) => Option[Boolean]`

    Compile time analysis, return whether data is needed for a channel.
    + Yes: `Some(true)`;
    + No:  `Some(false)`;
    + Unknown: `None`.

+ **isRequest** `(TLChannel) => Bool`

    Whether the transaction is a request (Put, AMO, Get, Hint, Acquire, Probe, Release or Grant).

+ **isResponse** `(TLChannel) => Bool`

    Whether the transaction is a response (AccessAck, ProbeAck, HintAck, Grant, ReleaseAck, GrantAck).

+ **hasData** `(TLChannel) => Bool`

    Whether the transaction has data. See the "[type of TileLink transactions](Bundles.md#type-of-tilelink-transactions)."

+ Helper functions to get transaction fields
  + **opcode** `(TLDataChannel) => Bool`
  + **param** `(TLDataChannel) => UInt`
  + **size** `(TLDataChannel) => UInt`
  + **data** `(TLDataChannel) => UInt`
  + **mask** `(TLDataChannel) => UInt`
  + **full_mask** `(TLDataChannel) => UInt`
  + **address** `(TLDataChannel) => UInt`
  + **source** `(TLDataChannel) => UInt`








**********************

```scala
last_modified = 02/04/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```

