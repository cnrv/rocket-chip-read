[Rocket](../Readme.md)/[diplomacy](../diplomacy.md)/[Parameters](https://github.com/ucb-bar/rocket-chip/blob/master/src/main/scala/diplomacy/Parameters.scala)
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

case class IdRange(start: Int, end: Int)
----------------------
*A non-empty half-open range* `[start, end)`

    0 <= start < end

+ *operator <*: strict partial order (lhs.end &le; rhs.start)
+ *operator >*: strict partial order (lhs.start > rhs.end)
+ *overlaps: (x: IdRange) => Boolean*: this &cap; x &ne; &empty;
+ *contains: (x: IdRange) => Boolean*: this &supe; x
+ *contains: (x: Int) => Boolean*: x &isin; this
+ *contains: (x: UInt) => Bool*: x &isin; this
+ *shift: (x: Int) => IdRange*: shift range by positive x
+ *size: _ => Int*: size of range
+ *range: _ => Range*: iterate

case class TransferSizes(min: Int, max: Int)
--------------------------
*An potentially empty inclusive range of 2-powers* `[min, max]`

    0 <= min <= max && isPow2(max) && isPow2(min) && (max == 0 || min != 0)

+ *none: _ => Boolean*: is empty
+ *contains: (x: Int) => Boolean*: `isPow(x)` && x &isin; this
+ *contains: (x: TransferSizes) => Boolean*: this &supe; x
+ *containsLg: (x: Int) => Boolean*: (1 << x) &isin; this
+ *containsLg: (x: UInt) => Bool*: (1.U << x) &isin; this
+ *intersect: (x: TransferSizes) => TransferSizes*: this &cap; x

case class AddressRange(base: BigInt, size: BigInt)
---------------------------
    case class AddressRange(base: BigInt, size: BigInt) extends Ordered[AddressRange]

*An address range expression*

+ *end: BigInt = base + size*: end of the address range.
+ *compare: AddressRange => Boolean*: compare two ranges.
+ *operator <: AddressRange => Boolean*: derived from Ordered[AddressRange]
+ *operator >: AddressRange => Boolean*: derived from Ordered[AddressRange]
+ *operator <=: AddressRange => Boolean*: derived from Ordered[AddressRange]
+ *operator >=: AddressRange => Boolean*: derived from Ordered[AddressRange]
+ *contains: (x: AddressRange) => Boolean*: this &supe; x
+ *union: (x: AddressRange) => Some[AddressRange]*: this &cup; x

object AddressRange
----------------------------
+ *fromSets: (seq: Seq[AddressSet]) => Seq[AddressRange]*: convert AddressSet to unified AddressRange
+ *unify: (seq: Seq[AddressRange]) => Seq[AddressRange]*: combine ranges which are combinable (order as well)

case class AddressSet(base: BigInt, mask: BigInt)
----------------------------
    case class AddressSet(base: BigInt, mask: BigInt) extends Ordered[AddressSet]

*AddressSets specify the address space managed by the manager*<br>
*Base is the base address, and mask are the bits consumed by the manager*<br>
*e.g: base=0x200, mask=0xff describes a device managing 0x200-0x2ff*<br>
*e.g: base=0x1000, mask=0xf0f decribes a device managing 0x1000-0x100f, 0x1100-0x110f, ...*<br>

+ *compare: AddressSet => Boolean*: compare two ranges.
+ *operator <: AddressSet => Boolean*: derived from Ordered[AddressSet]
+ *operator >: AddressSet => Boolean*: derived from Ordered[AddressSet]
+ *operator <=: AddressSet => Boolean*: derived from Ordered[AddressSet]
+ *operator >=: AddressSet => Boolean*: derived from Ordered[AddressSet]
+ *contains: (x: BigInt) => Boolean*: x &isin; this
+ *contains: (x: UInt) => Boolean*: x &isin; this
+ *contains: (x: AddressSet) => Boolean*: x &supe; this
+ *overlaps: (x: AddressSet) => Boolean*: this &cap; x &ne; &empty;
+ *intersect: (x: AddressSet) => Some[AddressSet]*: this &cap; x
+ *alignment: _ => BigInt*: get the minimal alignment (mask: 0x0000ffff => 0x00010000)
+ *contiguous: _ => Boolean*: whether the address space is contiguous(mask: 0x0000ffff => true, mask:0x0000ff0f => false)
+ *finite: _ => Boolean*: mask &ge; 0 ??
+ *max: _ => BigInt*: the address upper bound
+ *widen: (imask: BitInt) => AddressSet*: get a larger space using imask
+ *toString: _ => String*: convert to string
+ *toRange: _ => AddressRange*: convert to AddressRange

object AddressSet
----------------------------
+ *misaligned: (BigInt, BigInt, Seq[AddressSet]) => Seq[AddressSet]*: ?? not used
+ *unify: (seq: Seq[AddressSet]) => Seq[AddressSet]*: combine ranges which are combinable (order as well)




**********************

```scala
last modified = 12/03/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
