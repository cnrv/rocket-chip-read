[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[Parameters](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/Parameters.scala)
=====================

*TileLink interconnection parameters.*

**********************

### TL

Base TileLink connection.

### TLAsync

Asynchronous TileLink connection, cross asynchronous clock domains.

### TLRational

Mesochronous TileLink connection, cross source shared clock domains.


**********************

case class TLManagerParameters
------------
*Parameters for a TileLink manager.*

~~~scala
case class TLManagerParameters(
  address:            Seq[AddressSet],
  resources:          Seq[Resource] = Seq(),
  regionType:         RegionType.T  = RegionType.GET_EFFECTS,
  executable:         Boolean       = false, // processor can execute from this memory
  nodePath:           Seq[BaseNode] = Seq(),
  supportsAcquireT:   TransferSizes = TransferSizes.none,
  supportsAcquireB:   TransferSizes = TransferSizes.none,
  supportsArithmetic: TransferSizes = TransferSizes.none,
  supportsLogical:    TransferSizes = TransferSizes.none,
  supportsGet:        TransferSizes = TransferSizes.none,
  supportsPutFull:    TransferSizes = TransferSizes.none,
  supportsPutPartial: TransferSizes = TransferSizes.none,
  supportsHint:       TransferSizes = TransferSizes.none,
  fifoId:             Option[Int]   = None)
~~~

### Case variables:

+ **address**            `Seq[AddressSet]`

    Address range covered by this manager.

+ **resources**          `Seq[Resource] = Seq()`
+ **regionType**         `RegionType.T = RegionType.GET_EFFECTS`
+ **executable**         `Boolean = false`
+ **nodePath**           `Seq[BaseNode] = Seq()`
+ The supported types and sizes of packets
  + **supportsAcquireT**   `TransferSizes = TransferSizes.none`
  + **supportsAcquireB**   `TransferSizes = TransferSizes.none`
  + **supportsArithmetic** `TransferSizes = TransferSizes.none`
  + **supportsLogical**    `TransferSizes = TransferSizes.none`
  + **supportsGet**        `TransferSizes = TransferSizes.none`
  + **supportsPutFull**    `TransferSizes = TransferSizes.none`
  + **supportsPutPartial** `TransferSizes = TransferSizes.none`
  + **supportsHint**       `TransferSizes = TransferSizes.none`
+ **fifoId**             `Option[Int] = None`<br>
  If fifoId=Some, all accesses sent to the same fifoId are executed and ACK'd in FIFO order.<br>
  Note: you can only rely on this FIFO behaviour if your TLClientParameters include requestFifo.

### Member variables and functions:

+ **maxTransfer** `TransferSizes`

    The maximal packet size.

+ **maxAddress** `BigInt`

    The maximal address in all address spaces.

+ **name** `String`
+ **minAlignment** `BigInt`

    The minimal alignment of all address spaces.

+ **toResource** `_ => ResourceAddress`

    Convert this to `ResourceAddress`.

case class TLManagerPortParameters
--------------
*Parameters for a TileLink manager (upwards) port.*

~~~scala
case class TLManagerPortParameters(
  managers:   Seq[TLManagerParameters],
  beatBytes:  Int,
  endSinkId:  Int = 1,
  minLatency: Int = 0)
~~~

### Case variables:

+ **managers** `Seq[TLManagerParameters]`

    Parameters of the managers sharing this port.

+ **beatBytes** `Int`

    Number of bytes per beat.

+ **endSinkId** `Int = 1`
+ **minLatency** `Int = 0`

### Member variables and functions:

+ **maxTransfer** `_ => Int`

    The maximal packet size.

+ **maxAddress** `_ => BigInt`

    The maximal address in all address spaces.

+ Get the size of supported packets (the maximal size range supported by all managers)
  + **allSupportAcquireT**   `_ => TransferSizes`
  + **allSupportAcquireB**   `_ => TransferSizes`
  + **allSupportArithmetic** `_ => TransferSizes`
  + **allSupportLogical**    `_ => TransferSizes`
  + **allSupportGet**        `_ => TransferSizes`
  + **allSupportPutFull**    `_ => TransferSizes`
  + **allSupportPutPartial** `_ => TransferSizes`
  + **allSupportHint**       `_ => TransferSizes`

+ Get the supported types of packets (supported by any manager)
  + **anySupportAcquireT**   `_ => Boolean`
  + **anySupportAcquireB**   `_ => Boolean`
  + **anySupportArithmetic** `_ => Boolean`
  + **anySupportLogical**    `_ => Boolean`
  + **anySupportGet**        `_ => Boolean`
  + **anySupportPutFull**    `_ => Boolean`
  + **anySupportPutPartial** `_ => Boolean`
  + **anySupportHint**       `_ => Boolean`

+ Check whether an address is managed by this port with a certain type and size
  + **supportsAcquireTSafe**   `(address: UInt, lgSize: UInt) => Bool`
  + **supportsAcquireBSafe**   `(address: UInt, lgSize: UInt) => Bool`
  + **supportsArithmeticSafe** `(address: UInt, lgSize: UInt) => Bool`
  + **supportsLogicalSafe**    `(address: UInt, lgSize: UInt) => Bool`
  + **supportsGetSafe**        `(address: UInt, lgSize: UInt) => Bool`
  + **supportsPutFullSafe**    `(address: UInt, lgSize: UInt) => Bool`
  + **supportsPutPartialSafe** `(address: UInt, lgSize: UInt) => Bool`
  + **supportsHintSafe**       `(address: UInt, lgSize: UInt) => Bool`

+ Check whether an address is managed by this port with a certain type and size (fast version by assuming the address is valid)
  + **supportsAcquireTFast**   `(address: UInt, lgSize: UInt) => Bool`
  + **supportsAcquireBFast**   `(address: UInt, lgSize: UInt) => Bool`
  + **supportsArithmeticFast** `(address: UInt, lgSize: UInt) => Bool`
  + **supportsLogicalFast**    `(address: UInt, lgSize: UInt) => Bool`
  + **supportsGetFast**        `(address: UInt, lgSize: UInt) => Bool`
  + **supportsPutFullFast**    `(address: UInt, lgSize: UInt) => Bool`
  + **supportsPutPartialFast** `(address: UInt, lgSize: UInt) => Bool`
  + **supportsHintFast**       `(address: UInt, lgSize: UInt) => Bool`

+ **routingMask** `BigInt`

    Which bits suffice to distinguish between all managers.

+ **find** `(address: BigInt) => Option[TLManagerParameters]`

    Get the `TLManagerParameters` of an address.

+ **findSafe** `(address: UInt) => Vec()`

    Return a bit vector that identifies the managers containing this address.

+ **containsSafe** `(address: UInt) => Bool`

    Whether this address is managed by this port.

+ **findFast** `(address: UInt) => Vec()`

    A faster version of `findSafe()` by assuming the address is valid.

+ **findFifoIdFast** `(address: UInt) => Int`

    Get the `fifoId + 1` or 0 if none.

+ **hasFifoIdFast** `(address: UInt) => Boolean`

    Whether there is a matched `fifoId`.


case class TLClientParameters
--------------
*Parameters for a TileLink client.*

~~~scala
case class TLClientParameters(
  sourceId:            IdRange       = IdRange(0,1),
  nodePath:            Seq[BaseNode] = Seq(),
  supportsProbe:       TransferSizes = TransferSizes.none,
  supportsArithmetic:  TransferSizes = TransferSizes.none,
  supportsLogical:     TransferSizes = TransferSizes.none,
  supportsGet:         TransferSizes = TransferSizes.none,
  supportsPutFull:     TransferSizes = TransferSizes.none,
  supportsPutPartial:  TransferSizes = TransferSizes.none,
  supportsHint:        TransferSizes = TransferSizes.none)
~~~

### Case variables:

+ **sourceId** `IdRange = IdRange(0,1)`

    Source ID range used for routing responses.

+ **nodePath** `Seq[BaseNode] = Seq()`
+ The supported types and sizes of packets
  + **supportsProbe**       `TransferSizes = TransferSizes.none`
  + **supportsArithmetic**  `TransferSizes = TransferSizes.none`
  + **supportsLogical**     `TransferSizes = TransferSizes.none`
  + **supportsGet**         `TransferSizes = TransferSizes.none`
  + **supportsPutFull**     `TransferSizes = TransferSizes.none`
  + **supportsPutPartial**  `TransferSizes = TransferSizes.none`
  + **supportsHint**        `TransferSizes = TransferSizes.none`

### Member variables and functions:

+ **maxTransfer** `TransferSizes`

    The maximal packet size.

+ **name** `String`

case class TLClientPortParameters
-----------------------
*Parameters for a TileLink client (downwards) port.*

~~~scala
case class TLClientPortParameters(
  clients:       Seq[TLClientParameters],
  unsafeAtomics: Boolean = false,
  minLatency:    Int = 0) // Atomics are executed as get+put
~~~

### Case variables:

+ **clients** `Seq[TLClientParameters]`

    Parameters of the clients sharing this port.

+ **unsafeAtomics** `Boolean = false`
+ **minLatency** `Int = 0`


### Member variables and functions:

+ **endSourceId** `_ => Int`

    The maximal source ID.

+ **maxTransfer** `_ => Int`

    The maximal packet size.

+ Get the size of supported packets (the maximal size range supported by all clients)
  + **allSupportProbe**      `_ => TransferSizes`
  + **allSupportArithmetic** `_ => TransferSizes`
  + **allSupportLogical**    `_ => TransferSizes`
  + **allSupportGet**        `_ => TransferSizes`
  + **allSupportPutFull**    `_ => TransferSizes`
  + **allSupportPutPartial** `_ => TransferSizes`
  + **allSupportHint**       `_ => TransferSizes`

+ Get the supported types of packets (supported by any client)
  + **anySupportProbe**      `_ => Boolean`
  + **anySupportArithmetic** `_ => Boolean`
  + **anySupportLogical**    `_ => Boolean`
  + **anySupportGet**        `_ => Boolean`
  + **anySupportPutFull**    `_ => Boolean`
  + **anySupportPutPartial** `_ => Boolean`
  + **anySupportHint**       `_ => Boolean`

+ Check for support of a given operation at a specific id
  + **supportsProbe**      `(id: UInt, lgSize: UInt) => Bool`
  + **supportsArithmetic** `(id: UInt, lgSize: UInt) => Bool`
  + **supportsLogical**    `(id: UInt, lgSize: UInt) => Bool`
  + **supportsGet**        `(id: UInt, lgSize: UInt) => Bool`
  + **supportsPutFull**    `(id: UInt, lgSize: UInt) => Bool`
  + **supportsPutPartial** `(id: UInt, lgSize: UInt) => Bool`
  + **supportsHint**       `(id: UInt, lgSize: UInt) => Bool`


+ **find** `(id: Int) => Option[TLClientParameters]`

    Get the `TLClientParameters` of an ID.

+ **find** `(id: UInt) => Vec()`

    Return a bit vector that identifies the clients.

+ **contains** `(id: UInt) => Bool`

    Whether this ID belongs to this port.

case class TLBundleParameters
------------------
*Parameters for a TileLink IO interface (Bundle).*

~~~scala
case class TLBundleParameters(
  addressBits: Int,
  dataBits:    Int,
  sourceBits:  Int,
  sinkBits:    Int,
  sizeBits:    Int)
~~~

### Case variables:

+ **addressBits** `Int`

    Size of address.

+ **dataBits**    `Int`

    Size of data.

+ **sourceBits**  `Int`

    Size of source ID.

+ **sinkBits**    `Int`

    Size of sink ID?

+ **sizeBits**    `Int`

    Size of size field.

### Member variables and functions:

+ **addrLoBits** `Int`

    Size of beat offset bits.

+ **union** `(x: TLBundleParameters) => TLBundleParameters`

    Return a parameter object that fits both `this` and `x`.

object TLBundleParameters
-------------------

+ **emptyBundleParams** `TLBundleParameters(1,8,1,1,1)`

    The default (empty) bundle parameter object.

+ **union** `(Seq[TLBundleParameters]) => TLBundleParameters`

    Get a parameter that fits all individual parameter objects.

+ **apply** `(TLClientPortParameters, TLManagerPortParameters) => TLBundleParameters`

    Generate a bundle parameter according to port parameters.

case class TLEdgeParameters
-------------
*Parameters for a TileLink connection.*

~~~scala
case class TLEdgeParameters(
  client:  TLClientPortParameters,
  manager: TLManagerPortParameters)
~~~

### Case variables:

+ **client** `TLClientPortParameters`

    Client side parameters.

+ **manager** `TLManagerPortParameters`

    Manager side parameters.

### Member variables and functions:

+ **maxTransfer** `Int`

    The maximal transfer size in both client/manager sides.

+ **maxLgSize** `log2Ceil(maxTransfer)`
+ **bundle** `TLBundleParameters(client, manager)`

case class TLAsyncManagerPortParameters
------------------
*Async TileLink (cross clock-domain) manager port parameters.*

~~~scala
case class TLAsyncManagerPortParameters(
    depth: Int, base: TLManagerPortParameters)
~~~

case class TLAsyncClientPortParameters
------------------
*Async TileLink (cross clock-domain) client port parameters.*

~~~scala
case class TLAsyncClientPortParameters(base: TLClientPortParameters)
~~~

case class TLAsyncBundleParameters
-----------------
*Async TileLink (cross clock-domain) interface IO parameters.*

~~~scala
case class TLAsyncBundleParameters(depth: Int, base: TLBundleParameters)
~~~

+ **union** `(x: TLAsyncBundleParameters) => TLAsyncBundleParameters`

    Get a parameter that fits both `this` and `x`.

object TLAsyncBundleParameters
----------

+ **emptyBundleParams** `TLAsyncBundleParameters(1, TLBundleParameters.emptyBundleParams)`

    The default (empty) bundle parameter object.

+ **union** `(Seq[TLAsyncBundleParameters]) => TLAsyncBundleParameters`

    Get a parameter that fits all individual parameter objects.


case class TLAsyncEdgeParameters
------------
*Parameters for an asynchronous TileLink connection.*

~~~scala
case class TLAsyncEdgeParameters(
    client: TLAsyncClientPortParameters, manager: TLAsyncManagerPortParameters)
~~~

+ **bundle** `TLAsyncBundleParameters(manager.depth, TLBundleParameters(client.base, manager.base))`

### Case variables:

+ **client** `TLAsyncClientPortParameters`

    Client side parameters.

+ **manager** `TLAsyncManagerPortParameters`

    Manager side parameters.

### Member variables and functions:

+ **bundle** `TLAsyncBundleParameters(client, manager)`

case class TLRationalManagerPortParameters
---------------
*Rational TileLink (cross clock-domain) manager port parameters.*

~~~scala
case class TLRationalManagerPortParameters(
    direction: RationalDirection, base: TLManagerPortParameters)
~~~

+ **direction** `RationalDirection`

    The relation between two source synchronised clocks:
    + `Symmetric` Nor sure which side is slower so put queues on both sides.
    + `FastToSlow` Register at the slow sink.
    + `SlowToFast` Register at the slow source.

case class TLRationalClientPortParameters
-------------
*Rational TileLink (cross clock-domain) client port parameters.*

~~~scala
case class TLRationalClientPortParameters(base: TLClientPortParameters)
~~~

case class TLRationalEdgeParameters
-------------
*Parameters for a rational TileLink connection.*

~~~scala
case class TLRationalEdgeParameters(
    client: TLRationalClientPortParameters, manager: TLRationalManagerPortParameters)
~~~

+ **bundle** `TLBundleParameters(client.base, manager.base)`

object ManagerUnification
----------------

+ **apply** `(Seq[TLManagerParameters]) => Seq[TLManagerParameters]`

    Merge `TLManagerParameters` that have the same key (transaction types). Key is defined as
~~~scala
case class TLManagerKey(
    regionType:         RegionType.T,
    executable:         Boolean,
    lastNode:           BaseNode,
    supportsAcquireT:   TransferSizes,
    supportsAcquireB:   TransferSizes,
    supportsArithmetic: TransferSizes,
    supportsLogical:    TransferSizes,
    supportsGet:        TransferSizes,
    supportsPutFull:    TransferSizes,
    supportsPutPartial: TransferSizes,
    supportsHint:       TransferSizes)
~~~


<br><br><br><p align="right">
<sub>
Last updated: 18/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
