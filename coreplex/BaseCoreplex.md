[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[BaseCoreplex](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/BaseCoreplex.scala)
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
  + **outer** `BareCoreplex` pointer to the related LazyModule.
+ BareCoreplexModule
  + **outer** `BareCoreplex` pointer to the related LazyModule.
  + **io** `BareCoreplexBundle` I/O bundle.

### BaseCoreplex
*Base coreplex of Rocket chip. Support on-chip **interconnects** and **coherence managers**.*

~~~scala
BaseCoreplex extends BareCoreplex with CoreplexNetwork with BankedL2CoherenceManagers
~~~

+ BaseCoreplex
+ BaseCoreplexBundle
+ BaseCoreplexModule

<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 20/06/2017</sub></p>

