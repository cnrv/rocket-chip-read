[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[Edges](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/Edges.scala)
=====================
*Definitions for the TileLink packets.*
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
+ **staticHasData** `(TLChannel) => Option[Boolean]`<br>
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
+ Helper functions to get transaction fields

  **opcode**, **param**, **size**, **data**, and **source**<br>
  `(TLDataChannel) => UInt`<br>

  **mask**, **full_mask**, and **address**<br>
  `(TLAddrChannel) => UInt`<br>

  **addr_hi** `(UInt) => UInt` or `(TLAddrChannel) => UInt`<br>
  MSBs of an address (to a beat).
+ **addr_lo** `(UInt) => UInt` or `(TLAddrChannel) => UInt`<br>
  LSBs of an address (inside a beat).
+ **numBeats** `(TLChannel) => UInt`<br>
  Number of beats of this transaction.
+ **numBeats1** `(TLChannel) => UInt`<br>
  Number of beats - 1. (AXI style)

+ Helpers for counting beats

  **firstlastHelper** `(TLChannel, fire:Bool) => (first:Bool, last:Bool, done: Bool, count:UInt)`<br>
  **first**, **last** and **done**<br>
  `(TLChannel, fire:Bool) => Bool`<br>
  `(DecoupledIO[TLChannel]) => Bool`<br>
  `(ValidIO[TLChannel]) => Bool`<br>
  **firstlast**<br>
  `(TLChannel, fire:Bool) => (first:Bool, last:Bool, done: Bool)`<br>
  `(DecoupledIO[TLChannel]) => (first:Bool, last:Bool, done: Bool)`<br>
  `(ValidIO[TLChannel]) => (first:Bool, last:Bool, done: Bool)`<br>
  **count**<br>
  `(TLChannel, fire:Bool) => (first:Bool, last:Bool, done: Bool, count:UInt)`<br>
  `(DecoupledIO[TLChannel]) => (first:Bool, last:Bool, done: Bool, count:UInt)`<br>
  `(ValidIO[TLChannel]) => (first:Bool, last:Bool, done: Bool, count:UInt)`<br>
  **addr_inc**<br>
  `(TLChannel, fire:Bool) => (first:Bool, last:Bool, done: Bool, addr:UInt)`<br>
  `(DecoupledIO[TLChannel]) => (first:Bool, last:Bool, done: Bool, addr:UInt)`<br>
  `(ValidIO[TLChannel]) => (first:Bool, last:Bool, done: Bool, addr:UInt)`<br>
  The return value `addr` is the address inside a burst (`addr = count << log2Ceil(beatBytes)`)

class TLEdgeOut
---------------------
*Packet generator for downwards channels (A/C/E).*

~~~scala
class TLEdgeOut(
  client:  TLClientPortParameters,
  manager: TLManagerPortParameters)
  extends TLEdge(client, manager)
~~~

Arguments:

| name       |  type  |  description                    |
| :--        | :--:   | :--                             |
| fromSrc    | UInt   | source identifier               |
| toAddr     | UInt   | target address                  |
| lgSize     | UInt   | transaction size in log2 bytes  |
| growPerm   | UInt   | parameter for Acquire           |
| shrinkPerm | UInt   | parameter for Release           |
| reportPerm | UInt   | parameter for ProbeAck          |
| param      | UInt   | parameter for Hint              |
| data       | UInt   | payload                         |
| mask       | UInt   | write byte mask                 |
| atomic     | UInt   | type of atomic packets          |
| error      | Bool   | error acknowledgement           |

Return value:

| name       |  type     |  description                                                  |
| :--        | :--:      | :--                                                           |
| legal      | Boolean   | transaction type is supported and the target address is legal |
| packetA    | TLBundleA | generated packet for channel A                                |
| packetC    | TLBundleC | generated packet for channel C                                |
| packetE    | TLBundleE | generated packet for channel E                                |

+ Packet generators for channel A

  **Acquire** `(fromSrc, toAddr, lgSize, growPerm) => (legal, packetA)`<br>
  **Get** `(fromSrc, toAddr, lgSize) => (legal, packetA)`<br>
  **Put** `(fromSrc, toAddr, lgSize, data) => (legal, packetA)`<br>
  **Put** `(fromSrc, toAddr, lgSize, data, mask) => (legal, packetA)`<br>
  **Arithmetic** `(fromSrc, toAddr, lgSize, data, atomic) => (legal, packetA)`<br>
  **Logical** `(fromSrc, toAddr, lgSize, data, atomic) => (legal, packetA)`<br>
  **Hint** `(fromSrc, toAddr, lgSize, param) => (legal, packetA)`

+ Packet generators for channel C

  **Release**<br>
  `(fromSrc, toAddr, lgSize, shrinkPerm) => (legal, packetC)`<br>
  `(fromSrc, toAddr, lgSize, shrinkPerm, data) => (legal, packetC)`<br>
  **ProbeAck**<br>
  `(b: TLBundleB, reportPerm) => packetC`<br>
  `(b: TLBundleB, reportPerm, data: UInt) => packetC`<br>
  `(fromSrc, toAddr, lgSize, reportPerm) => packetC`<br>
  `(fromSrc, toAddr, lgSize, reportPerm, data) => packetC`<br>
  **AccessAck**<br>
  `(b: TLBundleB) => packetC`<br>
  `(b: TLBundleB, data: UInt) => packetC`<br>
  `(b: TLBundleB, error: Bool) => packetC`<br>
  `(b: TLBundleB, data, error) => packetC`<br>
  `(fromSrc, toAddr, lgSize) => packetC`<br>
  `(fromSrc, toAddr, lgSize, data) => packetC`<br>
  `(fromSrc, toAddr, lgSize, error) => packetC`<br>
  `(fromSrc, toAddr, lgSize, data, error) => packetC`<br>
  **HintAck** `(b: TLBundleB) => packetC`<br>
  **HintAck** `(fromSrc, toAddr, lgSize) => packetC`

+ Packet generators for Channel E

  **GrantAck** `(b: TLBundleD) => packetE`<br>
  **GrantAck** `(toSink: UInt) => packetE`<br>

class TLEdgeIn
---------------------
*Packet generator for upwards channels (B/D).*

~~~scala
class TLEdgeIn(
  client:  TLClientPortParameters,
  manager: TLManagerPortParameters)
  extends TLEdge(client, manager)
~~~

Arguments:

| name       |  type  |  description                    |
| :--        | :--:   | :--                             |
| fromAddr   | UInt   | source address                  |
| fromSink   | UInt   | sink identifier                 |
| toSrc      | UInt   | target identifier               |
| lgSize     | UInt   | transaction size in log2 bytes  |
| capPerm    | UInt   | parameter for Probe/Grant       |
| param      | UInt   | parameter for Hint              |
| data       | UInt   | payload                         |
| mask       | UInt   | write byte mask                 |
| atomic     | UInt   | type of atomic packets          |
| error      | Bool   | error acknowledgement           |

Return value:

| name       |  type     |  description                                                  |
| :--        | :--:      | :--                                                           |
| legal      | Boolean   | transaction type is supported and the target address is legal |
| packetB    | TLBundleB | generated packet for channel B                                |
| packetD    | TLBundleD | generated packet for channel D                                |

+ Packet generators for channel B

  **Probe** `(fromAddr, toSrc, lgSize, capPerm) => (legal, packetB)`<br>
  **Get** `(fromAddr, toSrc, lgSize) => (legal, packetB)`<br>
  **Put** `(fromAddr, toSrc, lgSize, data) => (legal, packetB)`<br>
  **Put** `(fromAddr, toSrc, lgSize, data, mask) => (legal, packetB)`<br>
  **Arithmetic** `(fromAddr, toSrc, lgSize, data, atomic) => (legal, packetB)`<br>
  **Logical** `(fromAddr, toSrc, lgSize, data, atomic) => (legal, packetB)`<br>
  **Hint** `(fromAddr, toSrc, lgSize, param) => (legal, packetB)`

+ Packet generators for channel D

  **Grant**<br>
  `(fromSink, toSrc, lgSize, capPerm) => packetD`<br>
  `(fromSink, toSrc, lgSize, capPerm, error) => packetD`<br>
  `(fromSink, toSrc, lgSize, capPerm, data) => packetD`<br>
  `(fromSink, toSrc, lgSize, capPerm, data, error) => packetD`

  **ReleaseAck**<br>
  `(c: TLBundleC) => packetD`<br>
  `(toSrc, lgSize) => packetD`

  **AccessAck**<br>
  `(a: TLBundleA) => packetD`<br>
  `(a: TLBundleA, data) => packetD`<br>
  `(a: TLBundleA, error) => packetD`<br>
  `(a: TLBundleA, data, error) => packetD`<br>
  `(toSrc, lgSize) => packetD`<br>
  `(toSrc, lgSize, data) => packetD`<br>
  `(toSrc, lgSize, error) => packetD`<br>
  `(toSrc, lgSize, data, error) => packetD`

  **HintAck** `(a:TLBundleA) => packetD`<br>
  **HintAck** `(toSrc, lgSize) => packetD`


<br><br><br><p align="right">
<sub>
Last updated: 07/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
