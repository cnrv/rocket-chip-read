[Rocket](Readme.md)/[coreplex](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/coreplex)
========================
This RTL package generates a complete coreplex by gluing together a variety of components from other packages,
including: tiled Rocket cores, a system bus network, coherence agents, debug devices, interrupt handlers, externally-facing peripherals,
clock-crossers and converters from TileLink to external bus protocols (e.g. AXI or AHB).

**********************

+ [BaseCoreplex](coreplex/BaseCoreplex.md)<br>
  The base class of a Rocket-chip.
+ [CoreplexNetwork](coreplex/CoreplexNetwork.md)<br>
  On-chip interconnect of a Rocket-chip.
+ [RISCVPlatform](coreplex/RISCVPlatform.md)<br>
  RISCV SoC Platform.
+ [RocketCoreplex](coreplex/RocketCoreplex.md)<br>
  Negotiate the interrupt, clock and reset connections for Rocket Tiles.


<br><br><br><p align="right">
<sub>
Last updated: 24/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
