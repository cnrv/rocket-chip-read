[Rocket](../Readme.md)/[tilelink](../tilelink.md)/[RegisterRouter](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tilelink/RegisterRouter.scala)
=====================
*A TileLink module that supports a register file and interrupts*

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
+ **concurrency** `Int` (param) whether the register file is pipelined (needed for SRAM/external implemented RFs)
+ **beatBytes** `Int` (param) the byte width of a beat.
+ **undefZero** `Boolean` (param) set zero to undefined fields.
+ **executable** `Boolean` (param) whether the address space is executable
+ **size** `Int` the byte size of the collective register space.
+ **regmap** `(mapping: RegField.Map*) => unit` actually route the TileLink messages to the register file.

Variables inside the regmap function:

+ **in** `RegMapperInput` the register file request port generated from TL.A channel.
+ **out** `RegMapperOutput` the register file response port to be connected to TL.D channel.

Basically, this is a TileLink wrapper of a RegMapper module.

### object TLRegisterNode
*TLRegisterNode generator*

~~~scala
object TLRegisterNode
{
  def apply(
      address:     Seq[AddressSet],
      device:      Device,
      deviceKey:   String  = "reg/control",
      concurrency: Int     = 0,
      beatBytes:   Int     = 4,
      undefZero:   Boolean = true,
      executable:  Boolean = false) =
    new TLRegisterNode(address, device, deviceKey, concurrency, beatBytes, undefZero, executable)
}
~~~

### abstract class TLRegisterRouterBase
*Base class for a TileLink register node*

~~~scala
abstract class TLRegisterRouterBase(
    devname: String,             // used by device
    devcompat: Seq[String],      // used by device
    val address: AddressSet,     // used by register node
    interrupts: Int,             // used by interrupt souce node
    concurrency: Int,            // used by register node
    beatBytes: Int,              // used by register node
    undefZero: Boolean,          // used by register node
    executable: Boolean          // used by register node
    )(implicit p: Parameters)
    extends LazyModule
~~~

+ **device** `SimpleDevice(devname, devcompat)` set up a simple device for the register file.
+ **node** `TLRegisterNode(Seq(address), device, "reg/control", concurrency, beatBytes, undefZero, executable)` set up the register node.
+ **intnode** `IntSourceNode(IntSourcePortSimple(num = interrupts, resources = Seq(Resource(device, "int"))))` set up an interrupt node.

### case class TLRegBundleArg

~~~scala
case class TLRegBundleArg(interrupts: HeterogeneousBag[Vec[Bool]], in: HeterogeneousBag[TLBundle])(implicit val p: Parameters)
~~~

### class TLRegBundleBase
*Base bundle for a register node, used for interrupt wire connections*

~~~scala
class TLRegBundleBase(arg: TLRegBundleArg) extends Bundle
~~~

+ **interrupts** `HeterogeneousBag[Vec[Bool]]` interrupt ports.
+ **in** `HeterogeneousBag[TLBundle]` TileLink input ports.

### class TLRegBundle
*Generic TileLink interrupt bundle*

~~~scala
class TLRegBundle[P](val params: P, arg: TLRegBundleArg)(implicit p: Parameters) extends TLRegBundleBase(arg)
~~~

### class TLRegModule
*Module implemetation of a TileLink register module.*

~~~scala
class TLRegModule[P, B <: TLRegBundleBase](val params: P, bundleBuilder: => B, router: TLRegisterRouterBase)
  extends LazyModuleImp(router) with HasRegMap
~~~

+ **io** `<: TLRegBundleBase` the module IO bundle.
+ **interrupts** `Vec[Bool]` internal interrupt lines.
+ **address** `AddressSet` the address set of this register module.
+ **regmap** `(mapping: RegField.Map*) => Unit` link regmap to `TLRegisterNode.regmap()`.

### class TLRegisterRouter
*The actual class used to make a register device.*

~~~scala
class TLRegisterRouter[B <: TLRegBundleBase, M <: LazyModuleImp](
     val base:        BigInt,
     val devname:     String,
     val devcompat:   Seq[String],
     val interrupts:  Int     = 0,
     val size:        BigInt  = 4096,
     val concurrency: Int     = 0,
     val beatBytes:   Int     = 4,
     val undefZero:   Boolean = true,
     val executable:  Boolean = false)
   (bundleBuilder: TLRegBundleArg => B)
   (moduleBuilder: (=> B, TLRegisterRouterBase) => M)(implicit p: Parameters)
  extends TLRegisterRouterBase(devname, devcompat, AddressSet(base, size-1), interrupts, concurrency, beatBytes, undefZero, executable)
{
  // require (size >= 4096) ... not absolutely required, but highly recommended
  lazy val module = moduleBuilder(bundleBuilder(TLRegBundleArg(intnode.bundleOut, node.bundleIn)), this)
}
~~~

+ **base** `BigInt` (param) the base address of this register device.
+ **devname** `String` (param) the device name used in device tree.
+ **devcompat** `Seq[String]` (param) the compatible device list used in the device tree.
+ **interrupts** `Int` (param) the number interrupt lines used by this device, used in interrupt souce node `IntSourceNode`.
+ **size** `BigInt` (param) the tatol address space size of this device (assume bigger than the actual register fields).
+ **concurrency** `Int` (param) the number of concurrent transactions. (0, reg; 1, SRAM, >1: even slower memory)
+ **beatBytes** `Int` (param) byte width of TileLink link.
+ **undefZero** `Boolean` (param) whether to set zero to undefined fields.
+ **executable** `Boolean` (param) whether the address space is executable.
+ **bundleBuilder** `(TLRegBundleArg) => TLRegBundleBase` a IO bundle generator (to habdle internal or external generated interrupts).
+ **moduleBuilder** `(=> TLRegBundleBase, TLRegisterRouterBase) => LazyModuleImp` a register module generator.


<br><br><br><p align="right">
<sub>
Last updated: 25/09/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>


