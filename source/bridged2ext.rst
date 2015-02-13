Bridged Connectivity to External Networks
=========================================

Overview

This chapter covers potential issues that could occur with Bridged Connectivity to External Networks, starting with an overview of how bridged connectivity to external networks should function and the verification steps used to confirm a working layer 2 bridged network for the example reference topology fabric.  The displays taken on a working fabric can then be used as an aid in troubleshooting issues with external Layer 2 connectivity. 

There are different ways to extend Layer 2 domain beyond the ACI fabric:

● Extend the EPG out of the ACI fabric - A user can extend an EPG out of the ACI fabric by statically assigning a port (along with VLAN ID) to an EPG. The leaf will learn the endpoint information and assign the traffic (by matching the port and VLAN ID) to the proper EPG, and then enforce the policy. The endpoint learning, data forwarding, and policy enforcement remain the same whether the endpoint is directly attached to the leaf port or if it is behind a Layer 2 network (provided the proper VLAN is enabled in the layer2 network).

● Extend the bridge domain out of the ACI fabric - This option is designed to extend the entire bridge domain (not an individual EPG under bridge domain) to the outside network.



Problem Description

There are many ways to connect ACI Leafs to external devices. The interface properties could be access, trunk, port-channel, virtual port-channel, routed, routed sub-interfaces, or SVI. When establishing Layer 2 connectivity with external devices, it’s important to match the properties such as VLANs tagged, LACP modes, etc. This is equally applicable to networks hosted by ACI as well as external networks.

When a configuration mismatch occurs, depending on the parameters, the interfaces are either down, or not forwarding traffic as expected.

Symptom 1
Interfaces connecting to the external devices are in down state.

Verification

In this example, rtp_leaf1 and rtp_leaf3 need to form a vPC pair and connect using a dedicated port-channel per UCS Fabric Interconnect. A virtual port-channel has been configured, and the APIC has assigned port-channel4 as seen below on rtp_leaf1 and rtp_leaf3.

Please note that although in this output both vPC ID (2) and Port (Po4) match on both leafs, only the vPC ID need to match for this configuration to work.

rtp_leaf1# show vpc
Legend:
                (*) - local vPC is down, forwarding via vPC peer-link
 
vPC domain id                     : 10
Peer status                       : peer adjacency formed ok
vPC keep-alive status             : Disabled
Configuration consistency status  : success
Per-vlan consistency status       : success
Type-2 inconsistency reason       : Consistency Check Not Performed
vPC role                          : primary
Number of vPCs configured         : 2
Peer Gateway                      : Disabled
Dual-active excluded VLANs        : -
Graceful Consistency Check        : Enabled
Auto-recovery status              : Enabled (timeout = 240 seconds)
Operational Layer3 Peer           : Disabled
 
vPC Peer-link status
---------------------------------------------------------------------
id   Port   Status Active vlans
--   ----   ------ --------------------------------------------------
1           up     -
 
vPC status
----------------------------------------------------------------------
id   Port   Status Consistency Reason                     Active vlans
--   ----   ------ ----------- ------                     ------------
2    Po4    down*  success     success                    -
343  Po1    up     success     success                    700,751
 
 
rtp_leaf3# show vpc
Legend:
                (*) - local vPC is down, forwarding via vPC peer-link
 
vPC domain id                     : 10
Peer status                       : peer adjacency formed ok
vPC keep-alive status             : Disabled
Configuration consistency status  : success
Per-vlan consistency status       : success
Type-2 inconsistency reason       : Consistency Check Not Performed
vPC role                          : secondary
Number of vPCs configured         : 2
Peer Gateway                      : Disabled
Dual-active excluded VLANs        : -
Graceful Consistency Check        : Enabled
Auto-recovery status              : Enabled (timeout = 240 seconds)
Operational Layer3 Peer           : Disabled
 vPC Peer-link status
---------------------------------------------------------------------
id   Port   Status Active vlans
--   ----   ------ --------------------------------------------------
1           up     -
 
vPC status
----------------------------------------------------------------------
id   Port   Status Consistency Reason                     Active vlans
--   ----   ------ ----------- ------                     ------------
2    Po4    down*  success     success                    - 
343  Po1    up     success     success                    700,751
 
 
 
Since the interfaces are in the down (D) state, a check of interface status would reveal if there is a potential layer 1 issue as seen below.

