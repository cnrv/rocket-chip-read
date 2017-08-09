[Rocket](Readme.md)/[tilelink](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/tilelink)
========================
This RTL package uses diplomacy to generate bus implementations of the TileLink protocol. It also contains a variety
of adapters and protocol converters.

**********************

+ **[package](tilelink/package.md)**
  shared helper variables and functions.
+ **[Arbiter](tilelink/Arbiter.md)**
  TileLink arbiter.
+ **[Buffer](tilelink/Buffer.md)**
  buffer for TileLink channels.
+ **[Bundles](tilelink/Bundles.md)**
  TileLink channel definitions.
+ **[Bus](tilelink/Bus.md)**
  generic TileLink bus implementation.
+ **[Edges](tilelink/Edges.md)**
  definitions for the TileLink packets.
+ **[FIFOFixer](tilelink/FIFOFixer.md)**
  enforce FIFO order if required (related to the order of transactions from a shared port).
+ **[IntNodes](tilelink/IntNodes.md)**
  interrupt related nodes.
+ **[Nodes](tilelink/Nodes.md)**
  TileLink Nodes
+ **[Parameters](tilelink/Parameters.md)**
  TileLink interconnection parameters.
+ **[Splitter](tilelink/Splitter.md)**
  TileLink demultiplexer.
+ **[Xbar](tilelink/Xbar.md)**
  generic Tilelink crossbar.



<br><br><br><p align="right">
<sub>
Last updated: 09/08/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
