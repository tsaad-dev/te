---
coding: utf-8

title: Common YANG Data Types for Traffic Engineering

abbrev: TE Common YANG Types
docname: draft-ietf-teas-rfc8776-update-10
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
    org: Alef Edge
    email: xufeng.liu.ietf@gmail.com
  -
    name: Tarek Saad
    org: Cisco Systems Inc.
    email: tsaad.net@gmail.com
  -
    name: Igor Bryskin
    org: Individual
    email: i_bryskin@yahoo.com

contributor:
  -
    name: Vishnu Pavan Beeram
    org: Juniper Networks
    email: vbeeram@juniper.net
  -
    name: Rakesh Gandhi
    org: Cisco Systems, Inc.
    email: rgandhi@cisco.com

normative:
  ITU_G.808.1:
    title: Generic protection switching - Linear trail and subnetwork protection
    author:
      org: ITU-T Recommendation G.808.1
    date: May 2014
    seriesinfo: ITU-T G.808.1
    target: https://www.itu.int/rec/T-REC-G.808.1

informative:
  MEF_10.3:
    title: Ethernet Services Attributes Phase 3
    author:
      org: MEF
    date: October 2013
    seriesinfo: MEF 10.3


  ITU-T_G.709:
    title: Interfaces for the optical transport network
    author:
      org: International Telecommunication Union
    date: June 2020
    seriesinfo: ITU-T G.709
    target: https://www.itu.int/rec/T-REC-G.709/

--- abstract

This document defines a collection of common data types, identities, and groupings in YANG data modeling language. These derived common types and groupings are intended to be imported by modules that model, e.g., Traffic Engineering (TE) configuration and state capabilities.

This document obsoletes RFC 8776.

--- middle

# Introduction

YANG {{!RFC6020}} {{!RFC7950}} is a data modeling language used to model configuration data, state data, Remote Procedure Calls, and notifications for network management protocols such as the Network Configuration Protocol (NETCONF) {{!RFC6241}} or RESTCONF {{!RFC8040}}. The YANG language supports a small set of built-in data types and provides mechanisms to derive other types from the built-in types.

This document introduces a collection of common data types derived from the built-in YANG data types. The derived data types, identities, and groupings are designed to be the common definitions applicable for modeling Traffic Engineering (TE) features in model(s) defined outside of this document. These types can be used by non-TE modules per the guidance in {{Section 4.12 of ?I-D.ietf-netmod-rfc8407bis}}.

This document adds new common data types, identities, and groupings to both the "ietf-te-types" and the "ietf-te-packet-types" YANG models and obsoletes {{!RFC8776}}. For further details, refer to the revision statements of the YANG modules in {{te-yang-code}} and {{pkt-yang-code}} or the changes summary in {{changes-bis}}.

## Requirements Notation

{::boilerplate bcp14}

> RFC Editor: The document uses "CHANGE NOTE" to ease identifying the changes vs. RFC8776. Please remove these notes.

## Terminology

   The terminology for describing YANG data models is found in
   {{!RFC7950}}.

## Prefixes in Data Node Names

  Names of data nodes and other data model objects
  are prefixed using the standard prefix associated with the
  corresponding YANG imported modules, as shown in {{tab-prefixes}}.

