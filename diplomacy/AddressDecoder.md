[Rocket](../Readme.md)/[diplomacy](../diplomacy.md)/[AddressDecoder](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/diplomacy/AddressDecoder.scala)
=====================
*Find the minimum subset of bits needed to disambiguate port addresses.*

**********************

### object AddressDecoder

+ **apply** `(ports: Seq[Seq[AddressSet]], givenBits: BigInt = 0) => BigInt`<br>
  Find the minimum subset of bits needed to disambiguate port addresses.<br>
  **port**: the address ranges to analyse.<br>
  **givenBits**: the preset mask (any bit in this mask that less than the maximal base range will be used in the final mask).

The implementation of this function object is difficult to read.
Here are some key comments from the code provided by [Wesley W. Terpstra](https://github.com/terpstra).

~~~
The algorithm has a set of partitions, discriminated by the selected bits.
Each partion has a set of ports, listing all addresses that lead to that port.
Seq[Seq[Seq[AddressSet]]]
        ^^^^^^^^^^^^^^^ set of addresses that are routed out this port
    ^^^ the list of ports
^^^ cases already distinguished by the selected bits thus far

Solving this problem is NP-hard, so we use a simple greedy heuristic:
  pick the bit which minimizes the number of ports in each partition
  as a secondary goal, reduce the number of AddressSets within a partition
~~~

<br><br><br><p align="right">
<sub>
Last updated: 12/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