rtp_leaf1# show interface ethernet 1/27
Ethernet1/27 is down (sfp-speed-mismatch)
admin state is up, Dedicated Interface
On the GUI, Fabric -> Inventory -> Pod1 -> leafname -> Interfaces -> vPC Interfaces -> <vPC Domain ID> -> <vPC ID> -> Faults, would reveal:

 

 

Resolution

         

Configure the interface policies to match the peer device. In this scenario, the speed mismatch was addressed by changing the interface policy from 1G to 10G.


Symptom 2
Certain interfaces are in the ‘suspended’ state when configuring a port-channel or virtual port-channel.

Verification

Check the status of the vPC and port-channel using the CLI or GUI.

rtp_leaf1# show vpc
Legend:
                (*) - local vPC is down, forwarding via vPC peer-link
 
vPC domain id                     : 10
Peer status                       : peer adjacency formed ok
vPC keep-alive status             : Disabled
Configuration consistency status  : success
Per-vlan consistency status       : success
Type-2 inconsistency reason       : Consistency Check Not Performed
vPC role                          : primary
Number of vPCs configured         : 2
Peer Gateway                      : Disabled
Dual-active excluded VLANs        : -
Graceful Consistency Check        : Enabled
Auto-recovery status              : Enabled (timeout = 240 seconds)
Operational Layer3 Peer           : Disabled
 
vPC Peer-link status
---------------------------------------------------------------------
id   Port   Status Active vlans
--   ----   ------ --------------------------------------------------
1           up     -
 
vPC status
----------------------------------------------------------------------
id   Port   Status Consistency Reason                     Active vlans
--   ----   ------ ----------- ------                     ------------
2    Po4    up     success     success                    600-601,634
                                                          ,639,667-66
                                                          8
343  Po1    up     success     success                    700,751
 
rtp_leaf1# show port-channel summary
Flags:  D - Down        P - Up in port-channel (members)
        I - Individual  H - Hot-standby (LACP only)
        s - Suspended   r - Module-removed
        S - Switched    R - Routed
        U - Up (port-channel)
        M - Not in use. Min-links not met
--------------------------------------------------------------------------------
Group Port-       Type     Protocol  Member Ports
      Channel
-------------------------------------------------------------------------
------
1     Po1(SU)     Eth      LACP      Eth1/42(P)   Eth1/44(P)
4     Po4(SU)     Eth      LACP      Eth1/27(P)   Eth1/28(s)
 
On the GUI, Fabric -> Inventory -> Pod1 -> leafname -> Interfaces -> vPC Interfaces -> <vPC Domain ID> -> <vPC ID> -> Faults, would reveal:





Although the vPC is up, links to only one neighbor are members of this port-channel.

Since the interfaces are in the suspended (s) state, a check of the LACP interface status would reveal if there are any problems with LACP communications with the peer. In this example the peer LACP system identifier are different indicating two different peer devices.

rtp_leaf1# show lacp interface ethernet 1/27 | grep -A 2 Neighbor
Neighbor: 0x113
  MAC Address= 00-0d-ec-b1-a0-3c
  System Identifier=0x8000,00-0d-ec-b1-a0-3c
rtp_leaf1# show lacp interface ethernet 1/28 | grep -A 2 Neighbor
Neighbor: 0x113
  MAC Address= 00-0d-ec-b1-a9-fc
  System Identifier=0x8000,00-0d-ec-b1-a9-fc



Resolution

In this example, rtp_leaf1 and rtp_leaf3 need to form a vPC pair, and they each need to connect using a dedicated port-channel for each UCS Fabric Interconnect. When using the vPC wizard or directly configuring virtual port-channels, unique interface policy groups and interface selectors are needed to create dedicated port-channels for each peer device, such as UCS Fabric Interconnect A and Fabric Interconnect B.

Once the needed configuration is done, two independent port-channels are created.

GUI:

Fabric -> Access Policies -> Interface Policies -> Policy Groups

Fabric -> Access Policies -> Interface Policies -> Profiles

 


 

rtp_leaf1# show port-channel summary
Flags:  D - Down        P - Up in port-channel (members)
        I - Individual  H - Hot-standby (LACP only)
        s - Suspended   r - Module-removed
        S - Switched    R - Routed
        U - Up (port-channel)
        M - Not in use. Min-links not met
-------------------------------------------------------------------------
------
Group Port-       Type     Protocol  Member Ports
      Channel
