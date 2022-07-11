---
coding: utf-8

title: Updated Common YANG Data Types for Traffic Engineering

abbrev: Yang updates for TE Types
docname: draft-ietf-teas-rfc8776-update-00
updates: 8776
submissiontype: IETF
workgroup: TEAS Working Group
category: std
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
  -
    name: Italo Busi
    org: Huawei
    email: italo.busi@huawei.com
  -
    name: Aihua Guo
    org: Futurewei Technologies
    email: aihuaguo.ietf@gmail.com
  -
    name: Xufeng Liu
    org: IBM Corporation
    email: xufeng.liu.ietf@gmail.com
  -
    name: Tarek Saad
    org: Juniper Networks
    email: tsaad@juniper.net
  -
    name: Rakesh Gandhi
    org: Cisco Systems, Inc.
    email: rgandhi@cisco.com
  -
    name: Vishnu Pavan Beeram
    org: Juniper Networks
    email: vbeeram@juniper.net
  -
    name: Igor Bryskin
    org: Individual
    email: i_bryskin@yahoo.com

#contributor:

--- abstract

   This document defines few additional common data types and groupings
   in YANG data modeling language to be imported by modules that model Traffic
   Engineering (TE) configuration and state capabilities.

   This document updates RFC 8776 with a new revision of the module
   ietf-te-types.

--- middle

# Introduction

After the pubblication of {{!RFC8776}}, the need to add a new typedef and a new grouping to ietf-te-types YANG module has arisen.

These definitions have been developed in {{?I-D.ietf-teas-yang-te}} and {{?I-D.ietf-teas-yang-l3-te-topo}} and are quite mature: {{?I-D.ietf-teas-yang-te}} in particular is ready from WG Last Call.

However, these defintions have broader applicability than the I-D where they have originated, so it makes sense to move them within the ietf-te-types YANG module.

## Requirements Notation

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
   "OPTIONAL" in this document are to be interpreted as described in
   BCP 14 {{!RFC2119}} {{!RFC8174}} when, and only when, they appear in all
   capitals, as shown here.

## Terminology

   The terminology for describing YANG data models is found in
   {{!RFC7950}}.

## Prefixes in Data Node Names

In this document, names of data nodes and other data model objects,
added to the ietf-te-types YANG module do not need to be prefixed.

The revision of the ietf-te-types YANG module uses the prefixes defined in section 1.2 of {{!RFC8776}}.

{: #overview}

# Overview

   The module ietf-te-types has been updated to add the following
   YANG identies, types and groupings which can be reused by TE YANG models:

bandwidth-scientific-notation
: This types represents the bandwidth in
bit-per-second, using the scientific notation (e.g., 10e3).

encoding-and-switching-type
: This is a common grouping to define the LSP encoding and switching types.

{: #yang-code}

# TE Types YANG Module Revision

This section provides the updated revision of the "ietf-te-types"
YANG module.

NOTE: Only the typedef bandwidth-scientific-notation and 
the grouping encoding-and-switching-type have been added
in this module revision. Please focus your review on this part.

RFC Editor: remove the note above and this note


~~~~ yang
{::include ./ietf-te-types.yang}
~~~~
{: #fig-pc-yang title="TE Types YANG module"
sourcecode-markers="true" sourcecode-name="ietf-te-types@2022-03-25.yang"}

# IANA Considerations

This document updates the ietf-te-types YANG module registered by {{!RFC8776}}.

Therefore this document does not require any IANA actions.

# Security Considerations

The security considerations defined in section 7 of {{!RFC8776}} applies to the
revision of the ietf-te-types YANG module.

This document just adds new typedefs and groupings to the YANG modules defined in
{{!RFC8776}} and therefore it does not introduce additional considerations.

--- back

{: numbered="false"}

# Acknowledgements

The authors would like to thank 
Robert Wilton, Lou Berger, Mahesh Jethanandani and Jeff Haas
for their valuable input to the discussion
about the process to follow to provide tiny updates to a YANG module already published as an RFC.

   This document was prepared using kramdown.
