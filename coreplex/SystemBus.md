[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[SystemBus](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/SystemBus.scala)
========================
*The coherent bus between tiles and coherent hubs (also split memory and I/O spaces).*

**********************

## case class SystemBusParams
*Parameters used by the system bus.*

~~~scala
case class SystemBusParams(
  beatBytes: Int,
  blockBytes: Int,
  masterBuffering: BufferParams = BufferParams.default,
  slaveBuffering: BufferParams = BufferParams.flow // TODO should be BufferParams.none on BCE
) extends TLBusParams
~~~

+ **beatBytes** `Int` (param) number of bytes per beat.
+ **blockBytes** `Int` (param) number of bytes per burst.
+ **masterBuffering** `BufferParams.default` (param) buffer depth on the master (inner) side.
+ **slaveBuffering** `BufferParams.flow` (param) buffer depth on the slave (outer) side.

## class SystemBus

~~~scala
class SystemBus(params: SystemBusParams)(implicit p: Parameters) extends TLBusWrapper(params)
~~~

+ **master_splitter** `TLSplitter` (private) allows cycle-free connection to external networks.
+ **busView** `() => TLEdgeIn` get the inward Edge parameter.
+ **inwardSplitNode** `() => TLInwardNode` (protected) get the inward port of `master_splitter`.
+ **outwardSplitNode** `() => TLOutwardNode` (protected) get the outward port of `master_splitter`.
+ **tile_fixer** `TLFIFOFixer` (private) FIFO fixer for tiles.
+ **port_fixer** `TLFIFOFixer` (private) FIFO fixer for ports.
+ **master_fixer** `TLFIFOFixer` (private) FIFO fixer for masters.
+ **toSplitSlaves** `() => TLOutwardNode` get the outward port of `master_splitter`.
+ **toPeripheryBus** `() => TLOutwardNode` get the outward port of `slave_ww` as attachment point for peripheral bus.
+ **toMemoryBus** `() => TLOutwardNode` get the outward port of `xbar` as attachment point for memory bus.
+ **toSlave** `() => TLOutwardNode` get the outward port of `slave_buffer` as attachment point for slaves.
+ **fromAsyncMasters** `(depth:Int, sync:Int) => TLAsyncInwardNode`<br>
  Get an asynchornous master inward port attach point towards the `master_fixer`.
+ **fromSyncMasters** `(params: BufferParams) => TLSyncInwardNode`<br>
  Get a synchornous master inward port attach point towards the `master_fixer`.
+ **fromAsyncTiles** `(depth:Int, sync:Int) => TLAsyncInwardNode`<br>
  Get an asynchornous tile inward port attach point towards the `tile_fixer`.
+ **fromSyncTiles** `(params: BufferParams) => TLSyncInwardNode`<br>
  Get a synchornous tile inward port attach point towards the `tile_fixer`.
+ **fromRationalTiles** `(dir: RationalDirection) => TLRationalInwardNode`<br>
  Get a rational tile inward port attach point towards the `tile_fixer`.
+ **fromAsyncPorts** `(depth:Int, sync:Int) => TLAsyncInwardNode`<br>
  Get an asynchornous port inward port attach point towards the `port_fixer`.
+ **fromSyncPorts** `(params: BufferParams) => TLSyncInwardNode`<br>
  Get a synchornous port inward port attach point towards the `port_fixer`.
+ **fromRationalPorts** `(dir: RationalDirection) => TLRationalInwardNode`<br>
  Get a rational port inward port attach point towards the `port_fixer`.

The internal connections:
~~~

            tile_fixer      master_splitter      xbar       slave_buffer       slave_ww
  tile *==> ---------- *==> --------------- *==> ---- ===>* ------------ ==>* ----------- ==> toPeripheryBus
             FIFOFixer    |    Splitter        | Xbar|        Buffer    |     WidthWidget
                          |                    |     |                  |
            port_fixer    |                    |     |                  |     slave_frage
  port *==> ---------- *==>                    |     |                  \==>* -----------
             FIFOFixer                         |     |                  |      Fragmenter
                                               |     |                  \---------------- ==> toSlave
                               master_fixer    |     \----------------------------------- ==> toMemoryBus
master ------------------ *==> ------------ *==>
                                 FIFOFixer
~~~

## trait HasSystemBus
*Provides buses that serve as attachment points, for use in traits that connect individual devices or external ports.*

+ **sbus** `SystemBus` the system bus.
+ **sharedMemoryTLEdge** `() => TLEdgeIn` get the inward Edge parameter.


<br><br><br><p align="right">
<sub>
Last updated: 10/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