-------------------------------------------------------------------------
------
1     Po1(SU)     Eth      LACP      Eth1/42(P)   Eth1/44(P)
5     Po5(SU)     Eth      LACP      Eth1/27(P)
6     Po6(SD)     Eth      LACP      Eth1/28(P)
 
Problem Description:

There are various use cases, such as migration, where the L2 extension outside ACI Fabric is needed either through direct EPG extension or through special L2 Out connectivity. During migration scenarios, there is also a need for the default gateway to be external to the ACI fabric.

Most of the time, the problem represents itself as a reachability problem between fabric hosted endpoints and external networks. In this example, an example of Web tier within the Tenant Test is used and the address of WebServer 10.2.1.11 needs to be reachable from the Nexus 7K, which has been configured for:



N7K-1-65-vdc_4# show hsrp brie
P indicates configured to preempt.
|
Interface Grp Prio P State Active addr Standby addr Group addr
Vlan700 700 110 P Active local 10.1.0.2 10.1.0.1 (conf)
Vlan750 750 110 P Active local 10.2.0.2 10.2.0.1 (conf)
Vlan751 751 110 P Active local 10.2.1.2 10.2.1.1 (conf)

The WebServer with IP of 10.2.1.11 and BD's IP of 10.2.1.254 are unreachable from the Nexus 7Ks.

N7K-1-65-vdc_4# ping 10.2.1.254
PING 10.2.1.254 (10.2.1.254): 56 data bytes
Request 0 timed out
Request 1 timed out
Request 2 timed out
Request 3 timed out
Request 4 timed out
 
--- 10.2.1.254 ping statistics ---
5 packets transmitted, 0 packets received, 100.00% packet loss
N7K-1-65-vdc_4# ping 10.2.1.11
PING 10.2.1.11 (10.2.1.11): 56 data bytes
Request 0 timed out
Request 1 timed out
Request 2 timed out
Request 3 timed out
Request 4 timed out
 
--- 10.2.1.11 ping statistics ---
5 packets transmitted, 0 packets received, 100.00% packet loss

● Extending the EPG directly out of the ACI fabric

 

Symptom 3
The Leaf is not getting programmed with the correct VLANs for BridgeDomain and EPGs.



Verification/Resolution

The reachability problem could be due to many problems, however the most common problem is that the right leafs are not programmed with the correct vlans used for BridgeDomain and EPG identification.

BD relationship with the Context:

The context-BD relationship is key for programming the leaf. Without that the VLANs don't get programmed on the leaf as shown below.

 
rtp_leaf1# show vlan brief
 
 VLAN Name                             Status    Ports
 ---- -------------------------------- --------- -------------------------------
 13   infra:default                    active    Eth1/1, Eth1/2, Eth1/5, Eth1/35
 27   Test:Database                    active    Eth1/27, Eth1/28, Po2, Po3
 28   Test:CommerceWorkspaceTest:Datab active    Eth1/27, Eth1/28, Po2, Po3
      ase
 
Once the BD is assigned the right context, the BD and EPG Vlans get programmed appropriately.

rtp_leaf1# show vlan brief
 
 VLAN Name                             Status    Ports
 ---- -------------------------------- --------- -------------------------------
 13   infra:default                    active    Eth1/1, Eth1/2, Eth1/5, Eth1/35
 27   Test:Database                    active    Eth1/27, Eth1/28, Po2, Po3
 28   Test:CommerceWorkspaceTest:Datab active    Eth1/27, Eth1/28, Po2, Po3
      ase
 37   Test:Web                         active    Eth1/27, Eth1/28, Po2, Po3
 38   Test:CommerceWorkspaceTest:Web   active    Eth1/27, Eth1/28, Po2, Po3
 
While the VLANs are programmed properly, the Ports on which the VLANs are carried seem to be incomplete. The Po2 and Po3 links to UCS hosting the VMs are shown here, however the links to the N7Ks are not, which leads us to the next possible issue.

Ports not being programmed with EPG encap VLANs:

