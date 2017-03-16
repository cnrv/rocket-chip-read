[Rocket](../../Readme.md)/[uncore](../../uncore.md)/[tilelink2](../tilelink2.md)/[Parameters](https://github.com/ucb-bar/rocket-chip/blob/master/src/main/scala/uncore/tilelink2/Parameters.scala)
=====================



**********************


case class TLManagerParameters
------------
*Parameters for a TileLink2 manager.*

Case variables:

+ **address**            `Seq[AddressSet]`
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

+ **maxTransfer** `TransferSizes`

    The maximal packet size.

+ **maxAddress** `BigInt`

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

**********************

```scala
last_modified = 16/03/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
