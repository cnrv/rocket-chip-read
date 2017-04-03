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

+ **isAligned** `(address: UInt, lgSize: UInt) => Bool`<br>
  Whether `address` is aligned to `1 << lgSize`.
+ **mask** `(address: UInt, lgSize: UInt) => UInt`<br>
  Generate mask for a TileLink transaction.
+ **statucHasData** `(TLChannel) => Option[Boolean]`<br>
  Compile time analysis, return whether data is needed for a channel.<br>
  Yes: `Some(true)`;<br>
  No:  `Some(false)`;<br>
  Unknown: `None`.
+ **isRequest** `(TLChannel) => Bool`<br>
  Whether the transaction is a request (Put, AMO, Get, Hint, Acquire, Probe, Release or Grant).
+ **isResponse** `(TLChannel) => Bool`<br>
  Whether the transaction is a response (AccessAck, ProbeAck, HintAck, Grant, ReleaseAck, GrantAck).
+ **hasData** `(TLChannel) => Bool`<br>
  Whether the transaction has data. See the "[type of TileLink transactions](Bundles.md#type-of-tilelink-transactions)."
+ Helper functions to get transaction fields<br>
  **opcode** `(TLDataChannel) => Bool`<br>
  **param** `(TLDataChannel) => UInt`<br>
  **size** `(TLDataChannel) => UInt`<br>
  **data** `(TLDataChannel) => UInt`<br>
  **mask** `(TLDataChannel) => UInt`<br>
  **full_mask** `(TLDataChannel) => UInt`<br>
  **address** `(TLDataChannel) => UInt`<br>
  **source** `(TLDataChannel) => UInt`<br>
+ **addr_hi** `(UInt) => UInt` or `(TLAddrChannel) => UInt`<br>
  MSBs of an address (to a beat).
+ **addr_lo** `(UInt) => UInt` or `(TLDataChannel) => UInt`<br>
  LSBs of an address (inside a beat).
+ **numBeats** `(TLChannel) => UInt`<br>
  Number of beats of this transaction.
+ **numBeats1** `(TLChannel) => UInt`<br>
  Number of beats - 1. (AXI style)







**********************

```scala
last_modified = 03/04/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```

