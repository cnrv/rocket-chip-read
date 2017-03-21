[Rocket](../../Readme.md)/[uncore](../../uncore.md)/[tilelink2](../tilelink2.md)/[Parameters](https://github.com/ucb-bar/rocket-chip/blob/master/src/main/scala/uncore/tilelink2/Parameters.scala)
=====================



**********************


case class TLManagerParameters
------------
*Parameters for a TileLink2 manager.*

Case variables:

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
+ **fifoId**             `Option[Int] = None`

Member variables and functions:

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

Case variables:

+ **managers** `Seq[TLManagerParameters]`

    Parameters of the managers sharing this port.

+ **beatBytes** `Int`

    Number of bytes per beat.

+ **endSinkId** `Int = 1`
+ **minLatency** `Int = 0`

Member variables and functions:

+ **maxTransfer** `_ => TransferSizes`

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

Case variables:

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

Member variables and functions:

+ **maxTransfer** `TransferSizes`

    The maximal packet size.

+ **name** `String`

case class TLClientPortParameters
-----------------------
*Parameters for a TileLink client (downwards) port.*

Case variables:

+ **clients** `Seq[TLClientParameters]`

    Parameters of the clients sharing this port.

+ **unsafeAtomics** `Boolean = false`
+ **minLatency** `Int = 0`


Member variables and functions:

+ **endSourceId** `_ => Int`

    The maximal source ID.

+ **maxTransfer** `_ => TransferSizes`

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

**********************

```scala
last_modified = 21/03/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
