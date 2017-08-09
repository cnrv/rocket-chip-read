[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[InterruptBus](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/InterruptBus.scala)
========================
*The coreplex interrupt bus.*

Potential cake pattern mixes:
- Asynchronous interrupts: `HasAsyncExtInterrupts` + `HasExtInterruptsBundle` + `HasExtInterruptsModuleImp`
- Synchronous interrupts: `HasSyncExtInterrupts` + `HasExtInterruptsBundle` + `HasExtInterruptsModuleImp`
- Inputs `UInt`: `HasExtInterruptsModuleImp.interrupts`
- Outputs `IntOutwardNode`: `HasAsyncExtInterrupts.toPLIC` or `HasSyncExtInterrupts.toPLIC`


**********************

## class InterruptBusWrapper
*An interrupt bus used inside a coreplex.*

+ **int\_bus** `IntXbar` the interrupt crossbar.
+ **fromAsync** `IntInwardNode` get an asynchronous attach point for the interrupt bus.
+ **fromRational** `IntInwardNode` get a rational attach point for the interrupt bus.
+ **fromSync** `IntInwardNode` get a synchronous attach point for the interrupt bus.
+ **toPLIC** `IntOutwardNode` get the output towards the platform level interrupt controller.

## trait HasInterruptBus
*Add an interrupt bus for a coreplex.*

+ **ibus** `InterruptBusWrapper` the coreplex interrupt bus.

## abstract trait HasExtInterrupts
*This trait adds externally driven interrupts to the system.*
*However, it should not be used directly; instead one of the below synchronization wiring child traits should be used.*

~~~scala
abstract trait HasExtInterrupts extends HasInterruptBus {
  private val device = new Device with DeviceInterrupts {
    def describe(resources: ResourceBindings): Description = {
      Description("soc/external-interrupts", describeInterrupts(resources))
    }
  }
}
~~~

+ **device** `Device with DeviceInterrupts` the interrupt device description.
+ **nExtInterrupts** `Int` the number of external interrupt defined by parameter `NExtTopInterrupts`.
+ **extInterrupts** `IntInternalInputNode` the internal interrupt ports.

## trait HasAsyncExtInterrupts
*This trait should be used if the External Interrupts have NOT already been synchronized to the Periphery (PLIC) Clock.*

~~~scala
trait HasAsyncExtInterrupts extends HasExtInterrupts {
  if (nExtInterrupts > 0) {
    ibus.fromAsync := extInterrupts
  }
}
~~~

## trait HasSyncExtInterrupts
*This trait can be used if the External Interrupts have already been synchronized to the Periphery (PLIC) Clock.*

~~~scala
trait HasSyncExtInterrupts extends HasExtInterrupts {
  if (nExtInterrupts > 0) {
    ibus.fromSync := extInterrupts
  }
}
~~~

## trait HasExtInterruptsBundle
*Common io name and methods for propagating or tying off the port bundle.*

+ **interrupts** `UInt` the interrupt port.
+ **tieOffInterrupts** `() => Unit` tie all interrupt to low.

## trait HasExtInterruptsModuleImp
*This trait performs the translation from a UInt IO into Diplomatic Interrupts. The wiring must be done in the concrete LazyModuleImp.*

~~~scala
trait HasExtInterruptsModuleImp extends LazyMultiIOModuleImp with HasExtInterruptsBundle {
  val outer: HasExtInterrupts
  val interrupts = IO(UInt(INPUT, width = outer.nExtInterrupts))
  outer.extInterrupts.bundleIn.flatten.zipWithIndex.foreach { case(o, i) => o := interrupts(i) }
}
~~~

+ **outer** `HasExtInterrupts` pointing to the LazyModule.
+ **interrupts** `UInt` the interrupt port.

<br><br><br><p align="right">
<sub>
Last updated: 09/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