In this example, VLAN 751 is used to connect to the Nexus 7Ks, and the EPG has been assigned dynamically VLAN 639 within the scope of the VMM domain. The following output confirms while VLAN 639 has been programmed, VLAN 751 is not present on the leaf.

 
rtp_leaf1# show vlan extended
 
 VLAN Name                             Status    Ports
 ---- -------------------------------- --------- -------------------------------
 13   infra:default                    active    Eth1/1, Eth1/2, Eth1/5, Eth1/35
 27   Test:Database                    active    Eth1/27, Eth1/28, Po2, Po3
 28   Test:CommerceWorkspaceTest:Datab active    Eth1/27, Eth1/28, Po2, Po3
      ase
 37   Test:Web                         active    Eth1/27, Eth1/28, Po2, Po3
 38   Test:CommerceWorkspaceTest:Web   active    Eth1/27, Eth1/28, Po2, Po3
 
 VLAN Type  Vlan-mode  Encap
 ---- ----- ---------- -------------------------------
 13   enet  CE         vxlan-16777209, vlan-3500
 27   enet  CE         vxlan-14680064
 28   enet  CE         vlan-600
 37   enet  CE         vxlan-15794150
 38   enet  CE         vlan-639
 
 
For this issue to be resolved, the EPG needs to be binded to a port/leaf, and also the L2Out domain needs to be attached. The L2Out would need to be associated to a VLAN pool consisting of VLAN 751.

 

 
Once the configuration is applied, the leafs are programmed to carry all the relevant L2 constructs: BD, encap VLAN for VMM domain, and encap VLAN for L2Out. Also, the right interfaces are mapped to the encap VLANs: VLAN-751 on Po1 to N7Ks and VLAN-639 on Po2, Po3 to both Fabric Interconnects of a UCS System.

 
 
rtp_leaf1# show port-channel summary
Flags:  D - Down        P - Up in port-channel (members)
        I - Individual  H - Hot-standby (LACP only)
        s - Suspended   r - Module-removed
        S - Switched    R - Routed
        U - Up (port-channel)
        M - Not in use. Min-links not met
--------------------------------------------------------------------------------
Group Port-       Type     Protocol  Member Ports
      Channel
--------------------------------------------------------------------------------
1     Po1(SU)     Eth      LACP      Eth1/42(P)   Eth1/44(P)
2     Po2(SU)     Eth      LACP      Eth1/27(P)
3     Po3(SU)     Eth      LACP      Eth1/28(P)
rtp_leaf1# show vlan extended
 
 VLAN Name                             Status    Ports
 ---- -------------------------------- --------- -------------------------------
 13   infra:default                    active    Eth1/1, Eth1/2, Eth1/5, Eth1/35
 14   Test:CommerceWorkspaceTest:Web   active    Eth1/42, Eth1/44, Po1
 27   Test:Database                    active    Eth1/27, Eth1/28, Po2, Po3
 28   Test:CommerceWorkspaceTest:Datab active    Eth1/27, Eth1/28, Po2, Po3
      ase
 37   Test:Web                         active    Eth1/27, Eth1/28, Eth1/42,
                                                 Eth1/44, Po1, Po2, Po3
 38   Test:CommerceWorkspaceTest:Web   active    Eth1/27, Eth1/28, Po2, Po3
 
 VLAN Type  Vlan-mode  Encap
 ---- ----- ---------- -------------------------------
 13   enet  CE         vxlan-16777209, vlan-3500
 14   enet  CE         vlan-751
 27   enet  CE         vxlan-14680064
 28   enet  CE         vlan-600
 37   enet  CE         vxlan-15794150
 38   enet  CE         vlan-639

rtp_leaf1# show vpc
Legend:
                (*) - local vPC is down, forwarding via vPC peer-link
 
vPC domain id                     : 10
Peer status                       : peer adjacency formed ok
vPC keep-alive status             : Disabled
Configuration consistency status  : success
Per-vlan consistency status       : success
Type-2 inconsistency reason       : Consistency Check Not Performed
vPC role                          : primary
Number of vPCs configured         : 3
Peer Gateway                      : Disabled
Dual-active excluded VLANs        : -
Graceful Consistency Check        : Enabled
Auto-recovery status              : Enabled (timeout = 240 seconds)
Operational Layer3 Peer           : Disabled
 
vPC Peer-link status
---------------------------------------------------------------------
id   Port   Status Active vlans
--   ----   ------ --------------------------------------------------
1           up     -
 
vPC status
----------------------------------------------------------------------
id   Port   Status Consistency Reason                     Active vlans
--   ----   ------ ----------- ------                     ------------
1    Po2    up     success     success                    600-601,634
                                                          ,639,666-66
                                                          9
