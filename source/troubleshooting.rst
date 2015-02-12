***************
Troubleshooting
***************

Naming Conventions
==================

Overview
--------

Logical thinking and clear communication is the champion of the
troubleshooting process. This chapter presents some recommended practices for
naming of managed objects in the ACI policy model to provide clean and logical
organization and clarity in the object's reference. As the management
information tree is navigated during policy creation or inspection (during
troubleshooting), consistency and meaningful context become extremely helpful.

Effective troubleshooting with the ACI environment does require some knowledge
of the ACI policy model. Many of the objects within this policy are unbounded
fields that are left open to the administrator to name. Having a predefined
and consistent methodology for deriving these object names can provide some
clarity, which can greatly aid in configuration and, more importantly,
troubleshooting. By using names which are descriptive of the purpose and scope
in the tree relevant to the MO, easier identification is achieved for the
various MOs, their place in the tree, and their use/relationships at a glance.
This process of descriptive naming is very helpful in delivering context at a
glance.

A good example for this type of structured naming is configuring a VLAN pool
to be used for a Cisco Application Virtual Switch (AVS) deployment and naming
it "VLANsForAVS". The name identifies the object, and what it is used for.
Exploring this situation within the context of a real life situation is
helpful. Take for example entering a troubleshooting situation after the
environment has been configured. Ideally, it would be possible to see an
object when viewing the policy model through Visore or the CLI and know by the
name "VLANsForAVS" that it is a VLAN pool for an AVS deployment. The benefits
of this naming methodology are clear.

Suggested Naming Templates
--------------------------

Below are some suggested templates for naming the various MOs in the fabric
with an explanation of how each was constructed.

When naming Attachable Entity Profiles, it is good to define in the name the
resource type, and concatenate a suffix of -AEP behind it
([Resource-Type]-AEP). Examples:

* DVS-AEP describes an AEP for use with a VMware DVS
* UCS-AEP describes an AEP for use when connecting a Cisco Unified Computing
  System (UCS)
* L2Outxxx-AEP describes an AEP that gets used when connecting to an external
  device via an L2Out connection
* L3Outxxx-AEP describes an AEP that gets used when connecting to an external
  device via an L3Out connection
* vSwitch-AEP describes an AEP used when connecting to a standard vSwitch.

Contracts are used to describe communications that are allowed between
EndPoint Groups (EPGs). When creating contracts, it's a good idea to reference
which objects are talking and the scope of relevance in the fabric. This could
be defined in the format of [SourceEPG]to[DestinationEPG]-[Scope]Con which
includes the from and to EPGs as well as the scope of application for the
contract. Examples:

* WebToApp-GblCon describes a globally scoped contract object and is used to
  describe communications between the Web EPG and the App EPG.
* AppToDB-TnCon describes a contract scoped to a specific tenant that describes
  communications between the App EPG and the DB EPG within that specific
  tenant.

Contracts that deal with some explicit communications protocol function (such
as allowing ICMP or denying some specific protocol), can be given a name based
on the explicit reference and scope. This could be defined in the format of
[ExplicitFunction]-[Scope]Con which indicates the protocol or service to be
allowed as well as the scope for the placement of the contract. Some examples
of explicit contracts might include the following:

* ICMPAllow-CtxCon is a contract scoped to a specific context that allows ICMP
* HTTPDeny-ApCon is a contract scoped to an application that denies HTTP
  protocol

Contracts are compound objects that reference other lower-level objects. A
Contract references a subject, which references a filter that has multiple
filter entries. In order to maintain good naming consistency, similar naming
structure should be followed. A Subject should keep to a naming convention
like [RuleGroup]-[Direction]Sbj, as seen in these examples:


* AppTraffic-BiSbj names a subject that defines bidirectional flows of a
  specific applications traffic
* WebTraffic-UniSbj names a subject that defines web traffic in a single
  direction

A Filter should have a naming convention structure of [ResourceName]-flt, such
as:

* SQL-flt names a filter that contains entries to allow communications for an
  SQL server
* Exchange-flt names a filter that contains entries that allows
  communications for an Exchange server

Filter Entries should follow a structure like [ResourceName]-[Service] such as:

* Exchange-HTTP might be the name of a filter entry that allows HTTP service
  connections to an exchange server (such as for OWA connections)
* VC-Mgmt might name a filter entry allowing management connections to a VMware
  vCenter server
* SQL-CIMC is a name for a filter entry that allows connections to the CIMC
  interface on a SQL server running on a standalone Cisco UCS Rack mount
  server.

If all of these are put together the results might look like this:

AppToDB-TnConreferences DBTraffic-BiSbj with filter SQL-flt which has an entry
such as SQL-data. This combined naming chain can almost be read as common
text, such as "this contract to allow database traffic in both directions that
is filtered to only allow SQL data connections".

Interface policy naming should follow some characteristics, such as:

* Link Level structure - [Speed][Negotiation], Ex: 1GAuto, 10GAuto - directly
  describes the speed and negotiation mode.
* CDP Interface configuration policy - explicit naming: EnableCDP / DisableCDP
* LLDP Interface configuration policy - explicit naming: EnableLLDP /
  DisableLLDP

When grouping interface policies, it's good to structure naming based on the
interface type and its use like [InterfaceType]For[Resource-Type]such as:

* PCForDVS names a policy that describes a portchannel used for the uplinks
  from a DVS
* VPCForUCS names a virtual portchannel for connecting to a set of UCS Fabric
  Interconnects
* UplinkForvSwitch names a single port link connecting to a standard vSwitch.
* PCForL3Out names a portchannel connecting to an external L3 network

Interface profiles naming should be relative to the profile's use, such as
IntsFor[Resource-Type]. Examples:

* IntsForL3Outxxx names an interface profile for connecting to an external L3
  network
* IntsForUCS names an interface profile for connecting to a UCS system
* IntsForDVS names an interface profile for connecting to a DVS running on a
  VMware host
  
Switch Selectors should be named using a structure like
LeafsFor[Resource-Type]. Some examples:

* LeafsForUCS switch selector policy to group leafs that are used for
  connecting UCS
* LeafsForDVS switch selector policy that might be used to group leafs used
  for DVS connections
* LeafsForL3Out policy that might be used to group leafs for external L3
  connections
  
And when creating VLAN pools, structure of VLANsFor[Resources-Type] could
produce:

* VLANsForDVS names a VLAN pool for use with DVS-based endpoint connections
* VLANsForvSwitches names a VLAN pool for use with vSwitch-based endpoint
  connections
* VLANsForAVS names a VLAN pool for use with AVS-based endpoint
  connections
* VLANsForL2Outxxx names a VLAN pool used with L2 external connections.
  VLANsForL3Outxxx names a VLAN pool used with L3 external connections.
