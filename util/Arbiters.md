**Utilizing the Chisel2 compatability layer**

abstract class HellaLockingArbiter
----------------------
    abstract class HellaLockingArbiter[T <: Data](typ: T, arbN: Int, rr: Boolean = false) extends Module

*A generalized locking RR arbiter that addresses the limitations of the version in the Chisel standard library.*

class HellaPeekingArbiter
----------------------
    class HellaPeekingArbiter[T <: Data](
        typ: T, arbN: Int,
        canUnlock: T => Bool,
        needsLock: Option[T => Bool] = None,
        rr: Boolean = false)
      extends HellaLockingArbiter(typ, arbN, rr)

*A arbiter support bursts of variable length.*

+ *typ: T*: Data type.
+ *arbN: Int*: Number of ports.
+ *canUnlock: T => Bool*: function to detect tail.
+ *needsLock: Option[T => Bool]*: function to detect burst.
+ *rr: Boolean*: whether to use round-robin schedule (static priority by default).
+ **IO**
  + *in: Vec(arbN, Decoupled(typ.cloneType)).flip*: input ports
  + *out: Decoupled(typ.cloneType)*: output port

class HellaCountingArbiter
-----------------------
    class HellaCountingArbiter[T <: Data](
        typ: T, arbN: Int, count: Int,
        val needsLock: Option[T => Bool] = None,
        rr: Boolean = false)
      extends HellaLockingArbiter(typ, arbN, rr)

*A arbiter support bursts of constant length.*

+ *typ: T*: Data type.
+ *arbN: Int*: Number of ports.
+ *count: Int*: number of beats in a burst.
+ *needsLock: Option[T => Bool]*: function to detect burst.
+ *rr: Boolean*: whether to use round-robin schedule (static priority by default).
+ **IO**
  + *in: Vec(arbN, Decoupled(typ.cloneType)).flip*: input ports
  + *out: Decoupled(typ.cloneType)*: output port
