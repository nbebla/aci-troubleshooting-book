Declarative End State and Promise Theory
========================================

For many years, infrastructure management has been built on a static and
inflexible configuration paradigm. In terms of theory, traditional
configuration via traditional methods (CLI configuration of each box
individually) where configuration must be done on every device for every
possibility of every thing prior to this thing connecting, is termed an
Imperative Model of configuration. In this model, due to the way configuration
is built for eventual possibility, the trend is to overbuild the
infrastructure configuration to a fairly significant amount. When this is
done, fragility and complexity increase with every eventuality included.

.. image:: /images/traditional policy.jpg
   :width: 750 px
   :align: center

Similar to what is illustrated above, if configuration must be made on a
single port for an ESXi host, it must be configured to trunk all information
for all of the possible VLANs that might get used by a vSwitch or DVS on the
host, whether or not a VM actually exists on that host. On top of that,
additional ACLs may need to be configured for all possible entries on that
port, VLAN or switch to allow/restrict traffic to/from the VMs that might end
up migrating to that host/segment/switch. That is a fairly heavyweight set of
tasks for just some portions of the infrastructure, and that continues to
build as peripheral aspects of this same problem are evaluated. As these
configurations are built, hardware resource tables are filled up even if they
are not needed for actual forwarding. Also reflected are configurations on the
service nodes for eventualities that can build and grow, many times being
added but rarely ever removed. This eventually can grow into a fairly fragile
state that might be considered a form of firewall house of cards. As these
building blocks are built up over time and a broader perspective is taken, it
becomes difficult to understand which ones can be removed without the whole
stack tumbling down. This is one of the possible things that can happen when
things are built on an imperative model.

.. image:: /images/policy model theory.jpg
   :width: 750 px
   :align: center

On the other hand, a declarative mode allows a system to describe the
“end-state” expectations system-wide as depicted above, and allows the system
to utilize its knowledge of the integrated hardware and automation tools to
execute the required work to deliver the end state. Imagine an infrastructure
system where statements of desire can be made, such as “these things should
connect to those things and let them talk in this way”, and the infrastructure
converges on that desired end state. When that configuration is no longer
needed, the system knows this and removes that configuration.

.. image:: /images/promise-theory.jpg
   :width: 750 px
   :align: center

Promise Theory is built on the principles that allow for systems to be
designed based on the declarative model. It’s built on voluntary execution by
autonomous agents which provide and consume services from one another based on
promises.

As the IT industry continues to build and scale more and more, information and
systems are rapidly reaching breaking points where scaled-out infrastructure
cannot stretch to the hardware resources without violating the economic
equilibrium, nor scale-in the management without integrated agent-based
automation. This is why Cisco ACI, as a system built on promise theory, is a
purpose-built system for addressing scale problems that are delivery
challenges with traditional models.

