Organization of this Book
=========================

**Section 1: Introduction to ACI Troubleshooting**
--------------------------------------------------

The introduction covers basic concepts, terms and models while introducing the
tools that will be used in troubleshooting. Also covered are the
troubleshooting, verification and resolution methodologies used in later
sections that cover the actual problems being documented.

**Section 2: Sample Reference Topology**
----------------------------------------

This section sets the baseline sample topology used throughout all of the
troubleshooting exercises that are documented later in the book. Logical
diagrams are provided for the abstract policy elements (the endpoint group
objects, the application profile objects, etc) as well as the physical
topology diagrams and any supporting documentation that is needed to
understand the focal point of the exercises.  In each problem description in
Section 3, references will be made to the reference topology as necessary.
Where further examination is required, the specific aspects of the topology
being examined may be re-illustrated in the text of the troubleshooting
scenario.

**Section 3: Troubleshooting Application Centric Infrastructure**
-----------------------------------------------------------------

The Troubleshooting ACI section goes through specific problem descriptions as
it relates to the fabric. For each iterative problem, there will be a problem
description, a listing of the process, some verification steps, and possible
resolutions.

**Chapter format**: The chapters that follow in the Troubleshooting section
document the various problems: verification of causes and possible resolutions
are arranged in the following format.

**Overview**: Provides an introduction to the problem in focus by highlighting
the following information:

* Theory and concepts to be covered
* Information of what should be happening
* Verification steps of a working state

**Problem Description**: The problem description will be a high level
observation of the starting point for the troubleshooting actions to be
covered. Example:  a fabric node is showing “inactive” from the APIC by
using APIC CLI command acidiag fnvread.

**Symptoms**: Depending on the problem, various symptoms and their impacts may
be observed. In this example, some of the symptoms and indications of issues
around an inactive fabric node could be:

* loss of connectivity to the fabric
* low health score
* system faults
* inability to make changes through the APIC

In some chapters, multiple symptoms could be observed for the same problem
description that require different verification or resolution.

**Verification**: The logical set of steps to identify what is being observed
will be indicated along with the appropriate tools and output. Additionally,
some information on likely causes and resolution will be included.
