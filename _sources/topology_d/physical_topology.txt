Physical Fabric Topology
========================

For a consistent frame of reference, a sample reference topology has been
deployed, provisioned and used throughout the book. This ensures a consistent
reference for the different scenarios and troubleshooting exercises.

This section explores the different aspects of the reference topology, from
the logical application view to the physical fabric and any supporting details
that will be used throughout the troubleshooting exercises. Each individual
section will call out the specific components that have been focused on so the
reader does not have to refer back to this section in every exercise.

The topology includes a Cisco ACI Fabric composed of three clustered Cisco
APIC Controllers, two Nexus 9500 spine switches, and three Nexus 9300 leaf
switches. The APICs and Nexus 9000 switches are running the current release on
www.cisco.com at the initial version of this book. This is APIC version
1.0(1k) and Nexus ACI-mode version 11.0(1d).

The fabric is connected to both external Layer 2 and Layer 3 networks. For the
external Layer 2 network, the connection used a pair of interfaces aggregated
into a port channel connecting to a pair of Cisco Nexus 7000 switches that are
configured as a Virtual Port Channel. The connection to the external Layer 3
network is individual links on each leaf to each Nexus 7000.

Each leaf also contains a set of connections to host devices. Host devices
include a directly connected Cisco UCS C-Series rack server and a UCS B-Series
Blade Chassis connected via a pair of fabric interconnects. All servers are
running virtualization hypervisors. The blade servers are virtualized using
VMware ESX, with some of the hosts as part of a VMware Distributed Virtual
Switch, and some others as virtual leafs part of the Cisco ACI Application
Virtual Switch. The guest virtual machines on the hosts are a combination of
traditional operating systems and virtual network appliances such as virtual
Firewalls and Load Balancers.

.. image:: /images/physical_1.jpg
   :width: 750 px
   :align: center
