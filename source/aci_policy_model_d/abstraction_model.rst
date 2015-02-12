Abstraction Model
=================

ACI provides the ability to create a stateless definition of application
requirements. Application architects think in terms of application components
and interactions between such components; not necessarily thinking about
networks, firewalls and other services. By abstracting away the
infrastructure, application architects can build stateless policies and define
not only the application, but also Layer 4 through 7 services and interactions
within applications. Abstraction also means that the policy defining
application requirements is no longer tied to traditional network constructs,
and thus removes dependencies on the infrastructure and increases the
portability of applications.

The application policy model defines application requirements, and based on
the specified requirements, each device will instantiate a set of required
changes. IP addresses become fully portable within the fabric, while security
and forwarding are decoupled from any physical or virtual network attributes.
Devices autonomously and consistently update the state of the network based on
the configured policy requirements set within the application profile
definitions.

