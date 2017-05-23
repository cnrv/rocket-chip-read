[Rocket](../Readme.md)/[rocket](../rocket.md)/[BTB](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/rocket/BTB.scala)
========================
*Brach target buffer.*

*****************

class RAS
-----------------
*Return address stack*

+ **push** `(addr:UInt) -> Unit` Push an address to stack.
+ **peek** `() -> addr:UInt` Peek the last address.
+ **pop** `() -> Unit` Pop an address.
+ **clear** `() -> Unit` Clear the stack.
+ **isEmpty** `() -> Bool` Check whether the stack is empty.

class BHT
--------------------
*Branch history table*

+ Comment from source:
~~~
 BHT contains table of 2-bit counters and a global history register.
 The BHT only predicts and updates when there is a BTB hit.
 The global history:
    - updated speculatively in fetch (if there's a BTB hit).
    - on a mispredict, the history register is reset (again, only if BTB hit).
 The counter table:
    - each counter corresponds with the address of the fetch packet ("fetch pc").
    - updated when a branch resolves (and BTB was a hit for that branch).
      The updating branch must provide its "fetch pc".
~~~
+ **get** `(addr:UInt, update:Bool) -> BHTResp`<br>
  Get the saturation counter's value. Update the history when `update` is true.
+ **update** `(addr:UInt, d:BHTResp, taken:Bool, mispredict:Bool) -> Unit`<br>
  Update the history. When mispredict, correct the history. 

class BTB
----------------------------
*Branch atrget buffer*

+ Comment from source:
~~~
Fully-associative branch target buffer.
Higher-performance processors may cause BTB updates to occur out-of-order,
which requires an extra CAM port for updates (to ensure no duplicates get
placed in BTB).
~~~

+ I/O, type and parameters

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| p                      | Parameters       | param      | configuration                         |
| req                    | Valid[BTBReq]    | I          | request fro branch target.            |
| resp                   | Valid[BTBResp]   | O          | branch target response.               |
| btb\_update            | Valid[BTBUpdate] | I          | update BTB from MEM stage.            |
| bht\_update            | Valid[BHTUpdate] | I          | update BHT when branch from MEM stage.       |
| ras\_update            | Valid[RASUpdate] | I          | update when function call or return from ID. |


<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 23/05/2017</sub></p>
