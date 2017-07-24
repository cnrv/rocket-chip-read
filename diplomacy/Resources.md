[Rocket](../Readme.md)/[diplomacy](../diplomacy.md)/[Resources](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/diplomacy/Resources.scala)
=====================

*Device tree generation helpers*

**********************

## case class ResourcePermissions
~~~scala
case class ResourcePermissions(r: Boolean, w: Boolean, x: Boolean, c: Boolean) // not part of DTS
~~~

+ **r** `Boolean` (param) memory region readable.
+ **w** `Boolean` (param) memory region writable.
+ **x** `Boolean` (param) memory region executable.
+ **c** `Boolean` (param) memory region cachable.


## case class ResourceAddress
~~~scala
final case class ResourceAddress(address: Seq[AddressSet], permissions: ResourcePermissions)
    extends ResourceValue
~~~

*An address space with permission bits.*

+ **address** `Seq[AddressSet]` (param) address space.
+ **permissions** `ResourcePermissions` (param) permission flags.

## case class ResourceMapping
~~~scala
final case class ResourceMapping(address: Seq[AddressSet], offset: BigInt) extends ResourceValue
~~~


## case class ResourceInt
*Integer description in device tree.*
~~~scala
final case class ResourceInt(value: BigInt) extends ResourceValue
~~~

## case class ResourceString
*String description in device tree.*
~~~scala
final case class ResourceString(value: String) extends ResourceValue
~~~


## case class ResourceReference
*A reference pointing to another device in device tree.*
~~~scala
final case class ResourceReference(value: String) extends ResourceValue
~~~

## case class ResourceMap
~~~scala
final case class ResourceMap(value: Map[String, Seq[ResourceValue]], labels: Seq[String] = Nil)
    extends ResourceValue
~~~

## case class Binding
*Bind a device to a resource configuration. If device is None, the value is global.*


## case class ResourceBindings
*A map of resource bindings.*

+ **apply** `(key: String) => Seq[Binding]` get the bindings of ("int").

## case class Description
*A serializable discription of a device.*

## abstract class Device
*Definition of a device*

+ **describe** `(resources: ResourceBindings) => Description` (virtual) generate the device description.
+ **label** `String` A unique label of a device.

## trait DeviceInterrupts
*Interrupts of a device (extensible only to Device).*

+ **alwaysExtended** `Boolean = false`

    Not a concrete device (but a middle layer agent)??

+ **describeInterrupts** `(resources: ResourceBindings) => Map[String, Seq[ResourceValue]]`

    return interrupt definitions.

  + `("interrupt-parent" -> Seq(ResourceReference(Device.label)))` A concrete device's label.
  + `("interrupts" -> Seq[ResourceValue])` A concrete device's interrupts.
  + `("interrupts-extended" -> Seq[ResourceMap])` An extended devices' interrupts.

+ **int** `_ => Seq(Resource(this, "int"))`

    ??

## trait DeviceRegName
*Device registration name (extensible only to Device).*

+ **prefix** `String = "soc/"*` prefix
+ **describeName** `(devname: String, resources: ResourceBindings) => String`

    Get the device name string. For a valid device, the name is `$prefix/$devname@$base_addr`

+ **reg** `_ => Seq(Resource(this, "reg"))`

    ??

## class SimpleDevice
~~~scala
class SimpleDevice(devname: String, devcompat: Seq[String])
    extends Device with DeviceInterrupts with DeviceRegName
~~~

*Simple device device definition.*

+ *describe: (resources: ResourceBindings) => Description*: generate a description of this device
~~~scala
Description(describeName(devname, resources),
    ListMap("reg"        -> resources("reg").map(_.value),
            "compatible" -> devcompat.map(ResourceString(_)), // optional
            describeInterrupts(resources)))
~~~

## class MemoryDevice
~~~scala
class MemoryDevice extends Device with DeviceRegName
~~~

*Simple memory device definition*

+ override prefix to "".
+ *describe: (resources: ResourceBindings) =>  Description*: generate a description of this device
~~~scala
Description(describeName("memory", resources),
    ListMap("reg"         ->resources("reg").map(_.value),
            "device_type" -> Seq(ResourceString("memory"))))
~~~


## case class Resource

+ **bind** `(user: Device, value: ResourceValue) => Unit`
+ **bind** `(value: ResourceValue) => Unit`

## trait BindingScope
*(extensible only to LazyModule)*

+ **bindingTree** `_ => ResourceMap`

    Generate device tree map.

### object BindingScope
+ **active** `Option[BindingScope]`

    The current active LazyModule needing binding.

+ **find** `(m: Option[LazyModule]) => Option[BindingScope]`

    Return the first parent `LazyModule` extended with `BindingScope`.

## object ResourceBinding
*An global function object that is called with extension (weird Scala code pattern) in a device to initialize all binding functions.*

+ **apply** `(block: => Unit): Unit`

    Add a new code segement `block` into the binding functions.


<br><br><br><p align="right">
<sub>
Last updated: 24/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
