[Rocket](../Readme.md)/[regmapper](../regmapper.md)/[RegMapper](https://github.com/freechipsproject/rocket-chip/tree/master/src/main/scala/regmapper/RegMapper.scala)
========================
*A bus agnostic register interface to a register-based device*

**********************

### case class RegMapperParams
*Parameters used by RegMappers.*

~~~scala
case class RegMapperParams(indexBits: Int, maskBits: Int, extraBits: Int)
~~~

+ **indexBits** `Int` (param) bit size of the index field.
+ **maskBits** `Int` (param) bit size of the byte mask.
+ **extraBits** `Int` (param) bit size of the extra field.


### class RegMapperInput
*Read/write request*

~~~scala
class RegMapperInput(params: RegMapperParams) extends GenericParameterizedBundle(params)
~~~

+ **read** `Bool` whether it is a read request.
+ **index** `UInt` index (address offset) of the register word.
+ **data** `UInt` write data.
+ **mask** `UInt` write byte mask.
+ **extra** `UInt` extra information attached to the request. For `TLRegisterNode`, it is `{sourceId, lgSize}`.

### class RegMapperOutput
*Read/write response*

~~~scala
class RegMapperOutput(params: RegMapperParams) extends GenericParameterizedBundle(params)
~~~

+ **read** `Bool` whether it is responding to a read request.
+ **data** `UInt` read data.
+ **extra** `UInt` the extra information originally attached with the request.

### object RegMapper
*Create a generic register-based device*

+ **apply** `(bytes: Int, concurrency: Int, undefZero: Boolean, in: DecoupledIO[RegMapperInput], mapping: RegField.Map*) => DecoupledIO[RegMapperOutput]`
  - **bytes** the byte size of a word in the register device.
  - **concurrency** the max number of concurrent transactions.
  - **undefZero** whether to set zero to undefined fields.
  - **in** the input request channel.
  - **mapping** the collective set of register (byte) definitions.

Internal variabls inside `apply()`:

+ **bytemap** `Seq[byteAddr:Int => Seq[bitFields:RegField]]` the collective set of register (byte) definitions.
+ **bitmap** `Seq[bitAddr:Int => bitField:RegField]` flattened bit address to bitfield mapping.
+ **wordmap** `Seq[wordAddr:Int => Seq[bitAddr:Int => bitField:RegField]]` group bit mappings by words.
+ **inParams** `RegMapperParams` the RegField parameter.
+ **out** `DecoupledIO[RegMapperOutput]`
+ **front** `DecoupledIO[RegMapperInput]`
+ **pipelined** `Boolean` whether any of the bitfield require pipelined control (`in.ready` does not depend on `out.ready`).
+ **depth** `Int` the depth of control (delay in response, also the number of concurrent transactions).
+ **back** `DecoupledIO[RegMapperInput]` queue `front` for `depth` cycle.
+ **toBits** `(x:Int, tail:List[Boolean]) => List[Boolean]` convert `x` to a list of Boolean, the argument `tail` is for internal recursive calls only.
+ **ofBits** `(List[Boolean]) => Int` convert a list of Boolean to an Int.
+ **mask** `BigInt` the minimal mask that can decide the register map.
+ **maskFilter** `toBits(mask)`
+ **maskBits** `Int` the number of 1s in `mask`.
+ **regSize** `1<<maskBits` the maximal number of register words.
+ **regIndexI** `(Int) => Int` shrink the 0s and get the index of the register word.
+ **regIndexU** `(UInt) => UInt` shrink the 0s and get the index of the register word.
+ **flat** `Seq[index:Int, bitAddrOffset:Int, RegField]` flatten the register file into (shrinked index, offset in word, bit field).
+ **rivalid** `Vec[Bool]` input read valid for each flattened bit-field.
+ **wivalid** `Vec[Bool]` input write valid for each flattened bit-field.
+ **roready** `Vec[Bool]` output read ready for each flattened bit-field.
+ **woready** `Vec[Bool]` output write ready for each flattened bit-field.
+ **frontMask** `UInt` expand `front.bits.mask` from byte mask to bit mask.
+ **backMask** `UInt` expand `back.bits.mask` from byte mask to bit mask.

<br><br><br><p align="right">
<sub>
Last updated: 22/09/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>