343  Po1    up     success     success                    700,751
 
684  Po3    up     success     success                    600-601,634
                                                          ,639,667-66
                                                          8
rtp_leaf1#
 
Testing now reveals that while N7K can ping the BD address of 10.2.1.254, it cannot ping the WebServer VM (10.2.1.11).
 
N7K-2-50-N7K2# ping 10.2.1.254
PING 10.2.1.254 (10.2.1.254): 56 data bytes
Request 0 timed out
64 bytes from 10.2.1.254: icmp_seq=1 ttl=56 time=1.656 ms
64 bytes from 10.2.1.254: icmp_seq=2 ttl=56 time=0.568 ms
64 bytes from 10.2.1.254: icmp_seq=3 ttl=56 time=0.826 ms
64 bytes from 10.2.1.254: icmp_seq=4 ttl=56 time=0.428 ms
 
--- 10.2.1.254 ping statistics ---
5 packets transmitted, 4 packets received, 20.00% packet loss
round-trip min/avg/max = 0.428/0.869/1.656 ms
N7K-2-50-N7K2# ping 10.2.1.11
PING 10.2.1.11 (10.2.1.11): 56 data bytes
Request 0 timed out
Request 1 timed out
Request 2 timed out
Request 3 timed out
Request 4 timed out
 
--- 10.2.1.11 ping statistics ---
5 packets transmitted, 0 packets received, 100.00% packet loss
N7K-2-50-N7K2#
 
The scenario described here is Intra-EPG connectivity, where the contracts are not applied. So this is not related to any filter, which brings us to the next use case.

 

Symptom 4
ACI Fabric is not learning the endpoint IPs on the leafs.



Verification/Resolution

Once the leaf is programmed, the endpoints are learned as traffic is received. The endpoint learning is key, when the BD is in Hardware Proxy mode, so that the Fabric can efficiently route packets.

Since the N7Ks can ping the BD pervasive gateway address and not the Webserver IP of 10.2.1.11, the next step is to check the endpoint table.

As seen below, while the N7K addresses (10.2.1.2, 10.2.1.3) are seen, the webserver IP (10.2.1.11) is missing from the endpoint table.



 
rtp_leaf1# show endpoint  vrf Test:Test detail
Legend:
 O - peer-attached    H - vtep             a - locally-aged     S - static
 V - vpc-attached     p - peer-aged        L - local            M - span
 s - static-arp       B - bounce
+---------------+---------------+-----------------+--------------+-------------+----------------------+
      VLAN/       Encap           MAC Address       MAC Info/       Interface     Endpoint Group
      Domain      VLAN            IP Address        IP Info                       Info
+---------------+---------------+-----------------+--------------+-------------+----------------------+
Test:Test                               10.1.0.101 L
38/Test:Test            vlan-639    0050.56bb.d508 LV                        po2 Test:CommerceWorkspaceTest:Web
14/Test:Test            vlan-751    0026.f064.0000 LpV                       po1 Test:CommerceWorkspaceTest:Web
14/Test:Test            vlan-751    0000.0c9f.f2ef LpV                       po1 Test:CommerceWorkspaceTest:Web
14                      vlan-751    0026.980a.df44 LpV                       po1 Test:CommerceWorkspaceTest:Web
Test:Test               vlan-751          10.2.1.2 LV
14                      vlan-751    001b.54c2.2644 LV                        po1 Test:CommerceWorkspaceTest:Web
Test:Test               vlan-751          10.2.1.3 LV
 
 
+------------------------------------------------------------------------------+
                             Endpoint Summary
+------------------------------------------------------------------------------+
Total number of Local Endpoints     : 6
Total number of Remote Endpoints    : 0
Total number of Peer Endpoints      : 0
Total number of vPC Endpoints       : 5
Total number of non-vPC Endpoints   : 1
Total number of MACs                : 5
Total number of VTEPs               : 0
Total number of Local IPs           : 3
Total number of Remote IPs          : 0
Total number All EPs                : 6
 
Just as mac-addresses are learnt in traditional switching, the endpoints are learnt by the leaf when the first packet is received. A ping from the VM triggers this learning and the following output confirm this:

 
rtp_leaf1# show endpoint  vrf Test:Test detail
Legend:
 O - peer-attached    H - vtep             a - locally-aged     S - static
 V - vpc-attached     p - peer-aged        L - local            M - span
 s - static-arp       B - bounce
