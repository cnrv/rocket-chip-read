[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[BaseCoreplex](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/BaseCoreplex.scala)
========================
*The base class of a Rocket-chip.*

**********************

## BareCoreplex
*Bare-metal coreplex*

~~~scala
BareCoreplex extends LazyModule with BindingScope
~~~

### abstract class BareCoreplex
### abstract class BareCoreplexBundle
  + **outer** `BareCoreplex` pointer to the related LazyModule.
### abstract class BareCoreplexModule
  + **outer** `BareCoreplex` pointer to the related LazyModule.
  + **io** `BareCoreplexBundle` I/O bundle.

## BaseCoreplex
*Base coreplex of Rocket chip. Support on-chip **interconnects** and **coherence managers**.*

~~~scala
BaseCoreplex extends BareCoreplex with CoreplexNetwork with BankedL2CoherenceManagers
~~~

### abstract class BaseCoreplex
### class BaseCoreplexBundle
### class BaseCoreplexModule

<br><br><br><p align="right">
<sub>
Last updated: 20/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>


