[Rocket](../Readme.md)/[rocketchip](../rocketchip.md)/[Configs](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/rocketchip/Configs.scala)
=====================

*Available configuration parameters for the Rocket-Chip generator.*

**********************

## class BasePlatformConfig
*Basic configuration parameters*

+ device tree (DTS) descriptive parameters
  + **DTSModel** `"ucbbar,rocketship-unknown"`
  + **DTSCompat** `Nil`
  + **DTSTimebase** `1000000`<br>
    1 Mhz
  + **RTCPeriod** `1000`<br>
    Implies coreplex clock is DTSTimebase * RTCPeriod = 1 GHz
+ Tilelink connection parameters
  + **TLMonitorBuilder** `(args: TLMonitorArgs) => Some(LazyModule(new TLMonitor(args)))`
  + **TLCombinationalCheck** `false`<br>
    Adding connections between valid and ready to form a loop is `valid` depends on `ready`.
    This will cause combinational loop check failures in synthesis tools.
    Also test components are added to dump garabage to check corrupt data during `!valid` is safe.
+ Memory parameters
  + **NExtTopInterrupts** `2`
  + **SOCBusConfig** `site(L1toL2Config)`
  + **PeripheryBusConfig** `TLBusConfig(beatBytes = 4)`
  + **PeripheryBusArithmetic** `true`
  + **IncludeJtagDTM** `true`
  + **JtagDTMKey** `new JtagDTMKeyDefault()`
  + **ZeroConfig** `ZeroConfig(base=0xa000000L, size=0x2000000L, beatBytes=8)`
  + **ErrorConfig** `ErrorConfig(Seq(AddressSet(0x3000, 0xfff)))`
  + **ExtMem** `MasterConfig(base=0x80000000L, size=0x10000000L, beatBytes=8, idBits=4)`
  + **ExtBus** `MasterConfig(base=0x60000000L, size=0x20000000L, beatBytes=8, idBits=4)`
  + **ExtIn** `SlaveConfig(beatBytes=8, idBits=8, sourceBits=4)`

<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 15/06/2017</sub></p>