+---------------+---------------+-----------------+--------------+-------------+-------------------------+
      VLAN/       Encap           MAC Address       MAC Info/       Interface     Endpoint Group
      Domain      VLAN            IP Address        IP Info                       Info
+---------------+---------------+-----------------+--------------+-------------+-------------------------+
Test:Test                               10.1.0.101 L
38                      vlan-639    0050.56bb.d508 LpV                       po2 Test:CommerceWorkspaceTest:Web
Test:Test               vlan-639         10.2.1.11 LV
14/Test:Test            vlan-751    0026.f064.0000 LpV                       po1 Test:CommerceWorkspaceTest:Web
14/Test:Test            vlan-751    0000.0c9f.f2ef LpV                       po1 Test:CommerceWorkspaceTest:Web
14                      vlan-751    0026.980a.df44 LpV                       po1 Test:CommerceWorkspaceTest:Web
Test:Test               vlan-751          10.2.1.2 LV
14                      vlan-751    001b.54c2.2644 LV                        po1 Test:CommerceWorkspaceTest:Web
Test:Test               vlan-751          10.2.1.3 LV
 
 
+------------------------------------------------------------------------------+
                             Endpoint Summary
+------------------------------------------------------------------------------+
Total number of Local Endpoints     : 6
Total number of Remote Endpoints    : 0
Total number of Peer Endpoints      : 0
Total number of vPC Endpoints       : 5
Total number of non-vPC Endpoints   : 1
Total number of MACs                : 5
Total number of VTEPs               : 0
Total number of Local IPs           : 4
Total number of Remote IPs          : 0
Total number All EPs                : 6
 
 
Once the endpoint is learned, the ping is successful from the N7K to the Webserver IP of 10.2.1.11

 
N7K-1-65-vdc_4# ping 10.2.1.11
PING 10.2.1.11 (10.2.1.11): 56 data bytes
64 bytes from 10.2.1.11: icmp_seq=0 ttl=127 time=1.379 ms
64 bytes from 10.2.1.11: icmp_seq=1 ttl=127 time=1.08 ms
64 bytes from 10.2.1.11: icmp_seq=2 ttl=127 time=0.498 ms
64 bytes from 10.2.1.11: icmp_seq=3 ttl=127 time=0.479 ms
64 bytes from 10.2.1.11: icmp_seq=4 ttl=127 time=0.577 ms
 
--- 10.2.1.11 ping statistics ---
5 packets transmitted, 5 packets received, 0.00% packet loss
round-trip min/avg/max = 0.479/0.802/1.379 ms
N7K-1-65-vdc_4#
 


This issue is also seen with the N7K HSRP address as well, since N7K does not normally source packets from the HSRP address. In the above tables, the HSRP IP (10.2.1.1) is missing from the endpoint table.

Forcing N7K to source the packet from the HSRP address populates the endpoint table.

 
N7K-1-65-vdc_4# ping 10.2.1.254 source 10.2.1.1
PING 10.2.1.254 (10.2.1.254) from 10.2.1.1: 56 data bytes
Request 0 timed out
64 bytes from 10.2.1.254: icmp_seq=1 ttl=57 time=1.472 ms
64 bytes from 10.2.1.254: icmp_seq=2 ttl=57 time=1.062 ms
64 bytes from 10.2.1.254: icmp_seq=3 ttl=57 time=1.097 ms
64 bytes from 10.2.1.254: icmp_seq=4 ttl=57 time=1.232 ms
 
--- 10.2.1.254 ping statistics ---
5 packets transmitted, 4 packets received, 20.00% packet loss
round-trip min/avg/max = 1.062/1.215/1.472 ms
N7K-1-65-vdc_4# 
 


This is one of the reason, when the default gateway is outside the fabric, the Fabric BD mode should be enabled for flooding and NOT Hardware Proxy.

 
rtp_leaf1# show endpoint  vrf Test:Test detail
Legend:
 O - peer-attached    H - vtep             a - locally-aged     S - static
 V - vpc-attached     p - peer-aged        L - local            M - span
 s - static-arp       B - bounce
+---------------+---------------+-----------------+--------------+-------------+----------------------+
      VLAN/       Encap           MAC Address       MAC Info/       Interface     Endpoint Group
      Domain      VLAN            IP Address        IP Info                       Info
