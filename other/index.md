Class index
========================
***************************

# Coreplex
***************************

#### CoreplexNetwork

`CoreplexNetwork`       [trait](../coreplex/CoreplexNetwork.md#coreplexnetwork      )
`CoreplexNetworkBundle` [trait](../coreplex/CoreplexNetwork.md#coreplexnetworkbundle)
`CoreplexNetworkModule` [trait](../coreplex/CoreplexNetwork.md#coreplexnetworkmodule)

`BankedL2CoherenceManagers`       [trait](../coreplex/CoreplexNetwork.md#bankedl2coherencemanagers      )
`BankedL2CoherenceManagersBundle` [trait](../coreplex/CoreplexNetwork.md#bankedl2coherencemanagersbundle)
`BankedL2CoherenceManagersModule` [trait](../coreplex/CoreplexNetwork.md#bankedl2coherencemanagersmodule)

#### BareCoreplex

`BareCoreplex`       [abstract class](../coreplex/BaseCoreplex.md#abstract-class-barecoreplex      )
`BareCoreplexBundle` [abstract class](../coreplex/BaseCoreplex.md#abstract-class-barecoreplexbundle)
`BareCoreplexModule` [abstract class](../coreplex/BaseCoreplex.md#abstract-class-barecoreplexmodule)

`BaseCoreplex`       [abstract class](../coreplex/BaseCoreplex.md#abstract-class-basecoreplex)
`BaseCoreplexBundle` [class         ](../coreplex/BaseCoreplex.md#class-basecoreplexbundle   )
`BaseCoreplexModule` [class         ](../coreplex/BaseCoreplex.md#class-basecoreplexmodule   )

#### Configs

`BaseCoreplexConfig` [class](../coreplex/Configs.md#class-basecoreplexconfig)

#### RISCVPlatform

`CoreplexRISCVPlatform`       [trait](../coreplex/RISCVPlatform.md#trait-coreplexriscvplatform      )
`CoreplexRISCVPlatformBundle` [trait](../coreplex/RISCVPlatform.md#trait-coreplexriscvplatformbundle)
`CoreplexRISCVPlatformModule` [trait](../coreplex/RISCVPlatform.md#trait-coreplexriscvplatformmodule)

#### RocketTilesplex

`HasRocketTiles`       [trait](../coreplex/RocketCoreplex.md#trait-hasrockettiles      )
`HasRocketTilesBundle` [trait](../coreplex/RocketCoreplex.md#trait-hasrockettilesbundle)
`HasRocketTilesModule` [trait](../coreplex/RocketCoreplex.md#trait-hasrockettilesmodule)

# chip
***************************

#### Configs
`BasePlatformConfig` [class](../chip/Configs.md#class-baseplatformconfig)


# Diplomacy
***************************

#### DeviceTree
`DTS` [object](../diplomacy/DeviceTree.md#object-dts)

#### LazyModule
`LazyModule`    [abstract class](../diplomacy/LazyModule/abstract-class-lazymodule   ),
                [object        ](../diplomacy/LazyModule/object-lazymodule           )
`LazyModuleImp` [abstract class](../diplomacy/LazyModule/abstract-class-lazymoduleimp)

#### Nodes
`NodeHandle`       [case class    ](../diplomacy/Nodes.md#case-class-nodehandle  )
`NodeImp`          [abstract class](../diplomacy/Nodes.md#abstract-class-nodeimp )
`InwardNode`       [trait         ](../diplomacy/Nodes.md#trait-inwardnode       )
`InwardNodeHandle` [trait         ](../diplomacy/Nodes.md#trait-inwardnodehandle )
`InwardNodeImp`    [trait         ](../diplomacy/Nodes.md#trait-inwardnodeimp    )
`OutwardNode`      [trait         ](../diplomacy/Nodes.md#trait-outwardnode      )
`OutwardNodeHandle`[trait         ](../diplomacy/Nodes.md#trait-outwardnodehandle)
`OutwardNodeImp`   [trait         ](../diplomacy/Nodes.md#trait-outwardnodeimp   )

`NodeBinding` [trait      ](../diplomacy/Nodes.md#trait-nodebinding)
`BIND_ONCE`   [case object](../diplomacy/Nodes.md#trait-nodebinding)
`BIND_QUERY`  [case object](../diplomacy/Nodes.md#trait-nodebinding)
`BIND_STAR`   [case object](../diplomacy/Nodes.md#trait-nodebinding)

`BaseNode`  [abstract class](../diplomacy/Nodes.md#abstract-class-basenode )
`MixedNode` [abstract class](../diplomacy/Nodes.md#abstract-class-mixednode)

`MixedAdapterNode` [class](../diplomacy/Nodes.md#class-mixedadapternode)
`AdapterNode`      [class](../diplomacy/Nodes.md#class-adapternode     )

`MixedNexusNode` [class](../diplomacy/Nodes.md#class-mixednexusnode)
`NexusNode`      [class](../diplomacy/Nodes.md#class-nexusnode     )

`SplitterArg`      [case class](../diplomacy/Nodes.md#case-class-splitterarg )
`MixedSplitterNode`[class     ](../diplomacy/Nodes.md#class-mixedsplitternode)
`SplitterNode`     [class     ](../diplomacy/Nodes.md#class-splitternode     )

`IdentityNode` [class](../diplomacy/Nodes.md#class-identitynode)
`InputNode`    [class](../diplomacy/Nodes.md#class-inputnode   )
`OutputNode`   [class](../diplomacy/Nodes.md#class-outputnode  )
`SinkNode`     [class](../diplomacy/Nodes.md#class-sinknode    )
`SourceNode`   [class](../diplomacy/Nodes.md#class-sourcenode  )

#### Parameters

`AddressRange`  [case class](../diplomacy/Parameters.md#case-class-addressrange ),
                [object    ](../diplomacy/Parameters.md#object-addressrange     )
`AddressSet`    [case class](../diplomacy/Parameters.md#case-class-addressset   ),
                [object    ](../diplomacy/Parameters.md#object-addressset       )
`BufferParams`  [case class](../diplomacy/Parameters.md#case-class-bufferparams ),
                [object    ](../diplomacy/Parameters.md#object-bufferparams     )
`IdRange`       [case class](../diplomacy/Parameters.md#case-class-idrange      )
`RegionType`    [object    ](../diplomacy/Parameters.md#object-regiontype       )
`TransferSizes` [case class](../diplomacy/Parameters.md#case-class-transfersizes)

#### Resources
`Binding`          [case class    ](../diplomacy/Resources.md#case-class-binding    )
`BindingScope`     [trait         ](../diplomacy/Resources.md#trait-bindingscope    ),
                   [object        ](../diplomacy/Resources.md#object-bindingscope   )
`Description`      [case class    ](../diplomacy/Resources.md#case-class-description)
`Device`           [abstract class](../diplomacy/Resources.md#abstract-class-device )
`DeviceInterrupts` [trait         ](../diplomacy/Resources.md#trait-deviceinterrupts)
`DeviceRegName`    [trait         ](../diplomacy/Resources.md#trait-deviceregname   )
`MemoryDevice`     [class         ](../diplomacy/Resources.md#class-memorydevice    )
`SimpleDevice`     [class         ](../diplomacy/Resources.md#class-simpledevice    )

`Resource`           [case class      ](../diplomacy/Resources.md#case-class-resource           )
`ResourcePermissions`[case calss      ](../diplomacy/Resources.md#case-class-resourcepermissions)
`ResourceAddress`    [final case class](../diplomacy/Resources.md#case-class-resourceaddress    )
`ResourceInt`        [final case class](../diplomacy/Resources.md#case-class-resourceint        )
`ResourceMapping`    [final case class](../diplomacy/Resources.md#case-class-resourcemapping    )
`ResourceMap`        [final case class](../diplomacy/Resources.md#case-class-resourcemap        )
`ResourceReference`  [final case class](../diplomacy/Resources.md#case-class-resourcereference  )
`ResourceString`     [final case class](../diplomacy/Resources.md#case-class-resourcestring     )

`ResourceBinding`    [object    ](../diplomacy/Resources.md#object-resourcebindings     )
`ResourceBindings`   [case class](../diplomacy/Resources.md#case-class-resourcebindings )

# Regmapper
***************************

#### RegisterCrossing
`BusyRegisterCrossing`  [class](../regmapper/RegisterCrossing.md#class-busyregistercrossing )
`RegisterWriteCrossing` [class](../regmapper/RegisterCrossing.md#class-registerwritecrossing)

# Rocket
***************************

#### ALU
`ALU` [class](../rocket/ALU.md#class-alu)

#### BTB
`BHT` [class](../rocket/BTB.md#class-bht)
`BTB` [class](../rocket/BTB.md#class-btb)
`RAS` [class](../rocket/BTB.md#class-ras)

#### Breakpoint
`BPControl`      [class](../rocket/Breakpoint.md#class-bpcontrol     )
`BreakpointUnit` [class](../rocket/Breakpoint.md#class-breakpointunit)

#### HellaCacheArbiter
`HellaCacheArbiter` [class](../rocket/HellaCacheArbiter.md#class-hellacachearbiter)

#### HellaCache
`DCacheParams`        [case class](../rocket/HellaCache.md#case-class-dcacheparams  )
`HasHellaCache`       [trait     ](../rocket/HellaCache.md#trait-hashellacache      )
`HasHellaCacheBundle` [trait     ](../rocket/HellaCache.md#trait-hashellacachebundle)
`HasHellaCacheModule` [trait     ](../rocket/HellaCache.md#trait-hashellacachemodule)
`HellaCache`          [class     ](../rocket/HellaCache.md#class-hellacache         ),
                      [object    ](../rocket/HellaCache.md#object-hellacache        )
`HellaCacheBundle`    [class     ](../rocket/HellaCache.md#class-hellacachebundle   )
`HellaCacheIO`        [class     ](../rocket/HellaCache.md#class-hellacacheio       )
`HellaCacheModule`    [class     ](../rocket/HellaCache.md#class-hellacachemodule   )
`L1Metadata`          [class     ](../rocket/HellaCache.md#class-l1metadata         )

#### IBuf
`IBuf`        [class](../rocket/IBuf.md#class-ibuf       )
`Instruction` [class](../rocket/IBuf.md#class-instruction)

#### RVC
`ExpandedInstruction` [class](../rocket/RVC.md#class-expandedinstruction)
`RVCExpander`         [class](../rocket/RVC.md#class-rvcexpander        )

# Tile
***************************

#### BaseTile

`BareTile`          [abstract class](../tile/BaseTile.md#abstract-class-baretile      )
`BareTileBundle`    [abstract class](../tile/BaseTile.md#abstract-class-baretilebundle)
`BareTileModule`    [abstract class](../tile/BaseTile.md#abstract-class-baretilemodule)

`BaseTile`          [abstract class](../tile/BaseTile.md#abstract-class-basetile      )
`BaseTileBundle`    [class         ](../tile/BaseTile.md#abstract-class-basetilebundle)
`BaseTileModule`    [class         ](../tile/BaseTile.md#abstract-class-basetilemodule)

`HasExternallyDrivenTileConstants` [trait](../tile/BaseTile.md#trait-hasexternallydriventileconstants)
`HasTileLinkMasterPort`            [trait](../tile/BaseTile.md#trait-hastilelinkmasterport           )
`HasTileLinkMasterPortBundle`      [trait](../tile/BaseTile.md#trait-hastilelinkmasterportbundle     )
`HasTileLinkMasterPortModule`      [trait](../tile/BaseTile.md#trait-hastilelinkmasterportmodule     )



#### Interrupts

`TileInterrupts`              [class](../tile/Interrupts.md#class-tileinterrupts             )
`HasExternalInterrupts`       [trait](../tile/Interrupts.md#trait-hasexternalinterrupts      )
`HasExternalInterruptsModule` [trait](../tile/Interrupts.md#trait-hasexternalinterruptsmodule)

#### RocketTile

`RocketTileParams` [case class](../tile/RocketTile.md#case-class-rockettileparams)
`RocketTile`       [class     ](../tile/RocketTile.md#class-rockettile           )
`RocketTileBundle` [class     ](../tile/RocketTile.md#class-rockettilebundle     )


# Tilelink
***************************

#### Arbiters
`TLArbiter` [object](../tilelink/Arbiter.md#object-tlarbiter)

#### Buffer
`TLBuffer` [class ](../tilelink/Buffer.md#class-tlbuffer ),
           [object](../tilelink/Buffer.md#object-tlbuffer)

#### Bundles
`TLMessages`    [object](../tilelink/Bundles.md#object-tlmessages   )
`TLAtomics`     [object](../tilelink/Bundles.md#object-tlatomics    )
`TLHints`       [object](../tilelink/Bundles.md#object-tlhints      )
`TLPermissions` [object](../tilelink/Bundles.md#object-tlpermissions)

`TLBundleA` [final class](../tilelink/Bundles.md#final-class-tlbundleabcde)
`TLBundleB` [final class](../tilelink/Bundles.md#final-class-tlbundleabcde)
`TLBundleC` [final class](../tilelink/Bundles.md#final-class-tlbundleabcde)
`TLBundleD` [final class](../tilelink/Bundles.md#final-class-tlbundleabcde)
`TLBundleE` [final class](../tilelink/Bundles.md#final-class-tlbundleabcde)
`TLBundle`  [class      ](../tilelink/Bundles.md#class-tlbundle           ),
            [object     ](../tilelink/Bundles.md#object-tlbundle          )

`TLBundleSnoop`    [class ](../tilelink/Bundles.md#class-tlbundlesnoop   ),
                   [object](../tilelink/Bundles.md#object-tlbundlesnoop  )
`TLAsyncBundle`    [class ](../tilelink/Bundles.md#class-tlasyncbundle   )
`TLRationalBundle` [class ](../tilelink/Bundles.md#class-tlrationalbundle)

#### Edges
`TLEdge`    [class](../tilelink/Edges.md#class-tledge   )
`TLEdgeIn`  [class](../tilelink/Edges.md#class-tledgein )
`TLEdgeOut` [class](../tilelink/Edges.md#class-tledgeout)

#### FIFOFixer
`TLFIFOFixer` [class ](../tilelink/FIFOFixer.md#class-tlfifofixer ),
              [object](../tilelink/FIFOFixer.md#object-tlfifofixer)

#### IntNodes
`IntRange` [case class](../tilelink/IntNodes.md#case-class-intrange),
           [object    ](../tilelink/IntNodes.md#object-intrange    )

`IntSinkParameters`     [case class](../tilelink/IntNodes.md#case-class-intsinkparameters    )
`IntSinkPortParameters` [case class](../tilelink/IntNodes.md#case-class-intsinkportparameters)
`IntSinkPortSimple`     [object    ](../tilelink/IntNodes.md#object-intsinkportsimple        )

`IntSourceParameters`     [case class](../tilelink/IntNodes.md#case-class-intsourceparameters    )
`IntSourcePortParameters` [case class](../tilelink/IntNodes.md#case-class-intsourceportparameters)
`IntSourcePortSimple`     [object    ](../tilelink/IntNodes.md#object-intsourceportsimple        )

`IntIdentityNode`       [case class](../tilelink/IntNodes.md#interrupt-extension-of-basic-nodes)
`IntSourceNode`         [case class](../tilelink/IntNodes.md#interrupt-extension-of-basic-nodes)
`IntSinkNode`           [case class](../tilelink/IntNodes.md#interrupt-extension-of-basic-nodes)
`IntNexusNode`          [case class](../tilelink/IntNodes.md#interrupt-extension-of-basic-nodes)
`IntOutputNode`         [case class](../tilelink/IntNodes.md#interrupt-extension-of-basic-nodes)
`IntInputNode`          [case class](../tilelink/IntNodes.md#interrupt-extension-of-basic-nodes)
`IntBlindOutputNode`    [case class](../tilelink/IntNodes.md#interrupt-extension-of-basic-nodes)
`IntBlindInputNode`     [case class](../tilelink/IntNodes.md#interrupt-extension-of-basic-nodes)
`IntInternalOutputNode` [case class](../tilelink/IntNodes.md#interrupt-extension-of-basic-nodes)
`IntInternalInputNode`  [case class](../tilelink/IntNodes.md#interrupt-extension-of-basic-nodes)

`IntXbar` [class](../tilelink/IntNodes.md#class-intxbar)
`IntXing` [class](../tilelink/IntNodes.md#class-intxing)

#### Nodes
`TLImp`                [object    ](../tilelink/Nodes.md#object-tlimp                     )
`TLAdapterNode`        [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)
`TLBlindInputNode`     [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)
`TLBlindOutputNode`    [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)
`TLClientNode`         [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes),
                       [object    ](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)
`TLInputNode`          [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)
`TLIdentityNode`       [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)
`TLInternalInputNode`  [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)
`TLInternalOutputNode` [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)
`TLManagerNode`        [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes),
                       [object    ](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)
`TLNexusNode`          [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)
`TLOutputNode`         [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)

`TLAsyncImp`          [object](../tilelink/Nodes.md#object-tlasyncimp                                    )
`TLAsyncIdentityNode` [object](../tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)
`TLAsyncInputNode`    [object](../tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)
`TLAsyncOutputNode`   [object](../tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)
`TLAsyncSinkNode`     [object](../tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)
`TLAsyncSourceNode`   [object](../tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)

`TLRationalImp`          [object](../tilelink/Nodes.md#object-tlrationalimp                             )
`TLRationalIdentityNode` [object](../tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)
`TLRationalInputNode`    [object](../tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)
`TLRationalOutputNode`   [object](../tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)
`TLRationalSinkNode`     [object](../tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)
`TLRationalSourceNode`   [object](../tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)

#### Splitter
`TLSplitter` [class](../tilelink/Splitter.md#class-tlsplitter)

#### Xbar
`TLXbar` [class ](../tilelink/Xbar.md#class-tlxbar ),
         [object](../tilelink/Xbar.md#object-tlxbar)

# util
***************************

#### AsyncBundle
`AsyncBundle`     [final class](../util/AsyncBundle.md#final-class-asyncbundle)
`FromAsyncBundle` [object     ](../util/AsyncBundle.md#object-fromasyncbundle )
`ToAsyncBundle`   [object     ](../util/AsyncBundle.md#object-toasyncbundle   )

#### AsyncQueue
`AsyncQueue`       [class ](../util/AsyncQueue.md#class-asyncqueue      )
`AsyncQueueSink`   [class ](../util/AsyncQueue.md#class-asyncqueuesink  )
`AsyncQueueSource` [class ](../util/AsyncQueue.md#class-asyncqueuesource)
`AsyncValidSync`   [class ](../util/AsyncQueue.md#class-asyncvalidsync  )
`GrayCounter`      [object](../util/AsyncQueue.md#object-graycounter    )
`UIntSyncChain`    [object](../util/AsyncQueue.md#object-uintsyncchain  )


#### Arbiters
`HellaCountingArbiter` [class](../util/Arbiters.md#class-hellacountingarbiter)
`HellaPeekingArbiter`  [class](../util/Arbiters.md#class-hellapeekingarbiter )

#### BackBoxRegs
`AsyncResetReg`    [class ](../util/BackBoxRegs.md#class-asyncresetreg   ),
                   [object](../util/BackBoxRegs.md#object-asyncresetreg  )
`AsyncResetRegVec` [class ](../util/BackBoxRegs.md#class-asyncresetregvec)

#### ClockDivider
`ClockDivider2`    [class](../util/ClockDivider.md#class-clockdivider2    )
`Pow2ClockDivider` [class](../util/ClockDivider.md#class-pow2clockdivider2)

#### Counters
`TwoWayCounter`    [object    ](../util/Counters.md#object-twowaycounter  )
`WideCounter`      [case class](../util/Counters.md#case-class-widecounter)

#### Crossing
`Crossing`         [abstract class](../util/Crossing.md#abstract-class-crossing)
`CrossingIO`       [class         ](../util/Crossing.md#class-crossingio       )


<br><br><br><p align="right">
<sub>
Last updated: 25/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
