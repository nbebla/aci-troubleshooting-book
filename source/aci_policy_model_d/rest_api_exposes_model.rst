REST API just exposes the object model
======================================

REST stands for Representative State Transfer, and is a reference model for
direct object manipulation via HTTP protocol based operations.

The uniform ACI object model places clean boundaries between the different
components that can be read or manipulated in the system. When an object
exists in the tree, whether it is an object that was derived from discovery
(such as a port or module) or from configuration (such as an EPG or policy
graph), the objects then would be exposed via the REST API via a Universal
Resource Indicator (URI). The structure of the REST API calls is shown below
with a couple of examples.

.. image:: /images/rest-api.jpg
   :width: 750 px
   :align: center

The general structure of the REST API commands is seen at the top. Below the
general structure two specific examples of what can done with this structured
URI.

