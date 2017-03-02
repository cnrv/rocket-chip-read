object TLMessages
-----------------------------
*Constants to define message types*

+ Channel *A*: client -> master, uncached put/get data request, cached acquire data.
+ Channel *B*: master -> client, uncached put/get data request.
+ Channel *C*: client -> master, response for packets from channel *B*.
+ Channel *D*: master -> client, response for packets from channel *A*.
+ Channel *E*: client -> master, response for Grant from channel *D* for strong ordered transactions.

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




