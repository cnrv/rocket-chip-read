Notes for [Rocket-Chip](https://github.com/freechipsproject/rocket-chip)
================

**************

+ **[amba](amba.md)**
This RTL package uses diplomacy to generate bus implementations of AMBA protocols, including AXI4, AHB-lite, and APB.
+ **[chip](chip.md)**
This top-level utility package invokes Chisel to elaborate a particular configuration of a coreplex,
along with the appropriate testing collateral.
+ **[config](config.md)**
This utility package provides Scala interfaces for configuring a generator via a dynamically-scoped
parameterization library.
+ **[coreplex](coreplex.md)**
This RTL package generates a complete coreplex by gluing together a variety of components from other packages,
including: tiled Rocket cores, a system bus network, coherence agents, debug devices, interrupt handlers, externally-facing peripherals,
clock-crossers and converters from TileLink to external bus protocols (e.g. AXI or AHB).
+ **[devices](devices.md)**
This RTL package contains implementations for peripheral devices, including the Debug module and various TL slaves.
+ **[diplomacy](diplomacy.md)**
This utility package extends Chisel by allowing for two-phase hardware elaboration, in which certain parameters
are dynamically negotiated between modules.
+ **groundtest**
This RTL package generates synthesizeable hardware testers that emit randomized
memory access streams in order to stress-tests the uncore memory hierarchy.
+ **jtag**
This RTL package provides definitions for generating JTAG bus interfaces. 
+ **[regmapper](regmapper.md)**
This utility package generates slave devices with a standardized interface for accessing their memory-mapped registers.
+ **[rocket](rocket.md)**
This RTL package generates the Rocket in-order pipelined core,
as well as the L1 instruction and data caches.
This library is intended to be used by a chip generator that instantiates the
core within a memory system and connects it to the outside world.
+ **tile**
This RTL package contains components that can be combined with cores to construct tiles, such as FPUs and accelerators.
+ **[tilelink](tilelink.md)**
This RTL package uses diplomacy to generate bus implementations of the TileLink protocol. It also contains a variety
of adapters and protocol converters.
+ **unittest**
This utility package contains a framework for generateing synthesizeable hardware testers of individual modules.
+ **[util](util.md)**
This utility package provides a variety of common Scala and Chisel constructs that are re-used across
multiple other packages,

*******************

+ **[cake pattern](other/cake_pattern.md)**
+ **[Chisel operators](other/chisel_op.md)**
+ **[class index](other/index.md)**

The document is partially based on commit \#[29f5f77](https://github.com/freechipsproject/rocket-chip/tree/29f5f77817eccb771b3598e4ab9038b52e49f823).

<br><br><br><p align="right">
<sub>
Last updated: 12/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