+---------------+---------------+-----------------+--------------+-------------+----------------------+
Test:Test                               10.1.0.101 L
38                      vlan-639    0050.56bb.d508 LV                        po2 Test:CommerceWorkspaceTest:Web
Test:Test               vlan-639         10.2.1.11 LV
14/Test:Test            vlan-751    0026.f064.0000 LpV                       po1 Test:CommerceWorkspaceTest:Web
14/Test:Test            vlan-751    0000.0c9f.f2ef LpV                       po1 Test:CommerceWorkspaceTest:Web
14                      vlan-751    0026.980a.df44 LpV                       po1 Test:CommerceWorkspaceTest:Web
Test:Test               vlan-751          10.2.1.2 LV
14                      vlan-751    001b.54c2.2644 LpV                       po1 Test:CommerceWorkspaceTest:Web
Test:Test               vlan-751          10.2.1.3 LV
Test:Test               vlan-751          10.2.1.1 LV
 
 
+------------------------------------------------------------------------------+
                             Endpoint Summary
+------------------------------------------------------------------------------+
Total number of Local Endpoints     : 6
Total number of Remote Endpoints    : 0
Total number of Peer Endpoints      : 0
Total number of vPC Endpoints       : 5
Total number of non-vPC Endpoints   : 1
Total number of MACs                : 5
Total number of VTEPs               : 0
Total number of Local IPs           : 5
Total number of Remote IPs          : 0
Total number All EPs                : 6
 
  
N7K-1-65-vdc_4# ping 10.2.1.11 source 10.2.1.1
PING 10.2.1.11 (10.2.1.11) from 10.2.1.1: 56 data bytes
64 bytes from 10.2.1.11: icmp_seq=0 ttl=127 time=1.276 ms
64 bytes from 10.2.1.11: icmp_seq=1 ttl=127 time=0.751 ms
64 bytes from 10.2.1.11: icmp_seq=2 ttl=127 time=0.752 ms
64 bytes from 10.2.1.11: icmp_seq=3 ttl=127 time=0.807 ms
64 bytes from 10.2.1.11: icmp_seq=4 ttl=127 time=0.741 ms
 
--- 10.2.1.11 ping statistics ---
5 packets transmitted, 5 packets received, 0.00% packet loss
round-trip min/avg/max = 0.741/0.865/1.276 ms
N7K-1-65-vdc_4#
 
 

Problem Description

Extending bridged domain using external bridged network:

In this scenario, Layer 2 extension is achieved using a unique external EPG so as to address spanning tree interoperability when integrating/extending with external Layer 2 networks inside the ACI fabric. 

In this setup, the Web EPG is not directly associated with L2Out interfaces towards the N7K. Instead, Web EPG is associated to BD Web, which is then extended using external bridged connectivity named L2Out, with the external networks identified to be allowed to communicate with the Web tier.

Symptom 1
The Leaf is not getting programmed with the correct VLANs for BridgeDomain and EPGs.

Verification

As with the previous scenario with direct EPG extension outside the fabric, programming the leafs needs to happen before the endpoints are learned by the leafs. Mismatch in configuration is the most common scenario seen when defining the extended bridged network.

rtp_leaf1# show vlan extended
 
 VLAN Name                             Status    Ports
 ---- -------------------------------- --------- -------------------------------
 13   infra:default                    active    Eth1/1, Eth1/2, Eth1/5, Eth1/35
 27   Test:Database                    active    Eth1/27, Eth1/28, Po2, Po3
 28   Test:CommerceWorkspaceTest:Datab active    Eth1/27, Eth1/28, Po2, Po3
      ase
 37   Test:Web                         active    Eth1/27, Eth1/28, Eth1/42,
                                                 Eth1/44, Po1, Po2, Po3
 38   Test:CommerceWorkspaceTest:Web   active    Eth1/27, Eth1/28, Po2, Po3
 68   --                               active    Eth1/42, Eth1/44, Po1
 
 VLAN Type  Vlan-mode  Encap
 ---- ----- ---------- -------------------------------
 13   enet  CE         vxlan-16777209, vlan-3500
 27   enet  CE         vxlan-14680064
 28   enet  CE         vlan-600
 37   enet  CE         vxlan-15794150
 38   enet  CE         vlan-639
 68   enet  CE         vlan-750
 
Since N7Ks are expecting VLAN-751 but the L2Out is configured with VLAN-750, the Layer 2 domains are not extended correctly.

 



 

