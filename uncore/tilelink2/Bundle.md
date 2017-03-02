object **TLMessages**
-----------------------------

*Constants to define message types*

+ Channel *A*: client -> master, uncached put/get data request, cached acquire data.
+ Channel *B*: master -> client, uncached put/get data request.
+ Channel *C*: client -> master, response for packets from channel *B*.
+ Channel *D*: master -> client, response for packets from channel *A*.
+ Channel *E*: client -> master, response for Grant from channel *D* for strong ordered transactions.