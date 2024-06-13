---
layout: page
title: PMIx Standard
permalink: /standard
---

PMIx Standard Releases
----------------------

The following versions of the PMIx Standard document are available:

Direct repository link to the [latest release](https://github.com/pmix/pmix-standard/releases/latest).

-   Version 5.0 (May 2023)
    -   [Local website](/uploads/2023/05/pmix-standard-v5.0.pdf)
    -   [Repository release](https://github.com/pmix/pmix-standard/releases/tag/v5.0)
-   Version 4.2 (May 2024)
    -   [Local website](/uploads/2024/05/pmix-standard-v4.2.pdf)
    -   [Repository release](https://github.com/pmix/pmix-standard/releases/tag/v4.2)
-   Version 4.1 (Oct 2021)
    -   [Local website](/uploads/2021/10/pmix-standard-v4.1.pdf)
    -   [Repository release](https://github.com/pmix/pmix-standard/releases/tag/v4.1)
-   Version 4.0 (Dec 2020)
    -   [Local website](/uploads/2020/12/pmix-standard-v4.0.pdf)
    -   [Repository release](https://github.com/pmix/pmix-standard/releases/tag/v4.0)
-   Version 3.1 (Feb 2019)
    -   [Local website](/uploads/2019/02/pmix-standard-3.1.pdf)
    -   [Repository release](https://github.com/pmix/pmix-standard/releases/tag/v3.1)
-   Version 3.0 (Dec 2018)
    -   [Local website](/uploads/2018/12/pmix-standard-3.0.pdf)
    -   [Repository release](https://github.com/pmix/pmix-standard/releases/tag/v3.0)
-   Version 2.2 (Feb. 2019)
    -   [Local website](/uploads/2019/02/pmix-standard-2.2.pdf)
    -   [Repository release](https://github.com/pmix/pmix-standard/releases/tag/v2.2)
-   Version 2.1 (Dec 2018)
    -   [Local website](/uploads/2018/12/pmix-standard-2.1.pdf)
    -   [Repository release](https://github.com/pmix/pmix-standard/releases/tag/v2.1)
-   Version 2.0 (Sept. 2018)
    -   [Local website](/uploads/2018/09/pmix-standard.pdf)
    -   [Repository release](https://github.com/pmix/pmix-standard/releases/tag/v2.0)

You can track [current developments](/contribute) on the community resources for contributors.

Expectations attached with the PMIx Standard
--------------------------------------------

While an implementor of the PMIx library itself must at least include the
standard PMIx headers and instantiate each function, they are free to
return “not supported” for many function they choose not to implement.

This also applies to the host environments. Resource managers and other
system management stack components retain the right to decide on support
of a particular function. The PMIx community highlights functions
that are critical to basic application execution (e.g., PMIx\_Get),
while leaving flexibility for tailoring a vendor’s software for their
target market segment.

Similarly, while a PMIx library implementor, or an SMS component server, may choose
to support a particular PMIx API, they are not *required* to support
every attribute that might apply to it. This would pose a significant
barrier to entry for an implementor as there can be a broad range of
applicable attributes to a given API, at least some of which may rarely
be used. The PMIx community is attempting to help differentiate the
attributes by indicating those that are generally used (and therefore,
of higher importance to support) vs those that a “complete
implementation” would support.

Note that an environment that does not include support for a particular
attribute/API pair is not “incomplete” or of lower quality than one that
does include that support. Vendors must decide where to invest their
time based on the needs of their target markets, and it is perfectly
reasonable for them to perform cost/benefit decisions when considering
what functions and attributes to support.

The flip side of that statement is also true: Users who find that their
current vendor does not support a function or attribute they require may
raise that concern to their vendor and request that the implementation
be expanded. Alternatively, users may wish to utilize the PMIx Reference
Server as a “shim” between their application and the host environment as
it might provide the desired support until the vendor can respond.
Finally, in the extreme, one can exploit the portability of PMIx-based
application to change vendors.

Quick Summary of features per version
-------------------------------------

This list presents a short summary of features added during different
iterations of the PMIx standard. In recent [revisions of the standard
document](#pmix-standard-releases), a full changelog is provided that
contains a complete list of changes.

#### PMIx v1

The initial version of the standard, released in late 2015, covers the
basic functions required to launch and wireup a parallel application.
This includes the following APIs:

-   Client APIs
    -   PMIx\_Init, PMIx\_Initialized, PMIx\_Abort, PMIx\_Finalize
    -   PMIx\_Put, PMIx\_Commit, PMIx\_Fence, PMIx\_Get
    -   PMIx\_Publish, PMIx\_Lookup, PMIx\_Unpublish
    -   PMIx\_Spawn, PMIx\_Connect, PMIx\_Disconnect
    -   PMIx\_Resolve\_nodes, PMIx\_Resolve\_peers
-   Server APIs
    -   PMIx\_server\_init, PMIx\_server\_finalize
    -   PMIx\_generate\_regex, PMIx\_generate\_ppn
    -   PMIx\_server\_register\_nspace, PMIx\_server\_deregister\_nspace
    -   PMIx\_server\_register\_client, PMIx\_server\_deregister\_client
    -   PMIx\_server\_setup\_fork, PMIx\_server\_dmodex\_request
-   Common APIs
    -   PMIx\_Get\_version, PMIx\_Store\_internal, PMIx\_Error\_string
    -   PMIx\_Register\_errhandler, PMIx\_Deregister\_errhandler,
        PMIx\_Notify\_error

Note that the last set of APIs (focused on error handlers) was
subsequently replaced in v2 with a more generalized ability to handle
events. In addition, there was a modification made to PMIx\_Init and
PMIx\_Finalize in v2 to extend their flexibility and bring them into
alignment with the PMIx standard practice of including attribute arrays
to support future modifications of behavior.

#### PMIx v2

The second version of the standard, released in mid 2017, extended the
v1 release by adding support for workflow orchestration and tools.

-   Client APIs
    -   PMIx\_Query\_info\_nb, PMIx\_Log\_nb
    -   PMIx\_Allocation\_request\_nb, PMIx\_Job\_control\_nb,
        PMIx\_Process\_monitor\_nb
-   Server APIs
    -   PMIx\_server\_setup\_application,
        PMIx\_server\_setup\_local\_support
-   Tool APIs
    -   PMIx\_tool\_init, PMIx\_tool\_finalize
-   Common APIs
    -   PMIx\_Register\_event\_handler,
        PMIx\_Deregister\_event\_handler, PMIx\_Notify\_event
    -   PMIx\_Proc\_state\_string, PMIx\_Scope\_string,
        PMIx\_Persistence\_string
    -   PMIx\_Data\_range\_string, PMIx\_Info\_directives\_string,
        PMIx\_Data\_type\_string
    -   PMIx\_Alloc\_directive\_string
    -   PMIx\_Data\_pack, PMIx\_Data\_unpack, PMIx\_Data\_copy,
        PMIx\_Data\_print, PMIx\_Data\_copy\_payload

Descriptions of these APIs are provided in the v2 RFCs shown below.

#### PMIx v3

The third version of the standard, released in July 2018, focused on
completion of “instant on” support, further support for tools and
debuggers, and extension to support fabric and storage manager
integration.

-   Client APIs
    -   PMIx\_Log
    -   PMIx\_Get\_credential, PMIx\_Validate\_credential
    -   PMIx\_IOF\_pull, PMIx\_IOF\_deregister, PMIx\_IOF\_push
    -   PMIx\_Allocation\_request, PMIx\_Job\_control,
        PMIx\_Process\_monitor
-   Server APIs
    -   PMIx\_server\_IOF\_deliver
    -   PMIx\_server\_collect\_inventory,
        PMIx\_server\_deliver\_inventory
-   Tool APIs
    -   PMIx\_tool\_connect\_to\_server
-   Common APIs
    -   PMIx\_IOF\_channel\_string

#### PMIx v4

The fourth version of the standard, v4.0 released in December 2020 focused on
providing schedulers with access to point-to-point communication cost information along with providing
general access to network topology graphs, completion of debugger tool
support, the initial support for storage requests, and support for the
new PMIx Groups concept (in collaboration with the MPI Sessions Working
Group). In addition, Python bindings for the PMIx APIs were 
introduced in this release.

v4.1 released October 2022 added a chapter to manage data storage.

v4.2 still under development will backport some of v5 features
(in particular deprecation of macros and introduction of ABI compatible
functions) and some erratas. 

#### PMIx v5

The fifth version of the standard, released in May 2023, focused on
defining a common PMIx ABI by assigning specific values to defined
constants. A Use-Cases appendix was added to give examples of how PMIx
APIs are used in existing software. PMIx Standard v5 was the first
version approved using the procedures defined in the [PMIx Governance
v1.7 document](https://github.com/pmix/governance/releases/tag/v1.7).

-   Client APIs
    - PMIx\_Topology\_destruct
-   Common APIs
    - PMIx\_Data\_embed
    - PMIx\_Value\_load
    - PMIx\_Value\_unload
    - PMIx\_Value\_xfer
    - PMIx\_Info\_list\_start
    - PMIx\_Info\_list\_add
    - PMIx\_Info\_list\_xfer
    - PMIx\_Info\_list\_convert
    - PMIx\_Info\_list\_release

Historical Standardization Process
----------------------------------

Prior *ad hoc* versions of the standard were embodied in the header
files of the corresponding releases of the PMIx Reference
Implementation. These definitions have been superseded by the formal
documents. Each version of the Standard includes information on all
prior versions (e.g., the Version 2.0 document contains the definitions
from Version 1) and clearly marks all additions/changes incorporated
since the last release. Note that the PMIx Community chose not to
release a Version 1 document due to the delay in getting the formal
Standard document completed.

You can refer to the [historical RFCs standardization process manifesto](/standard/historic)
to review early standardization practices.

