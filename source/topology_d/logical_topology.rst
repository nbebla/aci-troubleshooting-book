Logical Application Topology
============================

To maintain a consistent reference throughout the book, an Application Profile
(AP) was built for a common 3-tier application that was used for every
troubleshooting sample. This AP represents the logical model of the
configuration that was deployed to the fabric infrastructure. The AP includes
all the information required for application connectivity and policy (QoS,
security, SLAs, Layer 4-7 services, logging, etc.).

This particular AP is a logical model built on a common application found in
data centers, which includes a front-end web tier, a middleware application
tier, and a back-end database tier. As the diagram illustrates, the flow of
traffic would be left to right, with client connections coming in to the web
tier, which communicates with the app tier, which then communicates to the
database tier, and returns right to left in reverse fashion.

.. image:: /images/application.jpg
   :width: 750 px
   :align: center
