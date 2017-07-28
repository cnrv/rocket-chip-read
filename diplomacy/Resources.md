[Rocket](../Readme.md)/[diplomacy](../diplomacy.md)/[Resources](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/diplomacy/Resources.scala)
=====================

*Device tree generation helpers*

**********************

- [Resource description](#resource-description)
- [Device description](#device-description)

**********************

## Resource description

### case class ResourcePermissions
*Permission of an address space.*

~~~scala
case class ResourcePermissions(r: Boolean, w: Boolean, x: Boolean, c: Boolean) // not part of DTS
~~~

+ **r** `Boolean` (param) memory region readable.
+ **w** `Boolean` (param) memory region writable.
+ **x** `Boolean` (param) memory region executable.
+ **c** `Boolean` (param) memory region cachable.


### case class ResourceAddress
*An address space with permission bits.*

~~~scala
final case class ResourceAddress(address: Seq[AddressSet], permissions: ResourcePermissions)
    extends ResourceValue
~~~

+ **address** `Seq[AddressSet]` (param) address space.
+ **permissions** `ResourcePermissions` (param) permission flags.

### case class ResourceMapping
*An address space with an offset to be respected by the address negotiation process.*

~~~scala
final case class ResourceMapping(address: Seq[AddressSet], offset: BigInt, permissions: ResourcePermissions)
    extends ResourceValue
~~~

+ **address** `Seq[AddressSet]` (param) address space.
+ **offset** `BigInt` (param) set an offset to move this address space to a specific range in the overall address space.
+ **permissions** `ResourcePermissions` (param) permission flags.

### case class ResourceInt
*Integer description in device tree.*

~~~scala
final case class ResourceInt(value: BigInt) extends ResourceValue
~~~

+ **value** `BigInt` (param) the integer value.

### case class ResourceString
*String description in device tree.*

~~~scala
final case class ResourceString(value: String) extends ResourceValue
~~~

+ **value** `String` (param) the string value.

### case class ResourceReference
*A reference pointing to another device in device tree.*

~~~scala
final case class ResourceReference(value: String) extends ResourceValue
~~~

+ **value** `String` (param) a string pointer (`Device.label`) pointing to the sub-device.

### case class ResourceMap
*A complex resource description. eg: interrupt controller.*

~~~scala
final case class ResourceMap(value: Map[String, Seq[ResourceValue]], labels: Seq[String] = Nil)
    extends ResourceValue
~~~

+ **value** `Map[String, Seq[ResourceValue]]` (param) a map of resources.
+ **labels** `Seq[String]` (param) string labels of this resource.

### case class Binding
*Used in ResourceBindings to describe the resource value associated to one property.*

~~~scala
case class Binding(device: Option[Device], value: ResourceValue)
~~~

+ **device** `Option[Device]`<br>
  The linked parent device (eg: interrupt controller to a interrupt generating device).
  If `device` is None, the the value is global.
+ **value** `ResourceValue` the resource value of this property.


### case class ResourceBindings
*A map of resource bindings.*

~~~scala
case class ResourceBindings(map: Map[String, Seq[Binding]])
~~~

+ **map** `Map[String, Seq[Binding]]` (param)
+ **apply** `(key: String) => Seq[Binding]` get the bindings of ("int").

### case class Description
*A serializable discription of a device.*

~~~scala
case class Description(name: String, mapping: Map[String, Seq[ResourceValue]])
~~~

+ **name** `String` (param) name of the described device.
+ **mapping** `Map[String, Seq[ResourceValue]]` (param) individual resource values of this device.

## Device description

## abstract class Device
*Definition of a device*

+ **describe** `(resources: ResourceBindings) => Description` (virtual) generate the device description.
+ **label** `String` A unique label of a device.

## trait DeviceInterrupts
*Interrupts of a device (extensible only to Device).*

> For a device that generates interrupts, it needs to decribe its interrupts and
> the conencted interrupt controller in its device tree entry.
> The device tree specification supports two type of interrupt description:
>
> - separate properties:
>
> ~~~
> interrupt-parent = <&intc>
> interrupts = <17, 4>
> ~~~
>
> - combined properties:
>
> ~~~
> interrupts-extended = <&intc 17> <&intc 4>
> ~~~
>
> Here for Rocket, _simple_ devices use the separate format while others use the extended format.

+ **alwaysExtended** `Boolean = false` always use the extended format.
+ **describeInterrupts** `(resources: ResourceBindings) => Map[String, Seq[ResourceValue]]`<br>
  return interrupt description.
  - **int** `Seq[Binding]` get the interupt related resource binding.
  - **parents** `Seq[Device]` get the interrupt controller devices.
  - **simple** `Boolean`<br>
  Whether to use the extended format (linked to only one controller and is forced to extended format).
  - **parent** `Option[("interrupt-parent", Seq[ResourceReference])]`<br>
  For a simple device, identify the loinked interrupt controller.
  - **interrupts** `Option[("interrupts", Seq[ResourceInt])]` for a simple device, list the interrupt lines.
  - **interrupts_extended** `Option[("interrupt-extended", Seq[(ResourceReference, ResourceInt)])]`<br>
  For an extended device, list the interrupt line pairs.
+ **int** `() => Seq(Resource(this, "int"))`

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
Last updated: 28/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
