[Rocket](../../Readme.md)/[uncore](../../uncore.md)/[tilelink2](../tilelink2.md)/[Package](https://github.com/ucb-bar/rocket-chip/blob/master/src/main/scala/uncore/tilelink2/package.scala)
=====================

*Helper variables and functions for TileLink*

**********************

Types
------------

+ **TLInwardNode** `type InwardNodeHandle[TLClientPortParameters, TLManagerPortParameters, TLBundle]`
+ **TLOutwardNode** `type OutwardNodeHandle[TLClientPortParameters, TLManagerPortParameters, TLBundle]`
+ **TLAsyncOutwardNode** `type OutwardNodeHandle[TLAsyncClientPortParameters, TLAsyncManagerPortParameters, TLAsyncBundle]`
+ **TLRationalOutwardNode** `type OutwardNodeHandle[TLRationalClientPortParameters, TLRationalManagerPortParameters, TLRationalBundle]`
+ **IntOutwardNode** `type OutwardNodeHandle[IntSourcePortParameters, IntSinkPortParameters, Vec[Bool]]`

Functions
--------------

+ **OH1ToOH** `(UInt) => UInt`  Mask to one-hot. `('b00_0111) => 'b000_1000`
+ **OH1ToUInt** `(UInt) => UInt` Mask to integer. `('b00_0111) => 3`
+ **UIntToOH1** `(UInt, Int) => UInt` Integer to mask. `(3, 8) => 'b0000_0111`
+ **trailingZeros** `(Int) => Option[Int]` Number of zero LSBs. `('b0110_1000) => Some(3)`
+ **leftOR** `(UInt) => UInt` Or bits from right to left. `('b0110_1000) => 'b1111_1000`
+ **rightOR** `(UInt) => UInt` Or bits from left to right. `('b0110_1000) => 'b0111_1111`
+ **maskGen** `(addr:UInt, lgSize:UInt, beatBytes:Int) => UInt`

    Generate byte mask in AXI style:
    + `maskGen(3, 3, 16) => 'b0000_0000_1111_1111` 8B transaction on 16B bus with address 3
    + `maskGen(5, 2, 8) => 'b1111_0000` 4B transaction on 8B bus with address 5
    + `maskGen(1, 0, 8) => 'b0000_0010` 1B transaction on 8B bus with address 1


<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 30/03/2017</sub></p>

