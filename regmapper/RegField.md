[Rocket](../Readme.md)/[regmapper](../regmapper.md)/[RegField](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/regmapper/RegField.scala)
========================
*Generic definitions for registers.*

**********************

### case class RegReadFn
*define a register read function.*

~~~scala
case class RegReadFn private(combinational: Boolean, fn: (Bool, Bool) => (Bool, Bool, UInt))
~~~

+ **combinational** `Boolean` whether to allow `in.ready` depending on `out.ready`
+ **fn** `(in.valid:Bool, out.ready:Bool) => (in.ready:Bool, out.valid:Bool, data:UInt)` the read function.

### object RegReadFn
*RegReadFn generator.*

+ **apply** `((Bool, Bool) => (Bool, Bool, UInt)) => RegReadFn` (implicit) direct function definition.
+ **apply** `((out.ready) => (out.valid, data:UInt)) => RegReadFn` (implicit) simplified function definition.
+ **apply** `(RegisterReadIO[UInt]) => RegReadFn` (implicit) convert a `RegisterReadIO` to a read function.
+ **apply** `(ReadyValidIO[UInt]) => RegReadFn` (implicit) convert a `ReadyValidIO` to a read function.
+ **apply** `(UInt) => RegReadFn` (implicit) read from a register.
+ **apply** `(Unit) => RegReadFn` (implicit) get always 0 read function.

### case class RegWriteFn
*define a register write function.*

~~~scala
case class RegWriteFn private(combinational: Boolean, fn: (Bool, Bool, UInt) => (Bool, Bool))
~~~

+ **combinational** `Boolean` whether to allow `in.ready` depending on `out.ready`
+ **fn** `(in.valid:Bool, out.ready:Bool, data:UInt) => (in.ready:Bool, out.valid:Bool)` the write function.

### object RegWriteFn
*RegWriteFn generator.*

+ **apply** `((Bool, Bool, UInt) => (Bool, Bool)) => RegWriteFn` (implicit) direct function definition.
+ **apply** `((out.ready, data:UInt) => (out.valid)) => RegWriteFn` (implicit) simplified function definition.
+ **apply** `(RegisterWriteIO[UInt]) => RegWriteFn` (implicit) convert a `RegisterWriteIO` to a write function.
+ **apply** `(DecoupledIO[UInt]) => RegWriteFn` (implicit) convert a `DecoupledIO` to a write function.
+ **apply** `(UInt) => RegWriteFn` (implicit) write to a register.
+ **apply** `(Unit) => RegWriteFn` (implicit) get always ready write function but actually write nothing.

### case class RegField
*A generic register.*

~~~scala
case class RegField(width: Int, read: RegReadFn, write: RegWriteFn, name: String, description: String)
~~~

+ **width** `Int` the bit width of the register.
+ **read** `RegReadFn` the read function.
+ **write** `RegWriteFn` the write function.
+ **name** `String` the name of the register.
+ **description** `String` the description of the register.
+ **pipelined** `() => Boolean` `in.ready` does not depend on `out.ready` for either read or write or both.
+ **readOnly** `() => RegField` get a read only version of this register.

### object RegField
*Register generator*

+ **Map** `(Int => Seq[RegField])` (type) Register field definition: byte address => sequence of bit fields
+ **apply** `(n:Int) => RegField` get a dummy n bit wide register.
+ **apply** `(Int, RegReadFn, RegWriteFn) => RegField` get an annonymas register.
+ **apply** `(Int, rw: UInt) => RegField` get a plain register (set `rw` to a `Reg`).
+ **apply** `(Int, UInt, String, String) => RegField` get a named register.
+ **apply** `(Int, RegReadFn, String, String) => RegField` get a named readonly register.
+ **apply** `(Int, RegWriteFn, String, String) => RegField` get a named writeonly register.
+ **w1ToClear** `(Int, UInt, String, set: UInt) => RegField` get a register that has a always 1 set of bits defined by `set` and when writing 1 to an unset bit clears it.
+ **rwReg** `(Int, SimpleRegIO) => RegField` wrap a blackbox register into a RW register.
+ **bytes** `(reg: UInt, numBytes: Int) => Seq[RegField]`
  Create byte-sized read-write RegFields out of a large UInt register.
  It is updated when any of the bytes are written. Because the RegFields
  are all byte-sized, this is also suitable when a register is larger
  than the intended bus width of the device (atomic updates are impossible).

### trait HasRegMap
*A trait extended by Module implementations to define the register file and the interrupts.*

+ **regmap** `(mapping: RegField.Map*) => Unit`
+ **interrupts** `Vec[Bool]`



<br><br><br><p align="right">
<sub>
Last updated: 25/09/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
