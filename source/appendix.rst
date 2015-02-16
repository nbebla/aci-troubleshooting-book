Appendix
========

.. contents::
   :local:
   :depth: 2

Overview
--------

This section is designed to provide a high level description of terms and
concepts that get brought up in this book. While ACI does not change how
packets are transmitted on a wire, there are some new terms and concepts
employed, and understanding those new terms and concepts will help those
working on ACI communicate with one another about the constructs used in ACI
used to transmit those bits. Associated new acronyms are also provided.

This is not meant to be an exhaustive list nor a completely detailed dictionary
of all of the terms and concepts, only the key ones that may not be a part of
the common vernacular or which would be relevant to the troubleshooting
exercises that were covered in the troubleshooting scenarios discussed.

A
+

**AAA**: acronym for Authentication, Authorization, and Accounting.

**ACI External Connectivity**: Any connectivity to and from the fabric that
uses an external routed or switched intermediary system, where endpoints fall
outside of the managed scope of the fabric.

**ACID transactions**: ACID is an acrronym for Atomicity, Consistency,
Isolation, Durability – properties of transactions that ensure consistency in
database transactions. Transactions to APIC devices in an ACI cluster are
considered ACID, to ensure that database consistency is maintained. This means
that if one part of a transaction fails the entire transaction fails.

**AEP**: Attach Entity Profile – this is a configuration profile of the
interface that gets applied when an entity attaches to the fabric. An AEP
represents a group of external entities with similar infrastructure policy
requirements.

**ALE**: Application Leaf Engine, an ASIC on a leaf switch.

**APIC**: Application Infrastructure Controller is a centralized policy
management controller cluster. The APIC configures the intended state of the
policy to the fabric.

**API**: Application Programming Interface used for programmable extensibility.

**Application Profile**: Term used to reference an application profile managed
object reference that models the logical components of an application and how
those components communicate. The AP is the key object used to represent an
application and is also the anchor point for the automated infrastructure
management in an ACI fabric.

**ASE**: Application Spine Engine, an ASIC on a Spine switch.

B
+

**BGP**: Border Gateway Protocol, on the ACI fabric BGP is used to distribute
reachability information within the fabric.

**Bridge Domain**: A unique layer 2 forwarding domain that contains one or more
subnets.

 

C
+

**Clos fabric**: A multi-tier nonblocking leaf-spine architecture network.

**Cluster**: Set of devices that work together as a single system to provide an
identical or similar set of functions.

**Contracts**: A logical container for the subjects which relate to the filters
that govern the rules for communication between endpoint groups.  ACI works on
a white list policy model.  Without a contract, the default forwarding policy
is to not allow any communication between EPGs but communication within an EPG
is allowed.

**Context**: A layer 3 forwarding domain, equivalent to a VRF.  Every bridge
domain needs to be associated with a context.


D
+

**DLB**: Dynamic Load Balancing – a network traffic load balancing mechanism
in the ACI fabric based on flowlet switching.

**DME**: Data Management Engine, a service that runs on the APIC that manages
data for the data model.

**dMIT**: distributed Management Information Tree, a representation of the ACI
object model with the root of the tree at the top and the leaves of the tree
at the bottom.  The tree contains all aspects of the object model that
represent an ACI fabric.

**Dn**: Distinguished name – a fully qualified name that represents a specific
object within the ACI management information tree as well as the specific
location information in the tree. It is made up of a concatenation of all of
the relative names from itself back to the root of the tree. As an example, if
policy object of type Application Profile is created named commerceworkspace
within a Tenant named Prod, the dn would be expressed as
uni/tn-Prod/ap-commerceworkspace.


E
+

**EP**: Endpoint - Any logical or physical device connected directly or
indirectly to a port on a leaf switch that is not a fabric facing port.
Endpoints have specific properties like an address, location, or potentially
some other attribute, which is used to identify the endpoint. Examples include
virtual-machines, servers, storage devices, etc.

**EPG**: A collection of endpoints that can be grouped based on common
requirements for a common policy. Endpoint groups can be dynamic or static.


F
+

**Fault**: When a failure occurs or an alarm is raised, the system creates a
fault managed object for the fault. A fault contains the conditions,
information about the operational state of the affected object, and potential
resolutions for the problem.

**Fabric**: Topology of network nodes.

**Filters**: Filters define the rules outlining the layer 2 to layer 4 fields
that will be matched by a contract.

**Flowlet switching**:  An optimized multipath load balancing methodology
based on research from MIT in 2004. Flowlet Switching is a way to use TCP’s
own bursty nature to more efficiently forward TCP flows by dynamically
splitting flows into flowlets and splitting traffic across multiple parallel
paths without requiring packet reordering.


G
+

**GUI**: Graphical User Interface.


H
+

**HTML**: HyperText Markup Language, a markup language that focuses on the
formatting of web pages.

**Hypervisor**: Software that abstracts the hardware on a host machine and
allows the host machine to run multiple virtual machines.

**Hypervisor integration**: Extension of ACI Fabric connectivity to a
virtualization manager to provide the APIC controller with a mechanism for
virtual machine visibility and policy enforcement.


I
+

**IFM**: Intra-Fabric Messages, Used for communication between different
devices on the ACI fabric.

**Inband Management (INB)**: Inband Management. Connectivity using an inband
management configuration. This uses a front panel (data plane) port of a leaf
switch for external management connectivity for the fabric and APICs.

