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
+ *contains: (x: IdRange) => Boolean*: this &sup; x
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
+ *contains: (x: TransferSizes) => Boolean*: this &sup; x
+ *containsLg: (x: Int) => Boolean*: (1 << x) &isin; this
+ *containsLg: (x: UInt) => Bool*: (1.U << x) &isin; this
+ *intersect: (x: TransferSizes) => TransferSizes*: this &cap; x
