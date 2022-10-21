---
coding: utf-8

title: Updated Common YANG Data Types for Traffic Engineering

abbrev: Yang updates for TE Types
docname: draft-ietf-teas-rfc8776-update-01
obsoletes: 8776
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

Editors' note: Copy the text from {{!RFC8776}} and merge it with the content of this section before WG LC if the RFC8876-bis approach is confirmed.

   This document updates RFC 8776 with a new revision of the module
   ietf-te-types.

--- middle

# Introduction

After the publication of {{!RFC8776}}, a new typedef and a new grouping to ietf-te-types have been defined. Given their broad applicability this document defines them as part of the ietf-te-types YANG model.

Editors' note: Copy the text from {{!RFC8776}} and merge it with the content of this section before WG LC if the RFC8876-bis approach is confirmed.

NOTE: These definitions have been developed in {{?I-D.ietf-teas-yang-te}} and {{?I-D.ietf-teas-yang-l3-te-topo}} and are quite mature: {{?I-D.ietf-teas-yang-te}} in particular is ready from WG Last Call.

RFC Editor: remove the note above and this note

## Requirements Notation

{::boilerplate bcp14}

## Terminology

   The terminology for describing YANG data models is found in
   {{!RFC7950}}.

## Prefixes in Data Node Names

  In this document, names of data nodes and other data model objects
  are prefixed using the standard prefix associated with the
  corresponding YANG imported modules, as shown in {{tab-prefixes}}.

