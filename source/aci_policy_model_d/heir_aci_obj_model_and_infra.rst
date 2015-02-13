Hierarchical ACI Object Model and the Infrastructure
====================================================

The APIC manages a distributed managed information tree (dMIT). The dMIT
discovers, manages, and maintains the whole hierarchical tree of objects in
the ACI fabric, including their configuration, operational status, and
accompanying statistics and associated faults.

The Cisco ACI object model structure is organized around a hierarchical tree
model, called a distributed Management Infrastructure Tree (dMIT). The dMIT is
the single source of truth in the object model, and is used in discovery,
management and maintenance of the hierarchical model, including configuration,
operational status and accompanying statistics and faults.

As mentioned before, within the dMIT, the Application Profile is the modeled
representation of an application, network characteristics and connections,
services, and all the relationships between all of these lower-level objects.
These objects are instantiated as Managed Objects (MO) and are stored in the
dMIT in a hierarchical tree, as shown below:

.. image:: /images/dmit.jpg
   :width: 750 px
   :align: center

|

All of the configurable elements shown in this diagram are represented as
classes, and the classes define the items that get instantiated as MOs, which
are used to fully describe the entity including its configuration, state,
runtime data, description, referenced objects and lifecycle position.

Each node in the dMIT represents a managed object or group of objects. These
objects are organized in a hierarchical structure, similar to a structured
file system with logical object containers like folders. Every object has a
parent, with the exception of the top object, called “root”, which is the top
of the tree. Relationships exist between objects in the tree.

.. image:: /images/mo-tree.jpg
   :width: 750 px
   :align: center

|

Objects include a class, which describes the type of object such as a port,
module or network path, VLAN, Bridge Domain, or EPG. Packages identify the
functional areas to which the objects belong. Classes are organized
hierarchically so that, for example, an access port is a subclass of the class
Port, or a leaf node is a subclass of the class Fabric Node.

Managed Objects can be referenced through relative names (Rn) that consist of
a prefix matched up with a name property of the object. As an example, a
prefix for a Tenant would be “tn” and if the name would be “Cisco”, that would
result in a Rn of “tn-Cisco” for a MO.

Managed Objects can also be referenced via Distinguished Names (Dn), which is
the combination of the scope of the MO and the Rn of the MO, as mentioned
above. As an example, if there is a tenant named “Cisco” that is a policy
object in the top level of the Policy Universe (polUni), that would combine to
give us a Dn of “uni/tn-Cisco”. In general, the DN can be related to a fully
qualified domain name.

Because of the hierarchical nature of the tree, and the attribute system used
to identify object classes, the tree can be queried in several ways for MO
information. Queries can be performed on an object itself through its DN, on a
class of objects such as switch chassis, or on a tree-level, discovering all
members of an object.

The structure of the dMIT provides easy classification of all aspects of the
relevant configuration, as the application objects are organized into related
classes, as well as hardware objects and fabric objects into related classes
that allow for easy reference, reading and manipulation from individual object
properties or multiple objects at a time by reference to a class. This allows
configuration and management of multiple similar components as efficiently as
possible with a minimum of iterative static configuration.

