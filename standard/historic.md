---
layout: page
title: PMIx Historical RFC Process
permalink: /standard/historic
---

This page contains an historical overview of the RFC standardization process
used during the early stages of the PMIx development.

**This process is now obsolete, please refer to the [current procedures](/standard)
for standardization.
The rest of this page is verbatim, as it appeared when these procedures were active,
but they are now obsolete.**

Historical PMIx RFC standardization process
-------------------------------------------

The PMIx developer community is currently in an early stage – thus, the
process for *extending* the standard is relatively lightweight compared
to more mature communities. In contrast, the process for *modifying* an
existing definition in the standard is intentionally made to be very,
very hard. This serves both to discourage any breaks in backward
compatibility, and to push proposers to scrutinize and scrub their
proposed extensions to ensure they have provided adequate flexibility
for future uses.

Given the dynamic, fast-moving nature of the community at this time, the
current process for *extending* the standard consists of the following
stages:

-   Create an RFC describing the feature plus any API or attribute
    additions
-   Create a prototype against the PMIx reference library’s *master*
    branch for review (do not commit)
-   Present the RFC/prototype at a weekly developer’s teleconference.
    This is done to give the community an opportunity to consider
    whether or not the proposed extension is acceptable in principal,
    and avoids unnecessary expenditure of effort on proposals that are
    “dead on arrival”
    -   If no objection is raised to the concept, then a comment is
        added to the RFC noting that it has “Concept Approval” and the
        corresponding GitHub label is set
    -   After two presentations without objection, a comment is added to
        the RFC marking it as “Provisionally Accepted”, the
        corresponding GitHub label is set, and the proposal is free to
        move to the next stage
    -   If there is an objection or modification request, the proposer
        will change the RFC/prototype and present again the next week.
        This resets the clock, therefore requiring an additional two
        meetings before moving ahead
-   Once the RFC/prototype has been Provisionally Accepted, the proposer
    is free to merge the prototype into the PMIx reference library’s
    *master* branch. The RFC itself is held “open” in the Provisionally
    Accepted state
-   As the community works with the new code, proposed modifications to
    the RFC may be identified. When this occurs, a new commit is made to
    the RFC with a link to the PR with the proposed prototype
    modifications. Discussion resumes to determine when the prototype
    modifications should be merged into the PMIx reference library’s
    master branch
-   At release time, all Provisionally Accepted RFCs will be
    “finalized”. At this time, the proposer will close the PR and make
    sure the necessary changes have been made to the PMIx standard
    document.

Note that the above process relies heavily on the level of collaboration
in the current PMIx community. No formal voting process is involved, nor
are there “membership” requirements that must be met before someone has
a voice in the process. This is likely to change as the community grows
and matures. However, the expectation is that the standard will also
have matured by that time, and so a slower, more formal process may be
more appropriate.

The process for modifying an existing definition in the standard
utilizes the same first three steps of the extension process. However,
the initial presentation of the RFC/prototype must include:

-   a detailed justification for the change; and
-   an assessment of the impact of the change on the installed community

The amount of information provided should reflect the magnitude of the
proposed change. For example, a minor modification in behavior
associated with an existing attribute would require less explanation
than a change to an existing API. In many cases, proposals to modify
definitions are changed to attribute extensions (i.e., the adding of new
attribute definitions). This reflects the PMIx standard’s philosophy of
adding sufficient flexibility (via an array of pmix\_info\_t directives)
to each API to accommodate future additional or modified behaviors
without perturbing the API itself.

Should the justification prove sufficiently convincing, a Notice of
Impending Change (containing a summary of the proposed change and the
justification) is sent out to the community’s mailing list alerting them
to the proposed modification, and inviting comments. This provides an
opportunity for users and implementors to voice their concerns and
suggest modifications or alternative solutions. Three notices must be
sent prior to a final review of the proposal.

Assuming no objections are raised, a final review of the proposal – and
its justification – is conducted during a developer’s weekly telecon.
The proposal can be accepted, rejected, or pushed back for modification
at that time. If accepted, the change is made to the standard’s document
– this will include both a description of the change, and the
justification for it.

### What is Standardized, and What is *Not* Standardized

No standards body can *require* an implementor to support something in
their standard, and PMIx is no different in that regard. While an
implementor of the PMIx library itself must at least include the
standard PMIx headers and instantiate each function, they are free to
return “not supported” for any function they choose not to implement.

