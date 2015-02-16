Fabric Node Access Methods
==========================

CLI In general, most work within ACI will be done through the APIC using the
access methods listed above. There are, however, times in which one must
directly access the individual fabric nodes (switches). Fabric nodes can be
accessed via SSH using the fabric administrative level credentials. The CLI is
not used for configuration but is used extensively for troubleshooting
purposes. The fabric nodes have a Linux shell along with a CLI interpreter to
run show level commands. The CLI can be accessed through the console port as
well.

Faults The APICs automatically detect issues on the system and records these
as faults. Faults are displayed in the GUI until the underlying issue is
cleared. After faults are cleared, they are retained until they are
acknowledged or until the retaining timer has expired. The fault is composed
of system parameters, which are used to indicate the reason for the failure,
and where the fault is located. Fault messages link to help to understand
possible actions in some cases.