Resolution

Changing it to VLAN-751, makes the N7K ping the BD address of 10.2.1.254, but not the WebServer 10.1.2.11. This is due to the fact that external network are identified as an EPG L2Out and contracts are needed to make communication happen between any two EPGs. 

 

rtp_leaf1# show vlan extended
 VLAN Name                             Status    Ports
 ---- -------------------------------- --------- -------------------------------
 13   infra:default                    active    Eth1/1, Eth1/2, Eth1/5, Eth1/35
 27   Test:Database                    active    Eth1/27, Eth1/28, Po2, Po3
 28   Test:CommerceWorkspaceTest:Datab active    Eth1/27, Eth1/28, Po2, Po3
      ase
 37   Test:Web                         active    Eth1/27, Eth1/28, Eth1/42,
                                                 Eth1/44, Po1, Po2, Po3
 38   Test:CommerceWorkspaceTest:Web   active    Eth1/27, Eth1/28, Po2, Po3
 69   --                               active    Eth1/42, Eth1/44, Po1
 
 VLAN Type  Vlan-mode  Encap
 ---- ----- ---------- -------------------------------
 13   enet  CE         vxlan-16777209, vlan-3500
 27   enet  CE         vxlan-14680064
 28   enet  CE         vlan-600
 37   enet  CE         vxlan-15794150
 38   enet  CE         vlan-639
 69   enet  CE         vlan-751
 

N7K-1-65-vdc_4# ping 10.2.1.254
PING 10.2.1.254 (10.2.1.254): 56 data bytes
64 bytes from 10.2.1.254: icmp_seq=0 ttl=56 time=1.068 ms
64 bytes from 10.2.1.254: icmp_seq=1 ttl=56 time=0.753 ms
64 bytes from 10.2.1.254: icmp_seq=2 ttl=56 time=0.708 ms
64 bytes from 10.2.1.254: icmp_seq=3 ttl=56 time=0.731 ms
64 bytes from 10.2.1.254: icmp_seq=4 ttl=56 time=0.699 ms
 
--- 10.2.1.254 ping statistics ---
5 packets transmitted, 5 packets received, 0.00% packet loss
round-trip min/avg/max = 0.699/0.791/1.068 ms
N7K-1-65-vdc_4# ping 10.2.1.11
PING 10.2.1.11 (10.2.1.11): 56 data bytes
Request 0 timed out
Request 1 timed out
Request 2 timed out
Request 3 timed out
Request 4 timed out
 
--- 10.2.1.11 ping statistics ---
5 packets transmitted, 0 packets received, 100.00% packet loss
 

Symptom 2
The Leaf is programmed with correct VLANs and Interfaces as expected, but the servers are unreachable from the outside L2 network.

Verification

The presence of contracts between the Web EPG and L2Out EPG need to be checked to confirm reachability of Webserver from N7K. The PcTag of Web EPG is found from Visore to be 49153.

rtp_leaf1# show zoning-rule | grep 49153
 
rtp_leaf1#


Resolution

After configuring contracts between the WebEPG and L2Out EPG, the command output shows as below:

rtp_leaf1# show zoning-rule | grep 49153
5352            49153           16386           default         enabled         2883584         permit
5353            16386           49153           default         enabled         2883584         permit
Once the contracts are defined, the pings from N7K are successful. The endpoints still are learnt as they send traffic, so the issues highlighted in the previous 'Symptoms when extending the EPG directly out of the ACI fabric: Endpoint not in the database' section is applicable even in this scenario.

N7K-1-65-vdc_4# ping 10.2.1.11
PING 10.2.1.11 (10.2.1.11): 56 data bytes
64 bytes from 10.2.1.11: icmp_seq=0 ttl=127 time=1.676 ms
64 bytes from 10.2.1.11: icmp_seq=1 ttl=127 time=0.689 ms
64 bytes from 10.2.1.11: icmp_seq=2 ttl=127 time=0.626 ms
64 bytes from 10.2.1.11: icmp_seq=3 ttl=127 time=0.75 ms
64 bytes from 10.2.1.11: icmp_seq=4 ttl=127 time=0.797 ms
 
--- 10.2.1.11 ping statistics ---
5 packets transmitted, 5 packets received, 0.00% packet loss
round-trip min/avg/max = 0.626/0.907/1.676 ms