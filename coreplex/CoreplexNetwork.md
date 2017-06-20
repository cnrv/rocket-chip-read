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
+ **tile_splitter** `LazyModule(new TLSplitter)`
+ **l1tol2** `LazyModule(new TLXbar)` the crossbar between L1$ and L2$.
+ **cbus** `LazyModule(new TLXbar)` the coherent bus
+ **intBar** `LazyModule(new IntXbar)` interrupt crossbar.
+ **mmio** `TLOutputNode()` MMIO port.
+ **mmioInt** `IntInputNode()` MMIO interrupt port.
+ **l2in** `TLInputNode()` DDR to L2$ port.
+ **l2out** `TLOutputNode()` L1$ to DDR port.



<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 20/06/2017</sub></p>
