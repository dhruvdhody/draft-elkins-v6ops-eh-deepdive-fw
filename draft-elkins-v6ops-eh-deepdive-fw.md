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

## Fundamental Premises

   Yet, there are some overriding principles.

   The blockage may be:

   - in the source network
   - in the destination network
   - in a transit network

   Then:

   - it may be blocked intentionally
   - it may be blocked unintentionally

   Intentional blocks are easier to assess.  The block is an
   administrator or network policy.  Of course, the policy may come
   about as a result of a misunderstanding of the function of EHs or
   lack of effective guidance but nonetheless, this is an understandable
   decision.

   The more troubling causes of EH blocks include:

   - bugs
   - default configurations or policies by the vendor
   - lack of support of EH or IPv6 itself

   As far as the blocking component itself (whether intentional or
   unintentional):

   - may be a router
   - may be a firewall
   - may be a load balancer
   - may be a proxy
   - may be a Host OS
   - may be a DNS or other configuration setting

   Note: A DNS or other configuration setting may block IPv6 or prefer
   IPv4.  If not tested correctly, lack of support for IPv6 itself may
   incorrectly appear as lack of support for EHs.

   Finally, the blockage or source may differ based on the type of EH.
   Some EHs are limited to an administrative domain, some EHs are
   processed at every hop, still others are from the source and
   destination.  Problem isolation techniques will differ for the
   various classes of EH.

   Our final document in this series will be a BCP to indicate which EH
   should be allowed, blocked, encrypted, or authenticated and at which
   component or platform.

   Note: {{?RFC9288}} "Recommendations on the Filtering of IPv6 Packets
   Containing IPv6 Extension Headers at Transit Routers" focuses on the
   IPv6 EH handling at transit routers only.  Our approach is to produce
   a final BCP with various recommendations across network segments,
   once the nature of the problems and techniques for isolation are well
   known.
   
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
