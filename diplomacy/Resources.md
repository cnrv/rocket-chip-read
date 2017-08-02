[Rocket](../Readme.md)/[diplomacy](../diplomacy.md)/[Resources](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/diplomacy/Resources.scala)
=====================

*Device tree generation helpers*

**********************

- [Resource description](#resource-description)
- [Device description](#device-description)
- [Device classes](#device-classes)
- [The resource bookkeeping system](#the-resource-bookkepping-system)

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
*It is used to map a device address into the bus address space. (see `SimpleBus`)*

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
+ **apply** `(key: String) => Seq[Binding]` get the key matched bindings.

### case class Description
*A serializable discription of a device.*

~~~scala
case class Description(name: String, mapping: Map[String, Seq[ResourceValue]])
~~~

+ **name** `String` (param) name of the described device.
+ **mapping** `Map[String, Seq[ResourceValue]]` (param) individual resource values of this device.

## Device description

### abstract class Device
*Definition of a device*

+ **describe** `(resources: ResourceBindings) => Description` (virtual) generate the device description.
+ **label** `String` A unique label of a device.

### trait DeviceInterrupts
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
+ **int** `() => Seq(Resource(this, "int"))` get the interrupt related device object and description string.

### trait DeviceRegName
*The device name of a device (extensible only to Device).*

+ **prefix** `String = "soc/"*` prefix
+ **describeName** `(devname: String, resources: ResourceBindings) => String`<br>
  Get the device name string.
  For a device with a register space, the name is `$prefix/$devname@$addr`
  where `$addr` points to its control register or general register space.
  Otherwise, the device is named as `$prefix/$devname`.
+ **reg** `() => Seq(Resource(this, "reg"))` get a reg device with defautl name "reg".
+ **reg** `(name: String) => Seq(Resource(this, "reg/"+name))`<br>
  Get a reg device with a name "reg/<name>".
+ **regFilter** `(String) => Boolean` a filter function used to pick reg devices.
+ **regName** `(name: String) => Option[String]` get the name provided the device is named as "reg/<name>".

## Device classes

### class SimpleDevice
*A simple device that can be named and support interrupts.*

~~~scala
class SimpleDevice(devname: String, devcompat: Seq[String])
    extends Device with DeviceInterrupts with DeviceRegName
~~~

+ **devname** `String` (param) the name of the device.
+ **devcompat** `Seq[String]*` (param) the **compatible** property of device tree.
+ **describe** `(resources: ResourceBindings) => Description` generate a description of this device.
  - **name** `String` device name.
  - **int** `Map[String, Seq[ResourceValue]]` interrupt description.
  - **compat** `("compatible", Seq[ResourceString])` compatible description.
  - **names** `("reg-names", Seq[ResourceString])` names of the names reg spaces.
  - **regs** `("reg", Seq[ResourceAddress])` the register spaces (named + bulk).
  
  Set device tree properties for "compatible", "reg-names", "reg", "interrupt-parent", "interrupts", and "interrupts-extended".

### class SimpleBus
*A simple bus.*

~~~scala
class SimpleBus(devname: String, devcompat: Seq[String], offset: BigInt = 0)
    extends SimpleDevice(devname, devcompat ++ Seq("simple-bus"))
~~~

+ **devname** `String` (param) the name of the device.
+ **devcompat** `Seq[String]*`<br>
  (param) The **compatible** property of device tree.
+ **offset** `BigInt` the offset of this bus.
  A bus is always compatible with "simple-bus".
+ **describe** `(resources: ResourceBindings) => Description` (override) generate a description of this device.
  - **ranges** `Seq[ResourceMapping]` the address spaces of all devices with the bus offset attached.
  - **map** `Seq[AddressRange]` a address range collection to contain all ranges.
  
  Set device tree properties for "#address-cells", "#size-cells", and "ranges", plus the ones set by `SimpleDevice`.

### class MemoryDevice
*Simple memory device*

~~~scala
class MemoryDevice extends Device with DeviceRegName
~~~

+ override prefix to "".
+ **describe** `(resources: ResourceBindings) =>  Description` generate a description of this device.

  Set device tree properties for "reg" and set device type to "memory".


## The resource bookkeeping system

### case class Resource
*A record of resource binding.*

~~~scala
case class Resource(owner: Device, key: String)
~~~

+ **bind** `(user: Device, value: ResourceValue) => Unit`<br>
  Record a binding of "this -> (user, value)". Here the user is another device
  (eg. the interrupt controller consume the interrupts generated by this device).
+ **bind** `(value: ResourceValue) => Unit`<br>
  Record a binding of "this -> value". A generic property.

> These bind() functions are called by the binding callback functions
> (Added by individual device using the ResourceBinding() object function into BindingScope.resourceBindingFns).
> The BindingScope is stored in BindingScope.active, from which the bind() function gets scope.

### trait BindingScope
*The bookkeeping database for a LazyModule that generates DTS.*
*Coreplex modules are the only LazyModules that generate DTS.*

+ **parentScope** `Option[BindingScope]` (private) the parent binding scope if there is one.
+ **resourceBindingFns** `Seq[() => Unit]` (protected, lazy) list of callbacks to set up bindings at scala run-time.
+ **resourceBindings** `Seq[(Resource, Option[Device], ResourceValue)]`<br>
  (protected, lazy) the binding map database.
+ **eval** `Unit` (private, lazy) use a lazy value to enforce the order of binding scope elaboration steps.

  > The binding scopes are elaborated from root to leaves.
  > The steps of eval()
  > - Check LazyModules are constructed.
  > - Ensure parent binding scopes are evaluated.
  > - Store the scope for bind() functions to use.
  > - Call all callbacks in `resourceBindingFns` in reversed order (why)?
  > - Clear the scope global variable.

+ **bindingTree** `() => ResourceMap` generate the device tree map for DTS and JSON.

### object BindingScope
+ **active** `Option[BindingScope]` pointing to the current BindingScope that is being evaluated.
+ **find** `(m: Option[LazyModule]) => Option[BindingScope]` find the first BindingScope from this to parents.

### object ResourceBinding
*A function object used to add resource binding callbacks to the callback function list in the BindingScope.*

+ **apply** `(block: => Unit) => Unit` add the callback function `block` to `BindingScope.resourceBindingFns`.


<br><br><br><p align="right">
<sub>
Last updated: 02/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
