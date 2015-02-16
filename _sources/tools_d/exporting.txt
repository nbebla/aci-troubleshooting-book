Exporting information from the Fabric
=====================================

Techsupport The Techsupport files in ACI capture application logs, system and
services logs, version information, faults, event and audit logs, debug
counters and other command output, then bundle all of that into one file on
the system. This is presented in a single compressed file (tarball) that can
be exported to an external location for off-system processing. Techsupport is
similar to functionality available on other Cisco products that allow for a
simple collection of copious amounts of relevant data from the system. This
collection can be initiated through the GUI or through the CLI using the
command techsupport.

Core Files A process crash on the ACI fabric will generate a core file, which
can be used to determine the reason for why the process crashed. This
information can be exported from the APIC for decoding by Cisco support and
engineering teams.