| Prefix          | YANG module          | Reference
| yang            | ietf-yang-types      | {{!RFC6991}}
| inet            | ietf-inet-types      | {{!RFC6991}}
| rt-types        | ietf-routing-types   | {{!RFC8294}}
| te-types        | ietf-te-types        | RFCXXXX
| te-packet-types | ietf-te-packet-types | RFCXXXX
{: #tab-prefixes title="Prefixes and corresponding YANG modules"}

RFC Editor Note: Please replace XXXX with the RFC number assigned to this document.

# Acronyms and Abbreviations

Editors' note: Copy the text from {{!RFC8776}} before WG LC if the RFC8876-bis approach is confirmed.

{: #overview}

# Overview

## TE Types Module Contents

Editors' note: Copy the text from {{!RFC8776}} and merge it with the content of this section before WG LC if the RFC8876-bis approach is confirmed.

   The module ietf-te-types has been updated to add the following
   YANG identies, types and groupings which can be reused by TE YANG models:

bandwidth-scientific-notation
: This types represents the bandwidth in
bit-per-second, using the scientific notation (e.g., 10e3).

encoding-and-switching-type
: This is a common grouping to define the LSP encoding and switching types.

## Packet TE Types Module Contents

Editors' note: Copy the text from {{!RFC8776}} before WG LC if the RFC8876-bis approach is confirmed.

{: #yang-code}

# TE Types YANG Module

Editors' note: Copy the text from {{!RFC8776}} and merge it with the content of this section before WG LC if the RFC8876-bis approach is confirmed.

This section provides the updated revision of the "ietf-te-types"
YANG module.

NOTE: Only the typedef bandwidth-scientific-notation and 
the grouping encoding-and-switching-type have been added
in this module revision. Please focus your review on this part. See also {{yang-diff}}.

RFC Editor: remove the note above and this note

~~~~ yang
{::include ../../ietf-te-types.yang}
~~~~
{: #fig-pc-yang title="TE Types YANG module"
sourcecode-markers="true" sourcecode-name="ietf-te-types@2022-03-25.yang"}

# Packet TE Types YANG Module

Editors' note: Copy the text from {{!RFC8776}} before WG LC if the RFC8876-bis approach is confirmed.

# IANA Considerations

For the following URIs in the "IETF XML Registry" {{?RFC3688}}, IANA has updated the reference field to refer to this document:

~~~~
      URI: urn:ietf:params:xml:ns:yang:ietf-te-types
      Registrant Contact:  The IESG.
      XML: N/A, the requested URI is an XML namespace.

      URI: urn:ietf:params:xml:ns:yang:ietf-te-packet-types
      Registrant Contact:  The IESG.
      XML: N/A, the requested URI is an XML namespace.
~~~~

This document also adds updated YANG modules to the "YANG Module
Names" registry {{!RFC7950}}:

~~~~
      name:      ietf-te-types
      namespace: urn:ietf:params:xml:ns:yang:ietf-te-types
      prefix:    te-types
      reference: RFC XXXX

      name:      ietf-te-packet-types
      namespace: urn:ietf:params:xml:ns:yang:ietf-te-packet-types
      prefix:    te-packet-types
      reference: RFC XXXX
~~~~

RFC Editor Note: Please replace XXXX with the RFC number assigned to this document.

# Security Considerations

Editors' note: Copy the text from {{!RFC8776}} before WG LC if the RFC8876-bis approach is confirmed.

The security considerations defined in section 7 of {{!RFC8776}} applies to the
revision of the ietf-te-types YANG module.

This document just adds new typedefs and groupings to the YANG modules defined in
{{!RFC8776}} and therefore it does not introduce additional considerations.

--- back

{: #changes-bis}

# Changes from RFC 8776

To be added in a future revision of this draft.

{: #yang-diff}

## TE Types YANG Diffs

This section provides the diff between the YANG module in section 3.1 of {{!RFC8776}} and the YANG model revision in {{yang-code}}.

The intention of this appendix is to facilitate focusing the review of the YANG model in {{yang-code}} to the changes compared with the YANG model in {{!RFC8776}}.

Editors note, please remove this appendix before publication.

Note - This diff has been generated using the following UNIX commands to compare the YANG module revisions in section 3.1 of {{!RFC8776}} and in {{yang-code}}:

~~~~~
diff ietf-te-types@2020-06-10.yang ietf-te-types.yang > model-diff.txt
sed 's/^/    /' model-diff.txt > model-diff-spaces.txt
sed 's/^    >   /    >   /' model-diff-spaces.txt > model-updates.txt
~~~~~

The output (model-updates.txt) is reported here:

{::include ./model-updates.txt}

{: #options}

# Option Considered for updating RFC8776

The concern is how to be able to update the ietf-te-types YANG module published in {{!RFC8776}} without delaying too much the progress of the mature WG documents.

Three possible options have been identified to address this concern.

One option is to keep these definitions in the YANG modules where they have initially been defined: other YANG modules can still import them. The drawback of this approach is that it defeating the value of common YANG modules like ietf-te-types since common definitions will be spread around multiple specific YANG modules.

A second option is to define them in a new common YANG module (e.g., ietf-te-types-ext). The drawback of this approach is that it will increase the number of YANG modules providing tiny updates to the ietf-te-types YANG module.

A third option is to develop a revision of the ietf-te-types YANG module within an RFC8776-bis. The drawback of this approach is that the process for developing a big RFC8776-bis just for a tiny update is too high. Moreover, as suggested during IETF 113 Netmod WG discussion, a new revision of the ietf-te-packet-types YANG module, which is also defined in {{!RFC8776}} but it does not need to be revised, needs to be published just to change its reference to RFC8776-bis (see {{?RFC9314}}).

A fourth option, considered in the -00 WG version, was to:

- describe within the document only the updates to the ietf-te-types YANG module proposed by this document;

- include the whole updated YANG model within the main body;

- add some notes, to be removed before publication, within updated YANG model to focus the review only to the updates to the ietf-te-types YANG module proposed by this document.

Based on the feedbacks from IETF 114 discussion, this version has been restructured to become an RFC8776-bis, with some notes, to be removed before publication, to focus the review only to the updates to the ietf-te-types YANG module proposed by this document.

During the Netmod WG session at IETF 114, an alternative process has been introduced:

https://datatracker.ietf.org/meeting/114/materials/slides-114-netmod-ad-topic-managing-the-evolution-of-ietf-yang-modules-00.pdf

Future updates of this document could align with the proposed approach.

Therefore, in order to avoid useless editorial work, this version of the document has been structured to become an RFC8776-bis but not all the existing text in {{!RFC8776}} has been copied: some editors' notes has been inserted instead. These editors' note will be removed and replaced by actual text copied from {{!RFC8776}} before WG LC if the RFC8776-bis approach is confirmed.

Editors note, please remove this appendix before publication.

{: numbered="false"}

# Acknowledgements

The authors would like to thank 
Robert Wilton, Lou Berger, Mahesh Jethanandani and Jeff Haas
for their valuable input to the discussion
about the process to follow to provide tiny updates to a YANG module already published as an RFC.

   This document was prepared using kramdown.
