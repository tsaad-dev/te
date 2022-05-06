---
coding: utf-8

title: Updated Common YANG Data Types for Traffic Engineering

abbrev: Yang updates for TE Types
docname: draft-busi-teas-te-types-update-01
updates: 8776
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

## Options considered

The concern is how to be able to update the ietf-te-types YANG module published in {{!RFC8776}} without delaying too much the progress of the mature WG documents.

Three possible options have been identified to address this concern.

One option is to keep these definitions in the YANG modules where they have initially been defined: other YANG modules can still import them. The drawback of this approach is that it defeating the value of common YANG modules like ietf-te-types since common definitions will be spread around multiple specific YANG modules.

A second option is to define them in a new common YANG module (e.g., ietf-te-types-ext). The drawback of this approach is that it will increase the number of YANG modules providing thiny updates to the ietf-te-types YANG module.

A third option is to develop a revision of the ietf-te-types YANG module within an RFC8776-bis. The drawback of this approach is that the process for developing a big RFC8776-bis just for a thiny update is too high. Moreover, it is not clear what could be done with the ietf-te-packet-types YANG module which is also defined in {{!RFC8776}} but it does not need to be revised.

This document explores an alternative option to just update {{!RFC8776}} with a new revision of the module ietf-te-types.

In order to focus the review process of this document only to the changes proposed by this document:
- {{overview}} describes only the updates to the ietf-te-types YANG module proposed by this document;
- {{yang-update}} defines only the diff between the revision of the ietf-te-types YANG module proposed in this document and the revision of the ietf-te-types YANG module published in {{!RFC8776}}.

In order to allow all the YANG toolchain to keep working by extracting the revision of the ietf-te-types YANG module proposed in this document, this revision is provided by {{yang-code}}. This text is intended not to be subject to the review of this document.

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

{: #yang-update}

# TE Types YANG Update

This section provides the diff between the YANG module in section 3.1 of {{!RFC8776}} and the YANG module revision in {{yang-code}}.

Note - This diff has been generated using the following UNIX commands to compare the YANG module revisions in section 3.1 of {{!RFC8776}} and in {{yang-code}}:

~~~~~
diff ietf-te-types@2020-06-10.yang ietf-te-types.yang > model-diff.txt
sed 's/^/    /' model-diff.txt > model-diff-spaces.txt
sed 's/^    >   /    >   /' model-diff-spaces.txt > model-updates.txt
~~~~~

The output (model-updates.txt) is reported here:

{::include ./model-updates.txt}

# IANA Considerations

This document updates the ietf-te-types YANG module registered by {{!RFC8776}}.

Therefore this document does not require any IANA actions.

# Security Considerations

The security considerations defined in section 7 of {{!RFC8776}} applies to the
revision of the ietf-te-types YANG module.

This document just adds new typedefs and groupings to the YANG modules defined in
{{!RFC8776}} and therefore it does not introduce additional considerations.

--- back

{: #yang-code}

# TE Types YANG Module

~~~~
<CODE BEGINS> file "ietf-te-types@2022-03-07.yang"
{::include ./ietf-te-types.yang}
<CODE ENDS>
~~~~


{: numbered="false"}

# Acknowledgements

   This document was prepared using kramdown.