This also applies to the host environments. Resource managers and other
system management stack components retain the right to decide on support
of a particular function. The PMIx community continues to look at ways
to assist SMS implementors in their decisions by highlighting functions
that are critical to basic application execution (e.g., PMIx\_Get),
while leaving flexibility for tailoring a vendor’s software for their
target market segment.

One area where this can become more complicated is regarding the
attributes that provide information to the client process and/or control
the behavior of a PMIx standard API. For example, the PMIX\_TIMEOUT
attribute can be used to specify the time (in seconds) before the
requested operation should time out. The intent of this attribute is to
allow the client to avoid “hanging” in a request that takes longer than
the client wishes to wait, or may never return (e.g., a PMIx\_Fence that
a blocked participant never enters).

If an application (for example) truly relies on the PMIX\_TIMEOUT
attribute in a call to PMIx\_Fence, it should set the **required** flag
in the pmix\_info\_t for that attribute. This informs the library and
its SMS host that it must return an immediate error if this attribute is
not supported. By not setting the flag, the library and SMS host are
allowed to treat the attribute as **optional**, ignoring it if support
is not available.

It is therefore critical that users and application implementors:

-   consider whether or not a given attribute is required, marking it
    accordingly; and
-   check the return status on *all* PMIx function calls to ensure
    support was present and that the request was accepted. Note that for
    non-blocking APIs, a return of PMIX\_SUCCESS only indicates that the
    request had no obvious errors and is being processed – the eventual
    callback will return the status of the requested operation itself.

While a PMIx library implementor, or an SMS component server, may choose
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

PMIx Roadmap
------------

The PMIx Standard is evolving fairly rapidly in response to milestones
associated with delivery of next-generation supercomputers. Accordingly,
the timeline is focused towards completing a broad array of features by
the end of 2019.

PMIx RFCs
---------

-   v2 RFCs
    -   [Basic Tool Interaction Mechanism](/standard/RFC/basic-tool-interaction-mechanism)
    -   [Event Notification](/standard/RFC/event-notification)
    -   [Modification of PMIx\_Connect/Disconnect](/standard/RFC/modification-of-pmix_connect-disconnect)
    -   [Flexible Allocation Support](/standard/RFC/flexible-allocation-support)
    -   [Modify Behavior of PMIx\_Get](/standard/RFC/modify-behavior-of-pmix_get)
    -   [Extended Tool Interaction Support](/standard/RFC/extended-tool-interaction-support)
    -   [Refactor Security Support](/standard/RFC/refactor-security-support)
    -   [Support for Network Interactions](/standard/RFC/support-for-network-interactions)
    -   [Query Time Remaining in Allocation](/standard/RFC/query-time-remaining-in-allocation)
    -   [Job Control and Monitoring](/standard/RFC/job-control-and-monitoring)
    -   [Extend Event Notification](/standard/RFC/extend-event-notification)
    -   [Expose PMIx Buffer Manipulation Functions](/standard/RFC/expose-pmix-buffer-manipulation-functions)
    -   [Acquisition of Subsystem Launch Information](/standard/RFC/acquisition-of-subsystem-launch-information)
-   v3 RFCs
    -   [Security Credential Transactions](/standard/RFC/security-credential-transactions)
    -   [Register Cleanup of Files and Directories](/standard/RFC/register-cleanup-of-files-and-directories)
    -   [IO Forwarding for Tools and Debuggers (provisionally accepted)](/standard/RFC/io-forwarding-for-tools-and-debuggers)
    -   [Environmental Parameter Directives for Applications and Launchers](/standard/RFC/envar-directives-for-applications-and-launchers)
    -   [Coordination Across Programming Models (OpenMP/MPI)](/standard/RFC/coordination-across-programming-models-openmp-mpi)
    -   [Modify the PMIx buffer manipulation APIs](/standard/RFC/modify-the-pmix-buffer-manipulation-apis)
    -   [Extended Debugger Support (in progress)](/standard/RFC/extended-debugger-support)
    -   [DataStore Abstraction Framework (in progress)](/standard/RFC/datastore-abstraction-framework)
    -   [Extension of PMIx Logging Support](/standard/RFC/extension-of-pmix-logging-support)
-   v4 RFCs
    -   [PMIx Support for Storage Systems (in progress)](/standard/RFC/pmix-support-for-storage-systems)
    -   [Support for Launching Applications under Debugger Tools (in progress)](/standard/RFC/support-for-launching-applications-under-debugger-tools)
    -   [PMIx Groups (in progress)](/standard/RFC/pmix-groups-2)
