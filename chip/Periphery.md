[Rocket](../Readme.md)/[chip](../chip.md)/[Periphery](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/chip/Periphery.scala)
=====================

**********************

### trait HasPeripheryParameters
*Parameters for peripherials.*

+ **peripheryBusConfig** `() => TLBusConfig`
+ **peripheryBusBytes** `() => Int` byte width of peripheral bus.
+ **socBusConfig** `() => TLBusConfig`
+ **socBusBytes** `() => Int` byte width of SoC bus.
+ **cacheBlockBytes** `() => Int` byte size of a cache block.
+ **peripheryBusArithmetic** `() => Boolean`
+ **nMemoryChannels** `() => Int` number of memory channels.
+ **nExtInterrupts** `() => Int` number of external interrupt lines.

### trait HasSystemNetworks
*HasSystemNetworks provides buses that will serve as attachment points,*
*for use in child traits that connect individual agents or external ports.*

~~~scala
trait HasSystemNetworks extends HasPeripheryParameters
~~~

+ **socBus** `LazyModule(new TLXbar)` Wide or unordered-access slave devices (TL-UH).
+ **peripheryBus** `LazyModule(new TLXbar)` Narrow and ordered-access slave devices (TL-UL).
+ **intBus** `LazyModule(new IntXbar)` Device and global external interrupts.
+ **fsb** `LazyModule(new TLBuffer(BufferParams.none))` Master devices talking to the frontside of the L2.
+ **bsb** `LazyModule(new TLBuffer(BufferParams.none))` Slave devices talking to the backside of the L2.
+ **mem** `Seq[LazyModule(new TLXbar)]` Ports out to DRAM.

## HasPeripheryExtInterrupts

### abstract trait HasPeripheryExtInterrupts
*This trait adds externally driven interrupts to the system.*
*However, it should not be used directly; instead one of the below*
*synchronization wiring child traits should be used.*

~~~scala
abstract trait HasPeripheryExtInterrupts extends HasSystemNetworks
~~~

+ **extInterrupts** `IntInternalInputNode` External interrupt input ports.

### trait HasPeripheryAsyncExtInterrupts
*This trait should be used if the External Interrupts have NOT*
*already been synchronized to the Periphery (PLIC) Clock.*

~~~scala
trait HasPeripheryAsyncExtInterrupts extends HasPeripheryExtInterrupts
~~~

Adding a `LazyModule(new IntXing)` in between of `intBus.intnode` and `extInterrupts`.

### trait HasPeripherySyncExtInterrupts
*This trait can be used if the External Interrupts have already been synchronized*
*to the Periphery (PLIC) Clock.*

~~~scala
trait HasPeripherySyncExtInterrupts extends HasPeripheryExtInterrupts
~~~

Directly connect `intBus.intnode` and `extInterrupts`.

### trait HasPeripheryExtInterruptsBundle
*Common io name and methods for propagating or tying off the port bundle.*

~~~scala
trait HasPeripheryExtInterruptsBundle extends HasPeripheryParameters
~~~

+ **interrupts** `UInt` The value of external interrupt
+ **tieOffInterrupts** `() => Unit` tie all interupts to zeros.

### trait HasPeripheryExtInterruptsModuleImp
*This trait performs the translation from a UInt IO into Diplomatic Interrupts.*
*The wiring must be done in the concrete LazyModuleImp.*

~~~scala
trait HasPeripheryExtInterruptsModuleImp extends LazyMultiIOModuleImp
    with HasPeripheryExtInterruptsBundle
~~~

+ **outer** `HasPeripheryExtInterrupts` pointer to parent LazyModule.
+ **interrupts** `IO(UInt(INPUT, width = outer.nExtInterrupts))` The actual external interrupt ports.


<br><br><br><p align="right">
<sub>
Last updated: 09/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>

