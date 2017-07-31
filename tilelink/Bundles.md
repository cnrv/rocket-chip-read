[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[Bundles](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/Bundles.scala)
=====================
*TileLink channel definitions.*

**********************


## object TLMessages
*Constants to define message types*

### Type of TileLink transactions

| Type            | ID | A | B | C | D | E | Data | Description                 | Response       |
| :---            |----|---|---|---|---|---| :--: |       :---:                 |     :---:      |
| PutFullData     | 0  | * | * |   |   |   |  *   | Write a block               | AccessAck      |
| PutPartialData  | 1  | * | * |   |   |   |  *   | Write a partial block       | AccessAck      |
| ArithmeticData  | 2  | * | * |   |   |   |  *   | Arithmetic atomic (AMO)     | AccessAckData  |
| LogicalData     | 3  | * | * |   |   |   |  *   | Logic AMO                   | AccessAckData  |
| Get             | 4  | * | * |   |   |   |      | Get a block                 | AccessAckData  |
| Hint            | 5  | * | * |   |   |   |      | Prefetch a block            | HintAck        |
| Acquire         | 6  | * |   |   |   |   |      | Coherent request            | Grant[Data]    |
| Probe           | 6  |   | * |   |   |   |      | Coherent enquiry            | ProbeAck[Data] |
| AccessAck       | 0  |   |   | * | * |   |      | Ack to Put(write)           |                |
| AccessAckData   | 1  |   |   | * | * |   |      | Ack to Get/AMO              |                |
| HintAck         | 2  |   |   | * | * |   |      | Ack to Hint                 |                |
| ProbeAck        | 4  |   |   | * |   |   |      | Ack to Probe without data   |                |
| ProbeAckData    | 5  |   |   | * |   |   |  *   | Ack to Probe with data      |                |
| Release         | 6  |   |   | * |   |   |      | Replace clean block         | ReleaseAck     |
| ReleaseData     | 7  |   |   | * |   |   |  *   | Writeback dirty block       | ReleaseAck     |
| Grant           | 4  |   |   |   | * |   |      | Permission promotion        | GrantAck       |
| GrantData       | 5  |   |   |   | * |   |  *   | Fetch data                  | GrantAck       |
| ReleaseAck      | 6  |   |   |   | * |   |      | Ack to Release[Data]        |                |
| GrantAck        | 0  |   |   |   |   | * |      | Ack to Grant (strong order) |                |

### TileLink channels

| Name | Direction  | Response | Base classes                              | Coherence  |
| :--: | :--:       |   :--:   | -------------                             | :---:      |
| A    | downwards  | D        | TLChannel < TLDataChannel < TLAddrChannel | U/C        |
| B    | upwards    | C        | TLChannel < TLDataChannel < TLAddrChannel |  C         |
| C    | downwards  |          | TLChannel < TLDataChannel < TLAddrChannel |  C         |
| D    | upwards    | E        | TLChannel < TLDataChannel                 | U/C        |
| E    | downwards  |          | TLChannel                                 |  C         |

Communication pattern:
+ client -> master: *A* -> *D* ( -> *E* if cached)
+ master -> client: *B* -> *C*

## object TLPermissions

> The three primary TileLink permissions are:
> - (T)runk: the agent is (or is on inwards path to) the global point of serialization.
> - (B)ranch: the agent is on an outwards path to
> - (N)one:
>
> These permissions are permuted by transfer operations in various ways.
> Operations can cap permissions, request for them to be grown or shrunk,
> or for a report on their current status.


#### Cap types (Grant = new permissions, Probe = permisions <= target)

- **toT** `() => 0.U`
- **toB** `() => 1.U`
- **toN** `() => 2.U`
- **isCap** `(x: UInt) => x <= toN`

#### Grow types (Acquire = permissions >= target)

- **NtoB** `() => 0.U`
- **NtoT** `() => 1.U`
- **BtoT** `() => 2.U`
- **isGrow** `(x: UInt) => x <= BtoT`

#### Shrink types (ProbeAck, Release)

- **TtoB** `() => 0.U`
- **TtoN** `() => 1.U`
- **BtoN** `() => 2.U`
- **isShrink** `(x: UInt) => x <= BtoN`

#### Report types (ProbeAck)

- **TtoT** `() => 3.U`
- **BtoB** `() => 4.U`
- **NtoN** `() => 5.U`
- **isReport** `(x: UInt) => x <= NtoN`


## object TLAtomics
*Command for atomic operations*

#### Arithmetic types
- **MIN** `() => 0.U`
- **MAX** `() => 1.U`
- **MINU** `() => 2.U`
- **MAXU** `() => 3.U`
- **ADD** `() => 4.U`
- **isArithmetic** `(x: UInt) => x <= ADD`

#### Logical types
- **XOR** `() => 0.U`
- **OR** `() => 1.U`
- **AND** `() => 2.U`
- **SWAP** `() => 3.U`
- **isLogical** `(x: UInt) => x <= SWAP`

## object TLHints
*Type of prefetch hints*

- **PREFETCH_READ** `() => 0.U`
- **PREFETCH_WRITE** `() => 1.U`

## final class TLBundle{A,B,C,D,E}
*Channel definitions*
+ *channelName*: channel name.
+ *opcode*: message type.
+ *param*: command for either Atomic, Permission or Hint.
+ *size*: **TODO** number of beats?
+ *source*: to be used as a part of the target client id for B and D.
+ *address*: address to identify master.
+ *mask*: byte mask (assume 1-bit per byte!).
+ *data*: data (so must be integer number of bytes).
+ *error*: indicating error in response packets.
+ *addr_lo*: lower address in channel *D* (beat id).
+ *sink*: to be used as a part of the target manager id for E.

Assumption: **TODO**
+ The beats in a burst on channel *A*, *B* and *C* must be in order.
+ The beats in a burst on channel *D* can be out of order? **TODO**

## class TLBundle

- **a,b,c,d,e** `DecoupledIO[TLBundleX]` the tilelink sub-channels.

### object TLBundle

- **apply** `() => TLBundle` TLBundle generator.

## class TLBundleSnoop

- **a,b,c,d,e** `DecoupledIO[TLBundleX]` the tilelink sub-channel. All directionless.

### object TLBundleSnoop
*A snoop point for a monitor to passively monitor a bus*

- **apply** `() => TLBundleSnoop` TLBundleSnoop generator.


## class TLAsyncBundle
*Tilink channel for asynchronous crossing.*

- **a,b,c,d,e** `AsyncBundle[TLBundleX]` the tilelink sub-channels.

## class TLRationalBundle
*Tilink channel for rational crossing.*

- **a,b,c,d,e** `RationalIO[TLBundleX]` the tilelink sub-channels.


<br><br><br><p align="right">
<sub>
Last updated: 21/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
