Class index
========================
***************************

+ AdapterNode<br>
  diplomacy.AdapterNode [class](../diplomacy/Nodes.md#class-adapternode)<br>
  diplomacy.IdentityNode [class](../diplomacy/Nodes.md#class-identitynode)<br>
  diplomacy.InputNode [class](../diplomacy/Nodes.md#class-inputnode)<br>
  diplomacy.MixedAdapterNode [class](../diplomacy/Nodes.md#class-mixedadapternode)<br>
  diplomacy.MixedNode [abstract class](../diplomacy/Nodes.md#abstract-class-mixednode)<br>
  diplomacy.NexusNode [class](../diplomacy/Nodes.md#class-nexusnode)<br>
  diplomacy.OutputNode [class](../diplomacy/Nodes.md#class-outputnode)<br>
  diplomacy.SinkNode [class](../diplomacy/Nodes.md#class-sinknode)<br>
  diplomacy.SourceNode [class](../diplomacy/Nodes.md#class-sourcenode)

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

+ Coreplex<br>
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

+ Device<br>
  diplomacy.Description [case class](../diplomacy/Resources.md#case-class-description)<br>
  diplomacy.Device [abstract class](../diplomacy/Resources.md#abstract-class-device)<br>
  diplomacy.DeviceInterrupts [trait](../diplomacy/Resources.md#trait-deviceinterrupts)<br>
  diplomacy.DeviceRegName [trait](../diplomacy/Resources.md#trait-deviceregname)<br>
  diplomacy.MemoryDevice [class](../diplomacy/Resources.md#class-memorydevice)<br>
  diplomacy.SimpleDevice [class](../diplomacy/Resources.md#class-simpledevice)

+ DTS<br>
  diplomacy.DTS [object](../diplomacy.md/diplomacy/DeviceTree.md#object-dts)

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
  devices.tilelink.TLAdapterNode [case class](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLAsyncImp [object](../devices/tilelink/Nodes.md#object-tlasyncimp)<br>
  devices.tilelink.TLAsyncIdentityNode [object](../devices/tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLAsyncInputNode [object](../devices/tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLAsyncOutputNode [object](../devices/tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLAsyncSinkNode [object](../devices/tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLAsyncSourceNode [object](../devices/tilelink/Nodes.md#object-asynchronous-tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLAtomics [object](../devices/tilelink/Bundles.md#object-tlatomics)<br>
  devices.tilelink.TLBlindInputNode [case class](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLBlindOutputNode [case class](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLBundleA [final class](../devices/tilelink/Bundles.md#final-class-tlbundleabcde)<br>
  devices.tilelink.TLBundleB [final class](../devices/tilelink/Bundles.md#final-class-tlbundleabcde)<br>
  devices.tilelink.TLBundleC [final class](../devices/tilelink/Bundles.md#final-class-tlbundleabcde)<br>
  devices.tilelink.TLBundleD [final class](../devices/tilelink/Bundles.md#final-class-tlbundleabcde)<br>
  devices.tilelink.TLBundleE [final class](../devices/tilelink/Bundles.md#final-class-tlbundleabcde)<br>
  devices.tilelink.TLBundleSnoop [object](../devices/tilelink/Bundles.md#object-tlbundlesnoop)<br>
  devices.tilelink.TLClientNode [case class](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes); [object](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLEdge [class](../devices/tilelink/Edges.md#class-tledge)<br>
  devices.tilelink.TLEdgeIn [class](../devices/tilelink/Edges.md#class-tledgein)<br>
  devices.tilelink.TLEdgeOut [class](../devices/tilelink/Edges.md#class-tledgeout)<br>
  devices.tilelink.TLHints [object](../devices/tilelink/Bundles.md#object-tlhints)<br>
  devices.tilelink.TLInputNode [case class](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLIdentityNode [case class](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLImp [object](../devices/tilelink/Nodes.md#object-tlimp)<br>
  devices.tilelink.TLInternalInputNode [case class](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLInternalOutputNode [case class](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLManagerNode [case class](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes); [object](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLMessages [object](../devices/tilelink/Bundles.md#object-tlmessages)<br>
  devices.tilelink.TLNexusNode [case class](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLOutputNode [case class](../devices/tilelink/Nodes.md#tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLPermissions [object](../devices/tilelink/Bundles.md#object-tlpermissions)<br>
  devices.tilelink.TLRationalBundle [object](../devices/tilelink/Bundles.md#object-tlrationalbundle)<br>
  devices.tilelink.TLRationalImp [object](../devices/tilelink/Nodes.md#object-tlrationalimp)<br>
  devices.tilelink.TLRationalIdentityNode [object](../devices/tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLRationalInputNode [object](../devices/tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLRationalOutputNode [object](../devices/tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLRationalSinkNode [object](../devices/tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)<br>
  devices.tilelink.TLRationalSourceNode [object](../devices/tilelink/Nodes.md#object-rational-tilelink-extension-of-basic-nodes)<br>

<br><br><br><p align="right">
<sub>
Last updated: 08/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
