---
title: "Deep Dive into IPv6 Extension Header Testing"
abbrev: "Deep Dive IPv6 EH"
category: bcp

docname: draft-elkins-v6ops-eh-deepdive-fw-latest
submissiontype: IETF  # also: "independent", "IAB", or "IRTF"
consensus: true
v: 3
area: "OPS"
workgroup: v6ops WG
keyword:
 - EH

author:
 -
    fullname: Nalini Elkins
    organization: Industry Network Technology Council
    abbrev: INT Council
    country: US
    phone: +1 831 234 4232
    email: nalini.elkins@insidethestack.com
 -
    fullname: Michael Ackermann
    organization: Industry Network Technology Council
    abbrev: INT Council
    country: US
    phone: +1 248 703 3600
    email: mackermann@bcbsm.com
    uri: https://www.bcbsm.com
 -
    fullname: Dhruv Dhody
    organization: India Internet Engineering Society
    country: IN
    email: dhruv.ietf@gmail.com
 
--- abstract

IPv6 Extension Header testing is a complex area.  Studies have shown
varying results.  This document proposes a methodology for isolating
the location and reasons for IPv6 Extension Headers blockage.  This
document outlines the basic framework and set of documents which will
follow.


--- middle

# Introduction

## Problem Description

   IPv6 Extension Headers (EHs) may be blocked at various points yet
   show the same symptom.  That is, if an EH is blocked at a router, it
   will appear to the client or measurement technique that the packet is
   dropped.  If an EH is blocked at a load balancer or CDN, the client
   will see the same symptom -- the packet is dropped.

   This is a problem because when the same symptom can be the due to
   multiple factors, incorrect conclusions may be drawn from the
   results.  That is, if, for example, loss of the sense of taste of
   sweetness can be due either to a brain tumor or a minor neurological
   problem, then if someone has a tendency towards hypochondria, they
   may incorrectly bemoan their impending death from a brain tumor when
   it may really be only a minor issue.

   This is the same for EH testing.  If a packet is seen to be dropped
   in measurement, it may only be that there is a bug in the load
   balancer code (for example) and not that EH transmission does not
   work writ large.

   This document proposes a framework to isolate the problem of where
   the packet is being dropped.  This is, however, more easily said than
   done.  There are many components and devices in a network.  Each may
   require a different isolation technique.

   We propose a methdology which starts with the simplest topology and
   grows towards more and more complex, real-world networks.  For
   example, in today's networks, if one attempts to access a well-known
   site such as Facebook.com, one is likely to access a cache server
   managed by a Content Delivery Network (CDN) rather than the origin
   server managed by Facebook.  It is important to isolate the testing
   so that we can determine the exact component which may be blocking
   the EH and why.

   We additionally discuss the potential issues with the type of data
   sent as well as how the way the data is sent for testing may impact
   test results.


# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
