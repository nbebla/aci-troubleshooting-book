**********************************
Application Centric Infrastructure
**********************************

.. contents::
   :local:
   :depth: 2

In the same way that humans build relationships to communicate and share their
knowledge, computer networks are built to allow for nodes to exchange data at
ever increasing speeds and rates. The drivers for these rapidly growing
networks are the applications, the building blocks that consume and provide the
data which are close to the heart of the business lifecycle. The
organizations tasked with nurturing and maintaining these expanding networks,
nodes and vast amounts of data, are critical to those that consume the
resources they provide.

IT organizations have managed the conduits of this data as network devices
with each device being managed individually. In the efforts to support an
application, a team or multiple teams of infrastructure specialists build and
configure static infrastructure including the following:

* Physical infrastructure (switches, ports, cables, etc.)
* Logical topology (VLANs, L2 interfaces and protocols, L3 interfaces and
  protocols, etc.)
* Access control configuration (permit/deny ACLs) for application integration
  and common services)
* Quality of Service configuration
* Services integration (firewall, load balancing, etc.)
* Connecting application workload engines (VMs, physical servers, logical
  application instances)

Cisco seeks to innovate the way this infrastructure is governed by introducing
new paradigms. Going from a network of individually managed devices to an
automated policy-based model that allows an organization to define the policy,
and the infrastructure to automate the implementation of the policy in the
hardware elements, will change the way the world communicates.

To this end, Cisco has introduced **Application Centric Infrastructure**, or
**ACI**, as an holistic systems-based approach to infrastructure management.

The design intent of ACI is to provide the following:

* Application-driven policy modeling
* Centralized policy management and visibility of infrastructure and
  application health
* Automated infrastructure configuration management
* Integrated physical and virtual infrastructure management
* Open interface to enable flexible software and ecosystem partner integration
* Seamless communications from any endpoint to any endpoint

There are multiple possible implementation options for an ACI fabric:

* Leveraging a network centric approach to policy deployment - in this case a
  full understanding of application interdependencies is not critical, and
  instead the current model of a network-oriented design is maintained. This
  can take one of two forms:
  
  - L2 Fabric – Uses the ACI policy controller to automate provisioning of
    network infrastructure based on L2 connectivity between connected network
    devices and hosts.
  - L3 Fabric – Uses the ACI policy model to automate provisioning network
    infrastructure based on L3 connectivity between network devices and hosts.
    
* Application-centric fabric – takes full advantage of all of the ACI objects
  to build out a flexible and completely automated infrastructure including L2
  and L3 reachability, physical machine and VM connectivity integration,
  service node integration and full object manipulation and management.
* Implementations of ACI that take full advantage of the intended design from
  an application-centric perspective allow for end-to-end network automation
  spanning physical and virtual network and network services integration.

All of the manual configuration and integration work detailed above is thus
automated based on policy, therefore making the infrastructure team’s efforts
more efficient.

Instead of manually configuring VLANs, ports and access lists for every device
connected to the network, the policy is created and the infrastructure itself
resolves and provisions the relevant configuration to be provisioned on demand,
where needed, when needed. Conversely, when devices, applications or workloads
detach from the fabric, the relevant configuration can be de-provisioned,
allowing for optimal network hygiene.

Cisco ACI follows a model-driven approach to configuration management. This
model-based configuration is disseminated through the managed nodes using the
concept of Promise Theory.

Promise Theory is a management model in which a central intelligence system
declares a desired configuration “end-state”, and the underlying objects act
as autonomous intelligent agents that can understand the declarative end-state
and either implement the required change, or send back information on why it
could not be implemented.

In ACI, the intelligent agents are purpose-built elements of the
infrastructure that take an active part in its management by the keeping of
"promises". Within promise theory, a promise is an agent’s declaration of
intent to follow an intended instruction defining operational behavior. This
allows management teams to create an abstract “end-state” model and the system
to automate the configuration in compliance. With declarative end-state
modeling, it is easier to build and manage networks of all scale sizes with
less effort.

Many new ideas, concepts and terms come with this coupling of ACI and Promise
Theory. This book is not intended to be a complete tutorial on ACI or Promise
Theory, nor is it intended to be a complete operations manual for ACI, or a
complete dictionary of terms and concepts. Where possible, however, a base
level of definitions will be provided, accompanied by explanations. The goal
is to provide common concepts, terms, models and fundamental features of the
fabric, then use that base knowledge to dive into troubleshooting methodology
and exercises.

To read more information on Cisco's Application Centric Infrastructure, the
reader may refer to the Cisco website at https://www.cisco.com/go/aci.
   