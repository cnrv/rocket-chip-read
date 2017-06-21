[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[CoreplexNetwork](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/CoreplexNetwork.scala)
========================
*On-chip interconnect of a Rocket-chip.*

**********************

### CoreplexNetwork
*Trait for LazyModule.*

~~~scala
trait CoreplexNetwork extends HasCoreplexParameters
~~~

+ **module** `CoreplexNetworkModule` pointer to the generated module.
+ **sbus** `LazyModule(new TLXbar)` globally-visible high-bandwidth devices.
+ **pbus** `LazyModule(new TLXbar)` globally-visible low-bandwidth devices.
+ **tile_splitter** `LazyModule(new TLSplitter)` cycle-free connection to external networks.
+ **int_xbar** `LazyModule(new IntXbar)` interrupt crossbar.
+ **mmio** `TLOutputNode()` external memory-mapped IO slaves.
+ **mmioInt** `IntInputNode()` external devices' interrupts.
+ **l2in** `TLInputNode()` external masters talking to the frontside of the shared cache.
+ **l2out** `TLOutputNode()` external slaves hanging off the backside of the shared cache.
+ **root** `Device` the root (`/`) desciption in the device tree.
+ **soc** `Device` the `soc` desciption in the device tree.
+ **cpus** `Device` the `cpus` desciption in the device tree.
+ **topManagers** `Some(ManagerUnification)` ??

![Coreplex Network](../figure/coreplex/coreplex_network.png)



<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 21/06/2017</sub></p>
