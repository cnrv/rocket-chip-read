Class index
========================
***************************

+ ALU<br>
  rocket.ALU [class](../rocket/ALU.md#class-alu)

+ Arbiters<br>
  rocket.HellaCacheArbiter [class](../rocket/HellaCacheArbiter.md#class-hellacachearbiter)<br>
  util.HellaCountingArbiter [class](../util/Arbiters.md#class-hellacountingarbiter)<br>
  util.HellaPeekingArbiter [class](../util/Arbiters.md#class-hellapeekingarbiter)<br>
  devices.tilelink.TLArbiter [object](../devices/tilelink/Arbiter.md#object-tlarbiter)<br>

+ Binding<br>
  diplomacy.Binding [case class](../diplomacy/Resources.md#case-class-binding)<br>
  diplomacy.BindingScope [trait](../diplomacy/Resources.md#trait-bindingscope); [object](../diplomacy/Resources.md#object-bindingscope)<br>

+ Blackbox<br>
  util.AsyncResetReg [class](../util/BackBoxRegs.md#class-asyncresetreg); [object](../util/BackBoxRegs.md#object-asyncresetreg)<br>
  util.AsyncResetRegVec [class](../util/BackBoxRegs.md#class-asyncresetregvec)<br>

+ Breakpoint<br>
  rocket.BPControl [class](../rocket/Breakpoint.md#class-bpcontrol)<br>
  rocket.BreakpointUnit [class](../rocket/Breakpoint.md#class-breakpointunit)

+ Clock<br>
  util.ClockDivider2 [class](../util/ClockDivider.md#class-clockdivider2)<br>
  util.Pow2ClockDivider [class](../util/ClockDivider.md#class-pow2clockdivider2)

+ Configs<br>
  chip.BasePlatformConfig [class](../chip/Configs.md#class-baseplatformconfig)

+ Coreplex
  + coreplex.BankedL2CoherenceManagers<br>
    LazyModule [trait](../coreplex/CoreplexNetwork.md#bankedl2coherencemanagers);
    Bundle [trait](../coreplex/CoreplexNetwork.md#bankedl2coherencemanagersbundle);
    Module [trait](../coreplex/CoreplexNetwork.md#bankedl2coherencemanagersmodule)<br>
  + coreplex.BareCoreplex<br>
    LazyModule [abstract class](../coreplex/BaseCoreplex.md#barecoreplex);
    Bundle [abstract class](../coreplex/BaseCoreplex.md#barecoreplex);
    Module [abstract class](../coreplex/BaseCoreplex.md#barecoreplex)<br>
  + coreplex.BaseCoreplex<br>
    LazyModule [abstract class](../coreplex/BaseCoreplex.md#basecoreplex);
    Bundle [class](../coreplex/BaseCoreplex.md#basecoreplex);
    Module [class](../coreplex/BaseCoreplex.md#basecoreplex)<br>
  + coreplex.CoreplexNetwork<br>
    LazyModule [trait](../coreplex/CoreplexNetwork.md#coreplexnetwork);
    Bundle [trait](../coreplex/CoreplexNetwork.md#coreplexnetworkbundle);
    Module [trait](../coreplex/CoreplexNetwork.md#coreplexnetworkmodule)<br>
  + coreplex.CoreplexRISCVPlatform<br>
    LazyModule [trait](../coreplex/RISCVPlatform.md#coreplexriscvplatform);
    Bundle [trait](../coreplex/RISCVPlatform.md#coreplexriscvplatformbundle);
    Module [trait](../coreplex/RISCVPlatform.md#coreplexriscvplatformmodule)<br>
  + coreplex.HasRocketTiles<br>
    LazyModule [trait](../coreplex/RocketTiles.md#hasrockettiles);
    Bundle [trait](../coreplex/RocketTiles.md#hasrockettilesbundle);
    Module [trait](../coreplex/RocketTiles.md#hasrockettilesmodule)<br>

+ Counter<br>
  util.TwoWayCounter [object](../util/Counters.md#object-twowaycounter)<br>
  util.WideCounter [case class](../util/Counters.md#case-class-widecounter)

+ Crossing<br>
  util.AsyncBundle [final class](../util/AsyncBundle.md#final-class-asyncbundle)<br>
  util.AsyncQueue [class](../util/AsyncQueue.md#class-asyncqueue)<br>
  util.AsyncQueueSink [class](../util/AsyncQueue.md#class-asyncqueuesink)<br>
  util.AsyncQueueSource [class](../util/AsyncQueue.md#class-asyncqueuesource)<br>
  util.AsyncValidSync [class](../util/AsyncQueue.md#class-asyncvalidsync)<br>
  util.Crossing [abstract class](../util/Crossing.md#abstract-class-crossing)<br>
  util.CrossingIO [class](../util/Crossing.md#class-crossingio)<br>
  util.FromAsyncBundle [object](../util/AsyncBundle.md#object-fromasyncbundle)<br>
  util.GrayCounter [object](../util/AsyncQueue.md#object-graycounter)<br>
  util.ToAsyncBundle [object](../util/AsyncBundle.md#object-toasyncbundle)<br>
  util.UIntSyncChain [object](../util/AsyncQueue.md#object-uintsyncchain)<br>

## Diplomacy

### Nodes
`AdapterNode`      [class](../diplomacy/Nodes.md#class-adapternode)
`IdentityNode`     [class](../diplomacy/Nodes.md#class-identitynode)
`InputNode`        [class](../diplomacy/Nodes.md#class-inputnode)
`MixedAdapterNode` [class](../diplomacy/Nodes.md#class-mixedadapternode)
`MixedNode`        [abstract class](../diplomacy/Nodes.md#abstract-class-mixednode)
`NexusNode`        [class](../diplomacy/Nodes.md#class-nexusnode)
`OutputNode`       [class](../diplomacy/Nodes.md#class-outputnode)
`SinkNode`         [class](../diplomacy/Nodes.md#class-sinknode)
`SourceNode`       [class](../diplomacy/Nodes.md#class-sourcenode)

### Resources
`Description`      [case class](../diplomacy/Resources.md#case-class-description)
`Device`           [abstract class](../diplomacy/Resources.md#abstract-class-device)
`DeviceInterrupts` [trait](../diplomacy/Resources.md#trait-deviceinterrupts)
`DeviceRegName`    [trait](../diplomacy/Resources.md#trait-deviceregname)
`MemoryDevice`     [class](../diplomacy/Resources.md#class-memorydevice)
`SimpleDevice`     [class](../diplomacy/Resources.md#class-simpledevice)

### DeviceTree
`DTS`              [[object](../diplomacy/DeviceTree.md#object-dts)

### Parameters

`AddressRange`     [case class](../diplomacy/Parameters.md#case-class-addressrange),
                   [object](../diplomacy/Parameters.md#object-addressrange)
`AddressSet`       [case class](../diplomacy/Parameters.md#case-class-addressset),
                   [object](../diplomacy/Parameters.md#object-addressset)
`IdRange`          [case class](../diplomacy/Parameters.md#case-class-idrange)
`TransferSizes`    [case class](../diplomacy/Parameters.md#case-class-transfersizes)

+ Instruction<br>
  rocket.ExpandedInstruction [class](../rocket/RVC.md#class-expandedinstruction)<br>
  rocket.Instruction [class](../rocket/IBuf.md#class-instruction)

+ L1 cache<br>
  rocket.HasHellaCache [trait](../rocket/HellaCache.md#trait-hashellacache)<br>
  rocket.HasHellaCacheBundle [trait](../rocket/HellaCache.md#trait-hashellacachebundle)<br>
  rocket.HasHellaCacheModule [trait](../rocket/HellaCache.md#trait-hashellacachemodule)<br>
  rocket.HellaCache [class](../rocket/HellaCache.md#class-hellacache); [object](../rocket/HellaCache.md#object-hellacache)<br>
  rocket.HellaCacheBundle [class](../rocket/HellaCache.md#class-hellacachebundle)<br>
  rocket.HellaCacheIO [class](../rocket/HellaCache.md#class-hellacacheio)<br>
  rocket.HellaCacheModule [class](../rocket/HellaCache.md#class-hellacachemodule)<br>
  rocket.L1Metadata [class](../rocket/HellaCache.md#class-l1metadata)

+ L1 data cache<br>
  rocket.DCacheParams [case class](../rocket/HellaCache.md#case-class-dcacheparams)

+ L1 instruction cache<br>
  rocket.BHT [class](../rocket/BTB.md#class-bht)<br>
  rocket.BTB [class](../rocket/BTB.md#class-btb)
  rocket.RAS [class](../rocket/BTB.md#class-ras)

+ LazyModule<br>
  diplomacy.LazyModule [abstract class](../diplomacy/LazyModule/abstract-class-lazymodule); [object](../diplomacy/LazyModule/object-lazymodule)<br>
  diplomacy.LazyModuleImp [abstract class](../diplomacy/LazyModule/abstract-class-lazymoduleimp)

+ Node<br>
  diplomacy.BaseNode [abstract class](../diplomacy/Nodes.md#abstract-class-basenode)<br>
  diplomacy.BIND\_ONCE [case object](../diplomacy/Nodes.md#case-object-bind_once)<br>
  diplomacy.BIND\_QUERY [case object](../diplomacy/Nodes.md#case-object-bind_query)<br>
  diplomacy.BIND\_STAR [case object](../diplomacy/Nodes.md#case-object-bind_star)<br>
  diplomacy.InwardNode [trait](../diplomacy/Nodes.md#trait-inwardnode)<br>
  diplomacy.InwardNodeHandle [trait](../diplomacy/Nodes.md#trait-inwardnodehandle)<br>
  diplomacy.InwardNodeImp [trait](../diplomacy/Nodes.md#trait-inwardnodeimp)<br>
  diplomacy.NodeHandle [case class](../diplomacy/Nodes.md#case-class-nodehandle)<br>
  diplomacy.NodeImp [abstract class](../diplomacy/Nodes.md#abstract-class-nodeimp)<br>
  diplomacy.OutwardNode [trait](../diplomacy/Nodes.md#trait-outwardnode)<br>
  diplomacy.OutwardNodeHandle [trait](../diplomacy/Nodes.md#trait-outwardnodehandle)<br>
  diplomacy.OutwardNodeImp [trait](../diplomacy/Nodes.md#trait-outwardnodeimp)

+ Region<br>
  diplomacy.AddressRange [case class](../diplomacy/Parameters.md#case-class-addressrange); [object](../diplomacy/Parameters.md#object-addressrange)<br>
  diplomacy.AddressSet [case class](../diplomacy/Parameters.md#case-class-addressset); [object](../diplomacy/Parameters.md#object-addressset)<br>
  diplomacy.IdRange [case class](../diplomacy/Parameters.md#case-class-idrange)<br>
  diplomacy.RegionType [object](../diplomacy/Parameters.md#object-regiontype)<br>
  diplomacy.TransferSizes [case class](../diplomacy/Parameters.md#case-class-transfersizes)

+ RegisterCrossing<br>
  regmapper.BusyRegisterCrossing [class](../regmapper/RegisterCrossing.md#class-busyregistercrossing)<br>
  regmapper.RegisterWriteCrossing [class](../regmapper/RegisterCrossing.md#class-registerwritecrossing)

+ Resource<br>
  diplomacy.Resource [case class](../diplomacy/Resources.md#case-class-resource)<br>
  diplomacy.ResourceAddress [case class](../diplomacy/Resources.md#case-class-resourceaddress)<br>
  diplomacy.ResourceBinding [object](../diplomacy/Resources.md#object-resourcebindings)<br>
  diplomacy.ResourceBindings [case class](../diplomacy/Resources.md#case-class-resourcebindings)<br>
  diplomacy.ResourceInt [case class](../diplomacy/Resources.md#case-class-resourceint)<br>
  diplomacy.ResourceMapping [case class](../diplomacy/Resources.md#case-class-resourcemapping)<br>
  diplomacy.ResourceMap [case class](../diplomacy/Resources.md#case-class-resourcemap)<br>
  diplomacy.ResourceReference [case class](../diplomacy/Resources.md#case-class-resourcereference)<br>
  diplomacy.ResourceString [case class](../diplomacy/Resources.md#case-class-resourcestring)

+ RVC<br>
  rocket.IBuf [class](../rocket/IBuf.md#class-ibuf)
  rocket.RVCExpander [class](../rocket/RVC.md#class-rvcexpander)

+ Tilelink<br>
  tilelink.TLAdapterNode [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  tilelink.TLAsyncImp [object](../tilelink/Nodes.md#object-tlasyncimp)<br>
  tilelink.TLAsyncIdentityNode [object](../tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)<br>
  tilelink.TLAsyncInputNode [object](../tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)<br>
  tilelink.TLAsyncOutputNode [object](../tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)<br>
  tilelink.TLAsyncSinkNode [object](../tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)<br>
  tilelink.TLAsyncSourceNode [object](../tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)<br>
  tilelink.TLAtomics [object](../tilelink/Bundles.md#object-tlatomics)<br>
  tilelink.TLBlindInputNode [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  tilelink.TLBlindOutputNode [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  tilelink.TLBundleA [final class](../tilelink/Bundles.md#final-class-tlbundleabcde)<br>
  tilelink.TLBundleB [final class](../tilelink/Bundles.md#final-class-tlbundleabcde)<br>
  tilelink.TLBundleC [final class](../tilelink/Bundles.md#final-class-tlbundleabcde)<br>
  tilelink.TLBundleD [final class](../tilelink/Bundles.md#final-class-tlbundleabcde)<br>
  tilelink.TLBundleE [final class](../tilelink/Bundles.md#final-class-tlbundleabcde)<br>
  tilelink.TLBundleSnoop [object](../tilelink/Bundles.md#object-tlbundlesnoop)<br>
  tilelink.TLClientNode [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes); [object](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  tilelink.TLEdge [class](../tilelink/Edges.md#class-tledge)<br>
  tilelink.TLEdgeIn [class](../tilelink/Edges.md#class-tledgein)<br>
  tilelink.TLEdgeOut [class](../tilelink/Edges.md#class-tledgeout)<br>
  tilelink.TLHints [object](../tilelink/Bundles.md#object-tlhints)<br>
  tilelink.TLInputNode [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  tilelink.TLIdentityNode [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  tilelink.TLImp [object](../tilelink/Nodes.md#object-tlimp)<br>
  tilelink.TLInternalInputNode [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  tilelink.TLInternalOutputNode [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  tilelink.TLManagerNode [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes); [object](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  tilelink.TLMessages [object](../tilelink/Bundles.md#object-tlmessages)<br>
  tilelink.TLNexusNode [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  tilelink.TLOutputNode [case class](../tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  tilelink.TLPermissions [object](../tilelink/Bundles.md#object-tlpermissions)<br>
  tilelink.TLRationalBundle [object](../tilelink/Bundles.md#object-tlrationalbundle)<br>
  tilelink.TLRationalImp [object](../tilelink/Nodes.md#object-tlrationalimp)<br>
  tilelink.TLRationalIdentityNode [object](../tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)<br>
  tilelink.TLRationalInputNode [object](../tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)<br>
  tilelink.TLRationalOutputNode [object](../tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)<br>
  tilelink.TLRationalSinkNode [object](../tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)<br>
  tilelink.TLRationalSourceNode [object](../tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)<br>

<br><br><br><p align="right">
<sub>
Last updated: 12/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