| Prefix          | YANG module          | Reference
| yang            | ietf-yang-types      | {{Section 3 of !RFC6991}}
| inet            | ietf-inet-types      | {{Section 4 of !RFC6991}}
| rt-types        | ietf-routing-types   | {{!RFC8294}}
| te-types        | ietf-te-types        | RFCXXXX
| te-packet-types | ietf-te-packet-types | RFCXXXX
{: #tab-prefixes title="Prefixes and corresponding YANG modules"}

> RFC Editor: Please replace XXXX through this document with the RFC number assigned to this document.

# Acronyms and Abbreviations


GMPLS:
: Generalized Multiprotocol Label Switching

LSP:
: Label Switched Path

LSR:
: Label Switching Router

LER:
: Label Edge Router

MPLS:
: Multiprotocol Label Switching

RSVP:
: Resource Reservation Protocol

TE:
: Traffic Engineering

DS-TE:
: Differentiated Services Traffic Engineering

SRLG:
: Shared Risk Link Group

NBMA:
: Non-Broadcast Multi-Access

APS:
: Automatic Protection Switching

SD:
: Signal Degrade

SF:
: Signal Fail

WTR:
: Wait-to-Restore

PM:
: Performance Metrics

# Overview {#overview}

This document defines two YANG modules for common TE types: "ietf-te-types" for TE generic types ({{te-yang-code}}) and "ietf-te-packet-types" for packet-specific types ({{pkt-yang-code}}). Other technology-specific TE types are outside the scope of this document.

## TE Types Module Contents

The "ietf-te-types" module ({{te-yang-code}}) contains common TE types that are independent and agnostic of any specific technology or control-plane instance.

The "ietf-te-types" module contains the following YANG reusable groupings:

te-bandwidth:
: A YANG grouping that defines the generic TE bandwidth. The modeling structure allows augmentation for each technology. For unspecified technologies, the string-encoded "te-bandwidth" type is used.

te-label:
: A YANG grouping that defines the generic TE label. The modeling structure allows augmentation for each technology. For unspecified technologies, "rt-types:generalized-label" is used.

performance-metrics-attributes:
: A YANG grouping that defines one-way and two-way measured Performance Metrics (PM) and indications of anomalies on link(s) or the path as defined in {{?RFC7471}}, {{?RFC8570}}, and {{?RFC7823}}.

performance-metrics-throttle-container:
: A YANG grouping that defines thresholds for advertisement suppression and measurement intervals.

Also, the "ietf-te-types" module contains the following YANG reusable types:

te-ds-class:
: A type representing the Differentiated Services (DS) Class-Type of traffic as defined in {{?RFC4124}}.

te-label-direction:
: An enumerated type for specifying the forward or reverse direction of a label.

te-hop-type:
: An enumerated type for specifying that a hop is loose or strict in a path.

te-global-id:
: A type representing an identifier that uniquely identifies an operator, which can be either a provider or a client. The definition of this type is taken from {{Section 3 of ?RFC6370}} and {{Section 3 of ?RFC5003}}. This attribute type is used solely to provide a globally unique context for TE topologies.

te-node-id:
: A type representing the identifier for a node in a TE topology. The identifier is represented as 4 octets in dotted-quad notation.
: This attribute MAY be mapped to the Router Address TLV described in {{Section 2.4.1 of ?RFC3630}}, the TE Router ID described in {{Section 6.2 of ?RFC6827}}, the Traffic Engineering Router ID TLV described in {{Section 4.3 of ?RFC5305}}, or the TE Router ID TLV described in {{Section 3.2.1 of ?RFC6119}}.
: The reachability of such a TE node MAY be achieved by a mechanism such as that described in {{Section 6.2 of ?RFC6827}}.

te-topology-id:
: A type representing the identifier for a topology. It is optional to have one or more prefixes at the beginning, separated by colons. The prefixes can be "network-types" as defined in the "ietf-network" module in {{!RFC8345}}, to help the user better understand the topology before further inquiry is made.

te-tp-id:
: A type representing the identifier of a TE interface Link Termination Point (LTP) on a specific TE node where the TE link connects. This attribute is mapped to a local or remote link identifier {{?RFC3630}} {{?RFC5305}}.

te-path-disjointness:
: A type representing the different resource disjointness options for a TE tunnel path as defined in {{?RFC4872}}.

admin-groups:
: A union type for a TE link's classic or extended administrative groups as defined in {{?RFC3630}}, {{?RFC5305}}, and {{?RFC7308}}.

srlg:
: A type representing the Shared Risk Link Group (SRLG) as defined in {{?RFC4203}} and {{?RFC5307}}.

te-metric:
: A type representing the TE metric as defined in {{?RFC3785}}.

te-recovery-status:
: An enumerated type for the different statuses of a recovery action as defined in {{?RFC4427}} and {{?RFC6378}}.

path-attribute-flags:
: A base YANG identity for supported LSP path flags as defined in {{?RFC3209}}, {{?RFC4090}}, {{?RFC4736}}, {{?RFC5712}}, {{?RFC4920}}, {{?RFC5420}}, {{?RFC7570}}, {{?RFC4875}}, {{?RFC5151}}, {{?RFC5150}}, {{?RFC6001}}, {{?RFC6790}}, {{?RFC7260}}, {{?RFC8001}}, {{?RFC8149}}, and {{?RFC8169}}.

link-protection-type:
: A base YANG identity for supported link protection types as defined in {{?RFC4872}} and {{?RFC4427}}.

restoration-scheme-type:
: A base YANG identity for supported LSP restoration schemes as defined in {{?RFC4872}}.

protection-external-commands:
: A base YANG identity for supported protection-related external commands used for troubleshooting purposes, as defined in {{?RFC4427}} and {{ITU_G.808.1}}.

CHANGE NOTE: The description and reference of the identity action-exercise, which applies only to APS and it is not defined in RFC4427, has been updated to reference ITU-T G.808.1.

association-type:
: A base YANG identity for supported LSP association types as defined in {{?RFC6780}}, {{?RFC4872}}, {{?RFC4873}}, and {{!RFC8800}}.

CHANGE NOTE: The association-type-diversity identity, defined in {{!RFC8800}} has been added to the association-type base identity.


objective-function-type:
: A base YANG identity for supported path objective functions as defined in {{!RFC5541}}.

CHANGE NOTE: The objective-function-type identity has been redefined to be used only for path objective functions and a new svec-objective-function-type identity has been added for the Synchronization VECtor (SVEC) objective functions. Therefore the of-minimize-agg-bandwidth-consumption, of-minimize-load-most-loaded-link and of-minimize-cost-path-set identities, defined in {{!RFC5541}} and derived from the objective-function-type identity, have been obsoleted because not applicable to paths but to Synchronization VECtor (SVEC) objects.


te-tunnel-type:
: A base YANG identity for supported TE tunnel types as defined in {{?RFC3209}} and {{?RFC4875}}.

lsp-encoding-types:
: A base YANG identity for supported LSP encoding types as defined in {{?RFC3471}}.

lsp-protection-type:
: A base YANG identity for supported LSP protection types as defined in {{?RFC4872}} and {{?RFC4873}}.

switching-capabilities:
: A base YANG identity for supported interface switching capabilities as defined in {{?RFC3471}}.

resource-affinities-type:
: A base YANG identity for supported attribute filters associated with a tunnel that must be satisfied for a link to be acceptable as defined in {{?RFC2702}} and {{?RFC3209}}.

CHANGE NOTE: The description of the path-metric-type has been updated


path-metric-type:
: A base YANG identity for supported path metric types as defined in {{?RFC3630}} {{?RFC3785}}, {{!RFC5440}}, {{?RFC7471}}, {{?RFC8233}} and {{?RFC8570}}.
: The unit of the path metric value is interpreted in the context of the path metric type. The derived identities SHOULD describe the unit and maximum value of the path metric types they define.
: For example, the bound of the 'path-metric-loss', defined in 'ietf-te-packet-types', is defined in multiples of the basic unit 0.000003% as described in {{?RFC7471}} and {{?RFC8570}}.

explicit-route-hop:
: A YANG grouping that defines supported explicit routes as defined in {{?RFC3209}} and {{?RFC3477}}.

te-link-access-type:
: An enumerated type for the different TE link access types as defined in {{?RFC3630}}.

CHANGE NOTE: The module "ietf-te-types" has been updated to add the following YANG identities, types and groupings.


lsp-provisioning-error-reason:
: A base YANG identity for reporting LSP provisioning error reasons. No standard LPS provisioning error reasons are defined in this document.

path-computation-error-reason:
: A base YANG identity for reporting path computation error reasons as defined in {{pc-error}}.

protocol-origin-type:
:  A base YANG identity for the type of protocol origin as defined in {{protocol-origin}}.

svec-objective-function-type:
: A base YANG identity for supported SVEC objective functions as defined in {{!RFC5541}} and {{!RFC8685}}.

svec-metric-type:
: A base YANG identity for supported SVEC objective functions as defined in {{!RFC5541}}.

encoding-and-switching-type:
: This is a common grouping to define the LSP encoding and switching types.

CHANGE NOTE: The tunnel-admin-state-auto YANG identity, derived from the tunnel-admin-status-type base YANG identity has also been added. No description is provided, since no description for the tunnel-admin-status-type base YANG identity has been provided in RFC8776.

CHANGE NOTE: The lsp-restoration-restore-none YANG identity, derived from the lsp-restoration-type base YANG identity has also been added. No description is provided, since no description for the lsp-restoration-type base YANG identity has been provided in RFC8776.

### Path Computation Errors {#pc-error}

The "ietf-te-types" module contains the YANG reusable identities for reporting path computation error reasons as defined in {{!RFC5440}}, {{!RFC5441}}, {{!RFC5520}}, {{!RFC5557}}, {{!RFC8306}}, and {{!RFC8685}}.

It also defines the following additional YANG reusable identities for reporting also the following path computation error reasons:

path-computation-error-no-topology:
: A YANG identity for reporting path computation error when there is no topology with the provided topology identifier.


### Protocol Origin {#protocol-origin}

The "ietf-te-types" module contains the YANG reusable identities for the type of protocol origin as defined in {{!RFC5440}} and {{!RFC9012}}.

It also defines the following additional YANG reusable identities for the type of protocol origin:

protocol-origin-api:
:  A YANG identity to be used when  the type of protocol origin is an Application Programmable Interface (API).

## Packet TE Types Module Contents

The "ietf-te-packet-types" module ({{pkt-yang-code}}) covers the common types and groupings that are specific to packet technology.

The "ietf-te-packet-types" module contains the following YANG reusable types and groupings:

backup-protection-type:
: A base YANG identity for supported protection types that a backup or bypass tunnel can provide as defined in {{?RFC4090}}.

te-class-type:
: A type that represents the Diffserv-TE Class-Type as defined in {{?RFC4124}}.

bc-type:
: A type that represents Diffserv-TE Bandwidth Constraints (BCs) as defined in {{?RFC4124}}.

bc-model-type:
: A base YANG identity for supported Diffserv-TE Bandwidth Constraints Models as defined in {{?RFC4125}}, {{?RFC4126}}, and {{?RFC4127}}.

te-bandwidth-requested-type:
: An enumerated type for the different options to request bandwidth for a specific tunnel.

performance-metrics-attributes-packet:
: A YANG grouping that contains the generic performance metrics and additional packet-specific metrics.

CHANGE NOTE: The module "ietf-te-packet-types" has been updated to add the following YANG identities and groupings.


bandwidth-profile-type:
: A base YANG identity for various bandwidth profiles specified in {{MEF_10.3}}, {{?RFC2697}}, {{?RFC2698}} and {{?RFC4115}} that may be used to limit bandwidth utilization of packet flows (e.g., MPLS-TE LSPs).

te-packet-path-bandwidth
: A YANG grouping that defines the path bandwidth information and could be used in any Packet TE model (e.g., MPLS-TE topology model) for the path bandwidth representation (e.g., the bandwidth of an MPLS-TE LSP).
: The Packet TE path bandwidth can be represented by a bandwidth profile as follows:

~~~~ ascii-art
         +--:(packet)
           +--rw bandwidth-profile-name?   string
           +--rw bandwidth-profile-type?   identityref
           +--rw cir                       uint64
           +--rw eir                       uint64
           +--rw cbs?                      uint64
           +--rw ebs?                      uint64
~~~~

NOTE: Other formats for the MPLS-TE path bandwidth are defined in {{?I-D.ietf-teas-yang-te-mpls}} and they could be added in a future update of this document.

te-packet-link-bandwidth:
: A YANG grouping that defines the link bandwidth information and could be used in any Packet TE model (e.g., MPLS-TE topology) for link bandwidth representation.
: All the link bandwidth related sections in the "ietf-te-types" generic module, {{te-yang-code}}, need to be augmented with this grouping for the usage of Packet TE technologies.



# TE Types YANG Module {#te-yang-code}

The "ietf-te-types" module imports from the following modules:

- "ietf-yang-types" and "ietf-inet-types" as defined in {{!RFC6991}}

- "ietf-routing-types" as defined in {{!RFC8294}}

In addition to {{!RFC6991}} and {{!RFC8294}}, this module references the following documents in defining the types and YANG groupings:
{{?RFC9522}}, {{?RFC4090}}, {{?RFC4202}}, {{?RFC4328}}, {{?RFC4561}}, {{?RFC4657}}, {{?RFC4736}}, {{?RFC6004}}, {{?RFC6511}}, {{?RFC7139}}, {{?RFC7308}}, {{?RFC7551}}, {{?RFC7571}}, {{?RFC7579}}, and {{ITU-T_G.709}}.

CHANGE NOTE: Please focus your review only on the updates to the YANG model: see also {{te-yang-diff}}.


~~~~ yang
{::include ../../ietf-te-types.yang}
~~~~
{: #fig-te-yang title="TE Types YANG module"
sourcecode-markers="true" sourcecode-name="ietf-te-types@2024-01-29.yang"}

{: #pkt-yang-code}

# Packet TE Types YANG Module

The "ietf-te-packet-types" module imports from the "ietf-te-types" module defined in {{te-yang-code}} of this document.

CHANGE NOTE: Please focus your review only on the updates to the YANG model: see also {{te-yang-diff}}.


~~~~ yang
{::include ../../ietf-te-packet-types.yang}
~~~~
{: #fig-pkt-yang title="Packet TE Types YANG module"
sourcecode-markers="true" sourcecode-name="ietf-te-packet-types@2024-01-25.yang"}

# IANA Considerations

This document requests IANA to update the following URIs in the "IETF XML Registry" {{?RFC3688}} to refer to this document:

~~~~
      URI: urn:ietf:params:xml:ns:yang:ietf-te-types
      Registrant Contact:  The IESG.
      XML: N/A, the requested URI is an XML namespace.

      URI: urn:ietf:params:xml:ns:yang:ietf-te-packet-types
      Registrant Contact:  The IESG.
      XML: N/A, the requested URI is an XML namespace.
~~~~

This document also requests IANA to add the following YANG modules to the "YANG Module
Names" registry {{!RFC7950}}:

~~~~
      name:      ietf-te-types
      Maintained by IANA?  N
      namespace: urn:ietf:params:xml:ns:yang:ietf-te-types
      prefix:    te-types
      reference: RFC XXXX

      name:      ietf-te-packet-types
      Maintained by IANA?  N
      namespace: urn:ietf:params:xml:ns:yang:ietf-te-packet-types
      prefix:    te-packet-types
      reference: RFC XXXX
~~~~

# Security Considerations

   The YANG module specified in this document defines a schema for data
   that is designed to be accessed via network management protocols such
   as NETCONF {{!RFC6241}} or RESTCONF {{!RFC8040}}.  The lowest NETCONF layer
   is the secure transport layer, and the mandatory-to-implement secure
   transport is Secure Shell (SSH) {{!RFC6242}}.  The lowest RESTCONF layer
   is HTTPS, and the mandatory-to-implement secure transport is TLS
   {{!RFC8446}}.

   The Network Configuration Access Control Model (NACM) {{!RFC8341}}
   provides the means to restrict access for particular NETCONF or
   RESTCONF users to a preconfigured subset of all available NETCONF or
   RESTCONF protocol operations and content.

   The YANG module in this document defines common TE type definitions
   (e.g., typedef, identity, and grouping statements) in YANG data
   modeling language to be imported and used by other TE modules.  When
   imported and used, the resultant schema will have data nodes that can
   be writable or readable.  Access to such data nodes may be considered
   sensitive or vulnerable in some network environments.  Write
   operations (e.g., edit-config) to these data nodes without proper
   protection can have a negative effect on network operations.


--- back

{: #changes-bis}

# Changes from RFC 8776

This version adds new common data types, identities, and groupings to the YANG modules. It also updates some of the existing data types, identities, and groupings in the YANG modules and fixes few bugs in {{!RFC8776}}.

The following new identities have been added to the 'ietf-te-types' module:

- lsp-provisioning-error-reason;

- association-type-diversity;

- tunnel-admin-state-auto;

- lsp-restoration-restore-none;

- restoration-scheme-rerouting;

- path-metric-optimization-type;

- link-path-metric-type;

- link-metric-type and its derived identities;

- path-computation-error-reason and its derived identities;

- protocol-origin-type and its derived identities;

- svec-objective-function-type and its derived identities;

- svec-metric-type and its derived identities.

The following new data types have been added to the 'ietf-te-types' module:

- path-type;

- te-gen-node-id.

The following new groupings have been added to the 'ietf-te-types' module:

- encoding-and-switching-type;

- te-generic-node-id.

The following new identities have been added to the 'ietf-te-packet-types' module:

- bandwidth-profile-type;

- link-metric-delay-variation;

- link-metric-loss;

- path-metric-delay-variation;

- path-metric-loss.

The following new groupings have been added to the 'ietf-te-packet-types' module:

- te-packet-path-bandwidth;

- te-packet-link-bandwidth.

The following identities, already defined in {{!RFC8776}}, have been updated in the 'ietf-te-types' module:

- objective-function-type (editorial);

- action-exercise (bug fix);

- path-metric-type:

   new base identities have been added;

- path-metric-te (bug fix);

- path-metric-igp (bug fix);

- path-metric-hop (bug fix);

- path-metric-delay-average (bug fix);

- path-metric-delay-minimum (bug fix);

- path-metric-residual-bandwidth (bug fix);

- path-metric-optimize-includes (bug fix);

- path-metric-optimize-excludes (bug fix);

- te-optimization-criterion (editorial).

The following data type, already defined in {{!RFC8776}}, has been updated in the 'ietf-te-types' module:

- te-node-id;

   The data type has been changed to be a union.

The following groupings, already defined in {{!RFC8776}}, have been updated in the 'ietf-te-types' module:

- explicit-route-hop

   The following new leaves have been added to the 'explicit-route-hop' grouping:

   - node-id-uri;

   - link-tp-id-uri;

   The following leaves, already defined in {{!RFC8776}}, have been updated in the 'explicit-route-hop':

   - node-id;

   - link-tp-id.

      The mandatory true statements for the node-id and link-tp-id have been replaced by must statements that requires at least the presence of:

      - node-id or node-id-uri;

      - link-tp-id or link-tp-id-uri.

- explicit-route-hop

   The following new leaves have been added to the 'explicit-route-hop' grouping:

   - node-id-uri;

   - link-tp-id-uri;

   The following leaves, already defined in {{!RFC8776}}, have been updated in the 'explicit-route-hop':

   - node-id;

   - link-tp-id.

      The mandatory true statements for the node-id and link-tp-id have been replaced by must statements that requires at least the presence of:

      - node-id or node-id-uri;

      - link-tp-id or link-tp-id-uri.

- optimization-metric-entry:

   The following leaves, already defined in {{!RFC8776}}, have been updated in the 'optimization-metric-entry':

   - metric-type;

      The base identity has been updated without impacting the set of derived identities that are allowed.

- tunnel-constraints;

   The following new leaf have been added to the 'tunnel-constraints' grouping:

    - network-id;

- path-constraints-route-objects:

   The following container, already defined in {{!RFC8776}}, has been updated in the 'path-constraints-route-objects':

    - explicit-route-objects-always;

      The container has been renamed as 'explicit-route-objects'. This change is not affecting any IETF standard YANG models since this grouping has not yet been used by any YANG model defined in existing IETF RFCs.

- generic-path-metric-bounds:

   The following leaves, already defined in {{!RFC8776}}, have been updated in the 'optimization-metric-entry':

   - metric-type;

      The base identity has been updated to:

      - increase the set of derived identities that are allowed and;

      - remove from this set the 'path-metric-optimize-includes' and the 'path-metric-optimize-excludes' identities (bug fixing)
      
- generic-path-optimization

   The following new leaf have been added to the 'generic-path-optimization' grouping:

    - tiebreaker;

   The following container, already defined in {{!RFC8776}}, has been deprecated:

    - tiebreakers.

The following identities, already defined in {{!RFC8776}}, have been obsoletes in the 'ietf-te-types' module for bug fixing:

- of-minimize-agg-bandwidth-consumption;

- of-minimize-load-most-loaded-link;

- of-minimize-cost-path-set;

- lsp-protection-reroute-extra;

- lsp-protection-reroute.

{: #te-yang-diff}

## TE Types YANG Diffs

RFC Editor: please remove this appendix before publication.

This section provides the diff between the YANG module in section 3.1 of {{!RFC8776}} and the YANG model revision in {{te-yang-code}}.

The intention of this appendix is to facilitate focusing the review of the YANG model in {{te-yang-code}} to the changes compared with the YANG model in {{!RFC8776}}.

This diff has been generated using the following UNIX commands to compare the YANG module revisions in section 3.1 of {{!RFC8776}} and in {{te-yang-code}}:

~~~~
diff ietf-te-types@2020-06-10.yang ietf-te-types.yang 
     > model-diff.txt
sed 's/^/    /' model-diff.txt > model-diff-spaces.txt
sed 's/^    >   /    >   /' model-diff-spaces.txt 
    > model-updates.txt
~~~~

The output (model-updates.txt) is reported here:

{::include ./diffs/te-types/model-updates.txt}

## Packet TE Types YANG Diffs

RFC Editor: please remove this appendix before publication.

This section provides the diff between the YANG module in section 3.2 of {{!RFC8776}} and the YANG model revision in {{pkt-yang-code}}.

The intention of this appendix is to facilitate focusing the review of the YANG model in {{pkt-yang-code}} to the changes compared with the YANG model in {{!RFC8776}}.

This diff has been generated using the following UNIX commands to compare the YANG module revisions in section 3.2 of {{!RFC8776}} and in {{pkt-yang-code}}:

~~~~
diff ietf-te-packet-types@2020-06-10.yang ietf-te-packet-types.yang 
     > model-diff.txt
sed 's/^/    /' model-diff.txt > model-diff-spaces.txt
sed 's/^    >   /    >   /' model-diff-spaces.txt 
    > model-updates.txt
~~~~

The output (model-updates.txt) is reported here:

{::include ./diffs/te-pkt-types/model-updates.txt}

{: #options}

# Option Considered for updating RFC8776

RFC Editor: please remove this appendix before publication.

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

{: numbered="false"}

# Acknowledgements

The authors would like to thank 
Robert Wilton, Lou Berger, Mahesh Jethanandani and Jeff Haas
for their valuable input to the discussion
about the process to follow to provide tiny updates to a YANG module already published as an RFC.

   This document was prepared using kramdown.
