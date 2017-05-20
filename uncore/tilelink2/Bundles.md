[Rocket](../../Readme.md)/[uncore](../../uncore.md)/[tilelink2](../tilelink2.md)/[Bundles](https://github.com/ucb-bar/rocket-chip/blob/master/src/main/scala/uncore/tilelink2/Bundles.scala)
=====================
*TileLink2 channel definitions.*

**********************


object TLMessages
-----------------------------
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

| Name | Direction  | Response | Base classes                              |
| :--: |            |   :--:   | -------------                             |
| A    | downwards  | D        | TLChannel < TLDataChannel < TLAddrChannel |
| B    | upwards    | C        | TLChannel < TLDataChannel < TLAddrChannel |
| C    | downwards  |          | TLChannel < TLDataChannel < TLAddrChannel |
| D    | upwards    | E        | TLChannel < TLDataChannel                 |
| E    | downwards  |          | TLChannel                                 |

Communication pattern:
+ client -> master: *A* -> *D* -> *E*
+ master -> client: *B* -> *C*

object TLPermissions
-----------------------------
**TODO** ?? (T)runk, (B)ranch, (N)one


object TLAtomics
-----------------------------
*Command for atomic operations*


object TLHints
-----------------------------
*Type of prefetch hints*

final class TLBundle{A,B,C,D,E}
------------------------------
*Channel definitions*
+ *channelName*: channel name.
+ *opcode*: **TODO** message type?.
+ *param*: command for either Atomic, Permission or Hint.
+ *size*: **TODO** number of beats?
+ *source*: **TODO** client id?
+ *address*: address to identify master.
+ *mask*: byte mask (assume 1-bit per byte!).
+ *data*: data (so must be integer number of bytes).
+ *error*: indicating error in response packets.
+ *addr_lo*: lower address in channel *D* (beat id).
+ *sink*: **TODO** ?

Assumption: **TODO**
+ The beats in a burst on channel *A*, *B* and *C* must be in order.
+ The beats in a burst on channel *D* can be out of order? **TODO**

object TLBundleSnoop
------------------------------
*A snoop point for a monitor to passively monitor a bus*

object TLRationalBundle
------------------------------
**TODO** *A bus connection for rational clock domains?*



<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 02/04/2017</sub></p>

