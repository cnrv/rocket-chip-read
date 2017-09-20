[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[RegisterRouter](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/RegisterRouter.scala)
=====================
**

**********************

### class TLRegisterNode
*An end node with a register file.*

~~~scala
class TLRegisterNode(
    address:     Seq[AddressSet],
    device:      Device,
    deviceKey:   String  = "reg/control",
    concurrency: Int     = 0,
    beatBytes:   Int     = 4,
    undefZero:   Boolean = true,
    executable:  Boolean = false)
  extends TLManagerNode(Seq(TLManagerPortParameters(
    Seq(TLManagerParameters(
      address            = address,
      resources          = Seq(Resource(device, deviceKey)),
      executable         = executable,
      supportsGet        = TransferSizes(1, beatBytes),
      supportsPutPartial = TransferSizes(1, beatBytes),
      supportsPutFull    = TransferSizes(1, beatBytes),
      fifoId             = Some(0))), // requests are handled in order
    beatBytes  = beatBytes,
    minLatency = min(concurrency, 1)))) // the Queue adds at most one cycle
~~~

+ **address** `Seq[AddressSet]` (param) the address space of this node.
+ **device** `Device` (param) the device descriptor of this node.
+ **deviceKey** `String` (param) the "reg-name" of this node.
+ **concurrency** `Int` (param) ??
+ **beatBytes** `Int` (param) the byte width of a beat.
+ **undefZero** `Boolean` (param) ??
+ **executable** `Boolean` (param) whether the address space is executable

<br><br><br><p align="right">
<sub>
Last updated: 20/09/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
