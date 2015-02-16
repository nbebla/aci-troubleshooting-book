Build object, use object to build policy, reuse policy
======================================================

The inherent model of ACI is built on the premise of object structure,
reference and reuse. In order to build an AP, one must first create the
building blocks with all the relevant information for those objects. Once
those are created, it is possible to build other objects referencing the
originally created objects as well as reuse other objects. As an example, it
is possible to build EPG objects, use those to build an AP object, and reuse
the AP object to deploy to different tenant implementations, such as a
Development Environment AP, a Test Environment AP, and a Production
Environment AP. In the same fashion, an EPG used to construct a Test AP may
later be placed into a Production AP, accelerating the time to migrate from a
test environment into production.

