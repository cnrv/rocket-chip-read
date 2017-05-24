[Rocket](../Readme.md)/[rocket](../rocket.md)/[HellaCache](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/rocket/HellaCache.scala)
========================
*Base module of caches.*

*****************

+ [Definitions](#definitions)
+ [Base for L1 data caches](#base-for-l1-data-caches)
+ [Traits for Tiles](#traits-for-tiles)

*****************
Definitions
-------------------------

### case class DCacheParams
*Parameters of a cache module.*

+ **nSets** `Int` Number of sets.
+ **nWays** `Int` Number of ways.
+ **rowBits** `Int` Number of bits of a row in memory (also the data width of a Tilelink beat).
+ **nTLBEntries** `Int` Number of TLB entries.
+ **tagECC** `Code` The encoding method used for tag ECC.
+ **dataECC** `Code` The encoding method used for data ECC.
+ **nMSHRs** `Int` Number of missing handlers for cacheable data.
+ **nSDQ** `Int` Number of entries in the store data queue (an optimisation used to reduce the size of request sent to MSHRs).
+ **nRPQ** `Int` Number of entries in the replay queue (used to merge accesses to the same missing cache line).
+ **nMMIOs** `Int` The maximal number of in-flight MMIO (uncached) accesses.
+ **blockBytes** `Int` Size of a cache line.
+ **scratch** `Option[BigInt]` The base address of the scratch pad (None to disable scratch pad).

### class HellaCacheIO
*Base class of the cache IO bundle between cache and processors.*

+ I/O, type and parameters

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| p                      | Parameters       | param      | configuration                         |
| req                    | DecoupledIO[HellaCacheReq] | O | cache request to cache               |
| s1\_kill               | Bool             | O          | kill the previous cycle's request     |
| s1\_data               | HellaCacheWriteData | O       | store data for the previous cycle's request |
| resp                   | ValidIO[HellaCacheResp] | I   | response from cache                   |
| replay\_next           | Bool             | I          | replay the next instruction           |
| s2\_xcpt               | HellaCacheExceptions | I      | exceptions from cache                 |
| invalidate\_lr         | Bool             | O          | reset the lr counter (wb xcpt)        |
| ordered                | Bool             | I          | load/store fence is enforced          |
| perf                   | HellaCachePerfEvents | I      | collection performance events         |

### class L1Metadata
*Base for metadata entry*

+ **coh** `ClientMetadata` The actual metadata of each cache line.
+ **tag** `UInt` Address tag.

### class L1MetadataArray
*L1 metadata array*

~~~scala
class L1MetadataArray[T <: L1Metadata](onReset: () => T)(implicit p: Parameters)
    extends L1HellaCacheModule()(p)
~~~

+ I/O, type and parameters

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| T                      | <: L1Metadata    | type       | the metadata class type               |
| onReset                | () => T          | param      | reset function for metadata           |
| p                      | Parameters       | param      | configuration                         |
| read                   | DecoupledIO[L1MetaReadReq] | I | read request                         |
| write                  | DecoupledIO[L1MetaWriteReq] | O | write request                       |
| resp                   | Vec[T]           | O          | read response from all ways           |


Base for L1 data caches
------------------------

### class HellaCache

~~~scala
abstract class HellaCache(implicit p: Parameters) extends LazyModule
~~~

+ Note: it is either a scratch pad or a cache.

### class HellaCacheBundle

~~~scala
class HellaCacheBundle(outer: HellaCache)(implicit p: Parameters) extends CoreBundle()(p)
~~~

+ I/O, type and parameters

| name                   | type             | direction  | description                           |
| :---                   | :--:             | :--:       | :---                                  |
| outer                  | HellaCache       | param      | pointer to the parent LazyModule      |
| p                      | Parameters       | param      | configuration                         |
| hartid                 | UInt             | I          | hart identifier                       |
| cpu                    | HellaCacheIO     | I          | channel with processors               |
| ptw                    | TLBPTWIO         | O          | channel for page table walk           |
| mem                    | HeterogeneousBag[TLBundle] | O | the channels to L2/IO                |

### class HellaCacheModule

~~~scala
class HellaCacheModule(outer: HellaCache) extends LazyModuleImp(outer)
    with HasL1HellaCacheParameters
~~~

### object HellaCache
*L1 cache generator function*

+ **apply** `(blocking:Boolean, scratch: () => Option[AAddressSet]) => LazyModule[HellaCacheModule]`
  + *blocking* generate a blocking cache or a scratch pad; otherwise, a non-blocing cache.
  + *scratch* the base address of the scratch pad.


Traits for Tiles
-----------------------------

### trait HasHelaCache

~~~scala
trait HasHellaCache extends HasTileLinkMasterPort with HasTileParameters
~~~

+ **module** `HasHellaCacheModule`
+ **implicit p** `Parameters` Tile has its own parameter object.
+ **dcache** `LazyModule[HellaCacheModule]`

### trait HasHellaCacheBundle

~~~scala
trait HasHellaCacheBundle extends HasTileLinkMasterPortBundle
~~~

### trait HasHellaCacheModule

~~~scala
trait HasHellaCacheModule extends HasTileLinkMasterPortModule
~~~

+ **dcachePorts** `ListBuffer[HellaCacheIO]` Dynamic built cache requesting channels.
+ **dcacheArb** `Module[HellaCacheArbiter]` The cahnnel arbiter.



<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 24/05/2017</sub></p>
