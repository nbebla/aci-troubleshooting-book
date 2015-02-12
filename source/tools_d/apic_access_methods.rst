APIC Access Methods
===================

There are multiple ways to connect to and manage the ACI fabric and object
model. An administrator can use the built-in Graphical User Interface (GUI),
programmatic methods using an Application Programming Interface (API), or
standard Command Line Interface (CLI). While there are multiple ways to access
the APIC, the APIC is still the single point of truth. All of these access
methods - the GUI, CLI and REST API - are just interfaces resolving to the
API, which is the abstraction of the object model managed by the DME.

GUI
---

One of the primary ways to configure, verify and monitor the ACI fabric is
through the APIC GUI. The APIC GUI is a browser-based HTML5 application that
provides a representation of the object model and would be the most likely
default interface that people would start with. GUI access is accessible
through a browser at the URL https://<APIC IP>
The GUI does not expose the underlying policy object model. One of the
available tools for browsing the MIT in addition to leveraging the CLI is
called “visore” and is available on the APIC and nodes. Visore supports
querying by class and object, as well as easily navigating the hierarchy of
the tree. Visore is accessible through a browser at the URL https://<APIC
IP>/visore.html

API
---

The APIC supports REST API connections via HTTP/HTTPS for processing of
XML/JSON documents for rapid configuration. The API can also be used to verify
the configured policy on the system. This is covered in details in the REST
API chapter.

A common tool used to query the system is a web browser based APP that runs on
Google Chrome (tm) web browser called "Postman".

CLI
---

The CLI can be used in configuring the APIC. It can be used extensively in
troubleshooting the system as it allows real-time visibility of the
configuration, faults, and statistics of the system or alternatively as an
object model browser. Typically the CLI is accessed via SSH with the
appropriate administrative level credentials. The APIC CLI can be accessed as
well through the CIMC KVM (Cisco Integrated Management Console Keyboard Video
Mouse interface).

CLI access is also available for troubleshooting the fabric nodes either
through SSH or the console.

The APIC and fabric nodes are based on a Linux kernel but there are some ACI
specific commands and modes of access that will be used in this book.

CLI MODES:
^^^^^^^^^^

APIC:
"""""

The APIC has fundamentally only one CLI access mode. The commands used in this
book are assuming admininistrave level access to the APIC by use of the admin
user account.

Fabric Node:
""""""""""""

The switch running ACI software has several different modes that can be used
to access different levels of information on the system:

* CLI - The CLI will be used to run NX-OS and Bash shell commands to check the
  concrete models on the switch. For example show vlan, show endpoint, etc. In
  some documentation this may have been referred to as Bash, iBash, or iShell.
* vsh_lc - This is the line card shell and it will be used to check line card
  processes and forwarding tables specific to the Application Leaf Engine (ALE)
  ASIC.
* Broadcom Shell - This shell is used to view information on the Broadcom
  ASIC. The shell will not be covered as it falls outside the scope of this
  book as its assumed troubleshooting at a Broadcom Shell level should be
  performed with assistance of Cisco Technical Assistance Center (TAC). Virtual
  Shell
* (VSH): Provides deprecated NX-OS CLI shell access to the switch. This mode
  can provide output on a switch in ACI mode that could be inaccurate. This
  mode is not recommended, not supported, and commands that provide useful
  output should be available from the normal CLI access mode.

Navigating the CLI:
^^^^^^^^^^^^^^^^^^^

There are some common commands as well as some unique differences than might
be seen in NX-OS on a fabric node. On the APIC, the command structure has
common commands as well as some unique differences compared to Linux Bash.
This section will present a highlight of a few of these commands but is not
meant to replace existing external documentation on Linux, Bash, ACI, and
NX-OS.

Common Bash commands:
"""""""""""""""""""""

When using the CLI, some basic understanding of Linux and Bash is necessary.
These commands include:

* **man** – prints the online manual pages. For example, man cd will display
* **what** the command cd does
* **ls** – list directory contents
* **cd** – change directory
* **cat** – print the contents of a file less – simple navigation tool for
  displaying the contents of a file
* **grep** – print out a matching line from a file
* **ps** – show current running processes – typically used with the options
  **ps –ef**
* **netstat** – display network connection status.  **netstat –a** will display
  active and ports which the system is listening on
* **ip route show** – displays the kernel route table. This is useful on the
  APIC but not on the fabric node
* **pwd** – print the current directory

Common CLI commands:
""""""""""""""""""""

Beyond the normal NX-OS commands on a fabric node, there are several more that
are specific commands to ACI. Some CLI commands referenced in this guide are
listed below:

* **acidiag** - Specifically **acidiag avread** and **acidiag fnvread** are two
  common commands to check the status of the controllers and the fabric nodes
* **techsupport** – CLI command to collect the techsupport files from the
  device
* **attach** – From the APIC, opens up a ssh session to the names node. For
  example **attach rtp_leaf1**
* **iping**/**itraceroute** – Fabric node command used in place of
  ping/traceroute which provides similar functionality against an fabric device
  address and VRF. Note that the Bash ping and traceroute commands do work but
  are effective only for the switch OOB access.

Help:
"""""

When navigating around the APIC CLI, there are some differences when
compared to NX-OS.

* <ESC><ESC> - similar to NX-OS “?” to get a list of command options and
  keywords.
* <TAB> - autocomplete of the command. For example **show int**<TAB> will
  complete to **show interface**.
* **man** <command> - displays the manual and usage output for the command.\
