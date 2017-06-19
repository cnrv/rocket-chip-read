[Rocket](../Readme.md)/[uncore](../uncore.md)/[BaseCoreplex](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/BaseCoreplex.scala)
========================
*The base class of a Rocket-chip.*

**********************

### BareCoreplex
*Bare-metal coreplex*

~~~scala
BareCoreplex extends LazyModule with BindingScope
~~~

+ BareCoreplex
+ BareCoreplexBundle
+ BareCoreplexModule

### BaseCoreplex
*Base coreplex of Rocket chip. Support on-chip **interconnects** and **coherence managers**.*

~~~scala
BaseCoreplex extends BareCoreplex with CoreplexNetwork with BankedL2CoherenceManagers
~~~

+ BaseCoreplex
+ BaseCoreplexBundle
+ BaseCoreplexModule

<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 19/06/2017</sub></p>

