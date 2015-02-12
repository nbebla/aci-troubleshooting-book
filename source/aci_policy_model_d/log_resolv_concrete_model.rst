Logical model, Resolved model, concrete model
=============================================

Within the ACI object model, there are essentially three stages of
implementation of the model: the Logical Model, the Resolved Model, and the
Concrete Model.

The Logical Model is the logical representation of the objects and their
relationships. The AP that was discussed previously is an expression of the
logical model. This is the declaration of the “end-state” expression that is
desired when the elements of the application are connected and the fabric is
provisioned by the APIC, stated in high-level terms.

The Resolved Model is the abstract model expression that the APIC resolves
from the logical model. This is essentially the elemental configuration
components that would be delivered to the physical infrastructure when the
policy must be executed (such as when an endpoint connects to a leaf).

The Concrete Model is the actual in-state configuration delivered to each
individual fabric member based on the resolved model and the Endpoints
attached to the fabric.

In general, the logical model should be the high-level expression of what
exists in the resolved model, which should be present on the concrete devices
as the concrete model expression. If there is any gap in these, there will be
inconsistent configurations.

