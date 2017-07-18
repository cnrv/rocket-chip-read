[Rocket](../Readme.md)/[diplomacy](../diplomacy.md)/[Parameters](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/diplomacy/Parameters.scala)
=====================

**********************
object RegionType
------------------------------
*Type of address region*

+ **CACHED**: cached memory region
+ **TRACKED**: ??
+ **UNCACHED**: uncached address space
+ **PUT\_EFFECTS**: ??
+ **GET\_EFFECTS**: ??

case class IdRange
----------------------
*A non-empty half-open range `[start, end)`, `0 <= start < end`*

~~~scala
case class IdRange(start: Int, end: Int)
~~~

+ **operator <** `(IdRange, IdRange) => Boolean` strict partial order (lhs.end &le; rhs.start)
+ **operator >** `(IdRange, IdRange) => Boolean` strict partial order (lhs.start > rhs.end)
+ **overlaps** `(x: IdRange) => Boolean` this &cap; x &ne; &empty;
+ **contains** <br>
  `(x: IdRange) => Boolean` this &supe; x<br>
  `(x: Int) => Boolean` x &isin; this<br>
  `(x: UInt) => Bool` x &isin; this
+ **shift** `(x: Int) => IdRange` shift range by positive x
+ **size** `() => Int` size of range
+ **range** `() => Range` iterate

case class TransferSizes
--------------------------
*An potentially empty inclusive range of 2's powers `[min, max]`, <br>
`0 <= min <= max && isPow2(max) && isPow2(min) && (max == 0 || min != 0)`*

~~~scala
case class TransferSizes(min: Int, max: Int)
~~~

+ **none** `() => Boolean` is empty
+ **contains** <br>
  `(x: Int) => Boolean` isPow2(x) && x &isin; this<br>
  `(x: TransferSizes) => Boolean` this &supe; x
+ **containsLg**<br>
  `(x: Int) => Boolean` (1 << x) &isin; this<br>
  `(x: UInt) => Bool` (1.U << x) &isin; this
+ **intersect** `(x: TransferSizes) => TransferSizes` this &cap; x

case class AddressRange
---------------------------

~~~scala
case class AddressRange(base: BigInt, size: BigInt) extends Ordered[AddressRange]
~~~

*An address range expression*

+ **end** `BigInt = base + size` end of the address range.
+ **compare** `AddressRange => Boolean` compare two ranges.
+ **operator < <= > >=** `AddressRange => Boolean` derived from Ordered[AddressRange]
+ **contains** `(x: AddressRange) => Boolean` this &supe; x
+ **union** `(x: AddressRange) => Some[AddressRange]` this &cup; x

object AddressRange
----------------------------
+ **fromSets** `(seq: Seq[AddressSet]) => Seq[AddressRange]` convert AddressSet to unified AddressRange
+ **unify** `(seq: Seq[AddressRange]) => Seq[AddressRange]` combine ranges which are combinable (order as well)

case class AddressSet
----------------------------
*AddressSets specify the address space managed by the manager*<br>
*Base is the base address, and mask are the bits consumed by the manager*<br>
*e.g: base=0x200, mask=0xff describes a device managing 0x200-0x2ff*<br>
*e.g: base=0x1000, mask=0xf0f decribes a device managing 0x1000-0x100f, 0x1100-0x110f, ...*<br>

~~~scala
case class AddressSet(base: BigInt, mask: BigInt) extends Ordered[AddressSet]
~~~

+ **compare** `(AddressSet) => Boolean` compare two ranges.
+ **operator < <= > >=** `(AddressSet => Boolean)` derived from Ordered[AddressSet]
+ **contains** <br>
  `(x: BigInt) => Boolean` x &isin; this<br>
  `(x: UInt) => Boolean` x &isin; this<br>
  `(x: AddressSet) => Boolean` x &supe; this
+ **overlaps** `(x: AddressSet) => Boolean` this &cap; x &ne; &empty;
+ **intersect** `(x: AddressSet) => Some[AddressSet]` this &cap; x
+ **alignment** `() => BigInt` get the minimal alignment (mask: 0x0000ffff => 0x00010000)
+ **contiguous** `() => Boolean` whether the address space is contiguous(mask: 0x0000ffff => true, mask:0x0000ff0f => false)
+ **finite** `() => Boolean` mask &ge; 0 ??
+ **max** `() => BigInt` the address upper bound
+ **widen** `(imask: BitInt) => AddressSet`<br>
  Get a larger space using imask.<br>
  Widen the match function to ignore all bits in imask:<br>
  `AddressSet(base, mask) => AddressSet(base & ~imask, mask | imask)`
+ **toString** `() => String` convert to string
+ **toRange** `() => AddressRange` convert to AddressRange

object AddressSet
----------------------------
+ **misaligned** `(BigInt, BigInt, Seq[AddressSet]) => Seq[AddressSet]` ?? not used
+ **unify** `(seq: Seq[AddressSet]) => Seq[AddressSet]` combine ranges which are combinable (order as well)

## case class BufferParams
*Parameters used to generate a buffer.*

~~~scala
case class BufferParams(depth: Int, flow: Boolean, pipe: Boolean)
~~~

- **depth** `Int` depth of the buffer.
- **flow** `Boolean` whether to allow combinational bypass when empty.
- **pipe** `Boolean` whether to use a pipeline of registers rather than R/W pointers.
- **latency** `() => Int` get the minimal latency of the buffer.
- **apply** `(DecoupledIO[T]) => DecoupledIO[T]` insert a buffer according to the configuration.

## object BufferParams

- **apply** `(d:Int) => BufferParams(d, false, false)`
- **default** `() => BufferParams(2, false, false)`
- **none** `() => BufferParams(0, false, false)`
- **flow** `() => BufferParams(1, true, false)`
- **pipe** `() => BufferParams(1, false, true)`


<br><br><br><p align="right">
<sub>
Last updated: 18/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
