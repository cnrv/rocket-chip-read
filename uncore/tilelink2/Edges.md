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
+ Helpers for counting beats<br>
  **firstlastHelper** `(TLChannel, fire:Bool) => (first:Bool, last:Bool, done: Bool, count:UInt)`<br>
  **first** `(TLChannel, fire:Bool) => Bool`<br>
  **first** `(DecoupledIO[TLChannel]) => Bool`<br>
  **first** `(ValidIO[TLChannel]) => Bool`<br>
  **last** `(TLChannel, fire:Bool) => Bool`<br>
  **last** `(DecoupledIO[TLChannel]) => Bool`<br>
  **last** `(ValidIO[TLChannel]) => Bool`<br>
  **done** `(TLChannel, fire:Bool) => Bool`<br>
  **done** `(DecoupledIO[TLChannel]) => Bool`<br>
  **done** `(ValidIO[TLChannel]) => Bool`<br>
  **firstlast** `(TLChannel, fire:Bool) => (first:Bool, last:Bool, done: Bool)`<br>
  **firstlast** `(DecoupledIO[TLChannel]) => (first:Bool, last:Bool, done: Bool)`<br>
  **firstlast** `(ValidIO[TLChannel]) => (first:Bool, last:Bool, done: Bool)`<br>
  **count** `(TLChannel, fire:Bool) => (first:Bool, last:Bool, done: Bool, count:UInt)`<br>
  **count** `(DecoupledIO[TLChannel]) => (first:Bool, last:Bool, done: Bool, count:UInt)`<br>
  **count** `(ValidIO[TLChannel]) => (first:Bool, last:Bool, done: Bool, count:UInt)`<br>
  <br>For the following, `addr = count << log2Ceil(beatBytes)`, the addrress inside a burst.<br>
  **addr_inc** `(TLChannel, fire:Bool) => (first:Bool, last:Bool, done: Bool, addr:UInt)`<br>
  **addr_inc** `(DecoupledIO[TLChannel]) => (first:Bool, last:Bool, done: Bool, addr:UInt)`<br>
  **addr_inc** `(ValidIO[TLChannel]) => (first:Bool, last:Bool, done: Bool, addr:UInt)`<br>

class TLEdgeOut
---------------------
*Packet generator for downwards channels (A/C/E).*

~~~scala
class TLEdgeOut(
  client:  TLClientPortParameters,
  manager: TLManagerPortParameters)
  extends TLEdge(client, manager)
~~~

+ Arguments:<br>
  **fromSrc** `UInt` source identifier.<br>
  **toAddr** `UInt` target address.<br>
  **lgSize** `UInt` transaction size in `log2(Bytes)`.<br>
  **growPerm**, **shrinkPerm**, **reportPerm** and **param** `UInt` packet parameter.<br>
  **data**, `UInt` data.<br>
  **mask**, `UInt` write byte mask.<br>
  **atomic**, `UInt` type of atomic packets.
  **error**, `Bool` error acknowledgement.
+ Return value:<br>
  **legal** `Boolean` Transaction type is supported and the target address is legal.<br>
  **packet** `TLBundleA`, `TLBundleC` or `TLBundleE` the generated packet.
+ **TLBundleA**<br>
  **Acquire** `(fromSrc, toAddr, lgSize, growPerm) => (legal, packet)`<br>
  **Get** `(fromSrc, toAddr, lgSize) => (legal, packet)`<br>
  **Put** `(fromSrc, toAddr, lgSize, data) => (legal, packet)`<br>
  **Put** `(fromSrc, toAddr, lgSize, data, mask) => (legal, packet)`<br>
  **Arithmetic** `(fromSrc, toAddr, lgSize, data, atomic) => (legal, packet)`<br>
  **Logical** `(fromSrc, toAddr, lgSize, data, atomic) => (legal, packet)`<br>
  **Hint** `(fromSrc, toAddr, lgSize, param) => (legal, packet)`
+ **TLBundleC**
  + **Release**<br>
  `(fromSrc, toAddr, lgSize, shrinkPerm) => (legal, packet)`<br>
  `(fromSrc, toAddr, lgSize, shrinkPerm, data) => (legal, packet)`
  + **ProbeAck**<br>
  `(b: TLBundleB, reportPerm) => packet`<br>
  `(b: TLBundleB, reportPerm, data: UInt) => packet`<br>
  `(fromSrc, toAddr, lgSize, reportPerm) => packet`<br>
  `(fromSrc, toAddr, lgSize, reportPerm, data) => packet`
  + **AccessAck**<br>
  `(b: TLBundleB) => packet`<br>
  `(b: TLBundleB, data: UInt) => packet`<br>
  `(b: TLBundleB, error: Bool) => packet`<br>
  `(b: TLBundleB, data: UInt, error: Bool) => packet`<br>
  `(fromSrc, toAddr, lgSize) => packet`<br>
  `(fromSrc, toAddr, lgSize, data) => packet`<br>
  `(fromSrc, toAddr, lgSize, error) => packet`<br>
  `(fromSrc, toAddr, lgSize, data, error) => packet`
  + **HintAck**<br>
  `(b: TLBundleB) => TLBundleC`<br>
  `(fromSrc, toAddr, lgSize) => packet`
+ **TLBundleE**<br>
  **GrantAck** `(b: TLBundleD) => packet`<br>
  **GrantAck** `(toSink: UInt) => packet`<br>




**********************

```scala
last_modified = 04/04/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```