**IS-IS**: Link local routing protocol leveraged by the fabric for
infrastructure topology. Loopback and VTEP addresses are internally advertised
over IS-IS. IS-IS announces the creation of tunnels from leaf nodes to all
other nodes in fabric.


J
+

**JSON**: JavaScript Object Notation, a data encapsulation format that uses
human readable text to encapsulate data objects in attribute and value pairs.


L
+

**Layer 2 Out (l2out)**: Layer 2 connectivity to an external network that
exists outside of the ACI fabric.

**Layer 3 Out (l3out)**: Layer 3 connectivity to an external network that
exists outside of the ACI fabric.

**L4-L7 Service Insertion**: The insertion of a service like a firewall and a
load balancer into the flow of traffic. Service nodes operate between Layers
4 and 7 of the OSI model, where as networking elements (i.e. the fabric)
operate at layers 1-3).

**Labels**: Used for classifying which objects can and cannot communicate with
each other.

**Leaf**: Network node in fabric providing host and border connectivity. Leafs
connect only to hosts and spines. Leafs never connect to each other.


M
+

**MO**: Managed Object – every configurable component of the ACI policy model
managed in the MIT is called a MO.

**Model**: A model is a concept which represents entities and the
relationships that exist between them.

**Multi-tier Application**: Client–server architecture in which presentation,
application logic, and database management functions are physically separated
and require networking functions to communicate with the other tiers for
application functionality.


O
+

**Object Model**: A collection of objects and classes are used to examine and
manipulate the configuration and running state of the system that is exposing
that object model. In ACI the object model is represented as a tree known as
the distributed management information tree (dMIT).

**Out of Band management (OOBM)**: External connectivity using a specific
out-of-band management interface on every switch and APIC.


P
+

**Port Channel**: Port link aggregation technology that binds multiple
physical interfaces into a single logical interface and provides more
aggregate bandwidth and link failure redundancy.
 

R
+

**RBAC**: Role Based Access Control, which is a method of managing secure
access to infrastructure by assigning roles to users, then using those roles
in the process of granting or denying access to devices, objects and privilege
levels.

**REpresentational State Transfer (REST)**: a stateless protocol usually run
over HTTP that allows a client to access a service.  The location that the
client access usually defines the data the client is trying to access from the
service.  Data is usually accessed and returned in either XML or JSON format.

**RESTful**: An API that uses REST, or Representational State Transfer.

**Rn**: Relative name, a name of a specific object within the ACI management
information tree that is not fully qualified. A Rn is significant to the
individual object, but without context, it’s not very useful in navigation. A
Rn would need to be concatenated with all the relative names from itself back
up to the root to make a distinguished name, which then becomes useful for
navigation. As an example, if an Application Profile object is created named
"commerceworkspace", the Rn would be "ap-commerceworkspace" because
Application Profile relative names are all prefaced with the letters "ap-".
See also the Dn definition.
 

S
+

**Service graph**: Cisco ACI treats services as an integral part of an
application. Any services that are required are treated as a service graph that
is instantiated on the ACI fabric from the APIC. Service graphs identify the
set of network or service functions that are needed by the application, and
represent each function as a node. A service graph is represented as two or
more tiers of an application with the appropriate service function inserted
between.

**Spine**: Network node in fabric carrying aggregate host traffic from leafs,
connected only to leafs in the fabric and no other device types.

**Spine Leaf topology**: A clos-based fabric topology in which spine nodes
connect to leaf nodes, leaf nodes connect to hosts and external networks.

**Subnets**: Contained by a bridge domain, a subnet defines the IP address
range that can be used within the bridge domain.

**Subjects**: Contained by contracts and create the relationship between
filters and contracts.

**Supervisor**: Switch module/line card that provides the processing engine.


T
+

**Tenants**: The logical container to group all policies for application
policies. This allows isolation from a policy perspective. For service
providers this would be a customer. In an enterprise or organization this
would allow the organization to define policy separation in a way that suits
their needs.  There are three pre-defined tenants on every ACI fabric:

* **common**: policies in this tenant are shared by all tenants. Usually these
  are used for shared services or L4-L7 services.
* **infra**: policies in this tenant are used to influence the operation of the
  fabric overlay
* **mgmt**: policies in this tenant are used to define access to the inband and
  out-of-band management and virtual machine controllers.
 

V
+

**Virtualization**: application of technology used to abstract hardware
resources into virtual representations and allowing software configurability.

**vPC**: virtual Port Channel, in which a port channel is created for link
aggregation, but is spread across multiple physical switches.

**VRF**: Virtual Routing and Forwarding - A L3 namespace isolation methodology
to allow for multiple L3 contexts to be deployed on a single device or
infrastructure.

**VXLAN**: VXLAN is a Layer 2 overlay scheme transported across a Layer 3
network. A 24-bit VXLAN segment ID (SID) or VXLAN network identifier (VNID) is
included in the encapsulation to provide up to 16 million VXLAN segments for
traffic isolation or segmentation. Each segment represents a unique Layer 2
broadcast domain. An ACI VXLAN header is used to identify the policy attributes
if the application endpoint within the fabric, and every packet carries these
policy attributes.

 
X
+

**XML**: eXtensible Markup Language, a markup language that focuses on encoding
data for documents rather than the formatting of the data for those documents.