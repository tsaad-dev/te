---
coding: utf-8

title: A YANG Data Model for MPLS-TE Topology

abbrev: MPLS-TE Topology YANG Model
docname: draft-busizheng-teas-yang-te-mpls-topology-06
submissiontype: IETF
workgroup: TEAS Working Group
category: std
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
  -
    name: Italo Busi
    org: Huawei Technologies
    email: italo.busi@huawei.com
  -
    name: Aihua Guo
    org: Futurewei Inc.
    email: aihuaguo.ietf@gmail.com
  -
    name: Xufeng Liu
    org: Alef Edge
    email: xufeng.liu.ietf@gmail.com
  -
    name: Tarek Saad
    org: Cisco Systems, Inc.
    email: tsaad.net@gmail.com
  -
    name: Rakesh Gandhi
    org: Cisco Systems, Inc.
    email: rgandhi@cisco.com

contributor:
  -
    name: Haomian Zheng
    org: Huawei Technologies
    email: zhenghaomian@huawei.com
  -
    name: Vishnu Pavan Beeram
    ins: V. Beeram
    org: Juniper Networks
    email: vbeeram@juniper.net
  -
    name: Igor Bryskin
    org: Individual
    email: i_bryskin@yahoo.com
  -
    name: Adrian Farrel
    org: Old Dog Consulting
    email: adrian@olddog.co.uk

--- abstract

This document describes a YANG data model for MPLS-TE network topologies.

--- middle

{: #introduction}

# Introduction

  This document describes a YANG data model for MPLS-TE network topologies: {{?RFC2702}}.

  This document also defines a collection of common data types and
  groupings in YANG data modeling language for MPLS-TE networks.  These
  derived common types and groupings are intended to be imported by the
  MPLS-TE topology model, defined in this document, as well as by the
  MPLS-TE tunnel model, defined in {{?I-D.ietf-teas-yang-te-mpls}}.

  Multiprotocol Label Switching - Transport Profile (MPLS-TP) is a
  profile of the MPLS protocol that is used in packet switched
  transport networks and operated in a similar manner to other existing
  transport technologies (e.g., OTN), as described in {{?RFC5921}}. The YANG
  model defined in this document can also be used for MPLS-TP network topologies.

## Tree Diagram

  A simplified graphical representation of the data model is used in
  {{mpls-te-topology-tree}} of this this document.  The meaning of the symbols in
  these diagrams is defined in {{!RFC8340}}.

{: #prefix}

## Prefixes in Data Node Names

  In this document, names of data nodes and other data model objects
  are prefixed using the standard prefix associated with the
  corresponding YANG imported modules, as shown in {{tab-prefixes}}.

| Prefix        | YANG Module             | Reference
| ------------- | ----------------------- | ------------- |
| rt-types      | ietf-routing-types      | {{!RFC8294}}  |
| mpls-te-types | ietf-mpls-te-types      | RFC XXXX      |
| nw            | ietf-network            | {{!RFC8345}}  |
| nt            | ietf-network-topology   | {{!RFC8345}}  |
| tet           | ietf-te-topology        | {{!RFC8795}}  |
| tet-pkt       | ietf-te-topology-packet | \[RFCYYYY]    |
| tet-mpls      | ietf-te-mpls-topology   | RFC XXXX      |
{: #tab-prefixes title="Prefixes and corresponding YANG modules"}

RFC Editor Note:
Please replace XXXX with the RFC number assigned to the RFC once this draft becomes an RFC.
Please replace YYYY with the RFC numbers assigned to {{!I-D.ietf-teas-yang-l3-te-topo}}.
Please remove this note.

{: #mpls-te-types-overview}

# MPLS-TE Types Overview

  The module ietf-mpls-te-types contains the following YANG
  types and groupings which can be used by other MPLS-TE YANG models:

  load-balancing-type:

  > This identity defines the types of load-balancing algorithms used on a
  bundled MPLS-TE link.

  te-mpls-label-hop:

  > This grouping is used for augmentation of the TE label for MPLS-TE
  paths.

{: #mpls-te-topo-overview}

# MPLS-TE Topology Model Overview

  The MPLS-TE technology-specific topology model augments the ietf-te-
  topology-packet YANG module, defined in {{!I-D.ietf-teas-yang-l3-te-topo}}, which in
  turn augments the generic ietf-te-topology YANG module, defined in
  {{!RFC8795}}, as shown in {{fig-mpls-te-topo}}.

~~~~ ascii-art
                +------------------+
   TE generic   | ietf-te-topology |
                +---------+--------+
                          ^
                          |
                          | Augments
                          |
             +------------+------------+
   Packet TE | ietf-te-topology-packet |
             +------------+------------+
                          ^
                          |
                          | Augments
                          |
              +-----------+-----------+
   MPLS-TE    | ietf-te-mpls-topology |
              +-----------------------+
~~~~
{: #fig-mpls-te-topo title="Relationship between MPLS-TE, Packet-TE and TE Topology Models"}

  Given the guidance for augmentation in {{!RFC8795}}, the following
  technology-specific augmentations need are provided:

  - A network-type to indicate that the TE topology is an MPLS-TE
    topology, as follow:

~~~~
      augment /nw:networks/nw:network/nw:network-types
              /tet:te-topology/tet-pkt:packet:
        +--rw mpls-topology!
~~~~

  - TE Label augmentations as described in {{mpls-te-label}}.

Note: TE bandwidth augmentations for paths, LSPs, and links are provided by the ietf-te-topology-packet module, defined in {{!I-D.ietf-teas-yang-l3-te-topo}}.

{: #mpls-te-label}

## TE Label Augmentations

  In MPLS-TE, label allocation is done by the network element. Information about
  the availability of label values does not need to be provided to the
  controller. Moreover, MPLS-TE tunnels are currently mainly only established
  within a single domain.

  Therefore this document does not define any MPLS-TE
  technology-specific augmentations, of the TE Topology model specific to the
  TE label because no TE label-related attributes are instantiated
  for MPLS-TE Topologies.

  Furthermore, because the primary use cases are for single domain MPLS-TE tunnels,
  this document does not define objects that facilitate the setup of multi-domain
  MPLS-TE tunnels. It is an item for future study to understand how a management
  system would coordinate YANG configuration of a tunnel that crosses a domain
  boundary, and it is expected that that would be defined in a separate document.

{: #mpls-tp-topology}

## MPLS-TP Topology

  Multiprotocol Label Switching - Transport Profile (MPLS-TP) is a
  profile of the MPLS protocol that is used in packet switched
  transport networks and operated in a similar manner to other existing
  transport technologies (e.g., OTN), as described in {{?RFC5921}}.

  Therefore, the YANG models defined in this document can also be applied
  to MPLS-TP network topologies.

  However, as described in {{?RFC5921}}, MPLS-TP networks support
  bidirectional LSPs and require no equal cost multipath (ECMP) and no
  previous hop popping (PHP). When reporting the
  topology for an MPLS-TP network, additional information is required
  to indicate whether the network components (links and nodes) support these MPLS-TP
  characteristics.

  It is worth noting that {{!RFC8795}} is already capable of modeling TE
  topologies supporting either unidirectional or bidirectional LSPs:
  all bidirectional TE links can support bidirectional LSPs, and all
  links can support unidirectional LSPs. Further, it is always possible to
  associate two unidirectional LSPs to compose a bidirecitonal service as
  long as they belong to the same tunnel.

  When setting up bidirectional LSPs (e.g., MPLS-TP LSPs) only
  bidirectional TE Links are selected by path computation.

  In order to allow reporting that ECMP is not affecting forwarding the
  packets of a given LSP, the model defined in this documents provides the
  load-balancing-type attribute which reports whether a link aggregation group (LAG)
  or TE Bundled Link performs load-balancing, and if so, whether it is on a per-flow
  or per-top-label basis:

~~~~
    augment /nw:networks/nw:network/nt:link/tet:te:
      +--rw load-balancing-type?   mte-types:load-balancing-type
~~~~

  When setting up LSPs which require the non-use of ECMP (e.g., MPLS-TP LSPs)
  only links that are not part of a LAG or TE Bundle, or that perform
  per-top-label load balancing are selected by path computation.

  It is assumed that almost all the MPLS-TE nodes are capable of
  supporting Ultimate Hop Popping (UHP) (i.e., they do not require the previous
  node on the path to perform PHP). However, if some interfaces are
  not able to support UHP, they can report it in the MPLS-TE topology:

~~~~
    augment /nw:networks/nw:network/nw:node/nt:termination-point
            /tet:te:
      +--ro uhp-incapable?   empty
~~~~

  When setting up LSPs which require the non-use of PHP (e.g., MPLS-TP LSPs)
  only the destination node interfaces (link termination points - LTPs) that are capable of supporting UHP
  are selected by path computation.

{: #pck-te-types-yang}

# YANG model for common MPLS-TE Types

~~~~ yang
{::include ../../ietf-mpls-te-types.yang}
~~~~
{: #fig-mpls-te-types-yang title="MPLS-TE Types YANG model" sourcecode-markers="true" sourcecode-name="ietf-mpls-te-types@2023-10-13.yang"}

{: #mpls-te-topology}

# YANG Model for MPLS-TE Topology

{: #mpls-te-topology-tree}

## YANG Tree

  {{fig-mpls-te-topology-tree}} shows the tree diagram of the YANG model defined in
  module ietf-te-mpls-topology.yang.

~~~~ ascii-art
{::include ../../ietf-te-mpls-topology.tree}
~~~~
{: #fig-mpls-te-topology-tree title="MPLS-TE topology YANG tree" artwork-name="ietf-te-mpls-topology.tree"}

{: #mpls-te-topology-yang}

## YANG Code

~~~~ yang
{::include ../../ietf-te-mpls-topology.yang}
~~~~
{: #fig-mpls-te-topology-yang title="MPLS-TE topology YANG module" sourcecode-markers="true" sourcecode-name="ietf-te-mpls-topology@2023-10-13.yang"}

{: #security}

# Security Considerations

   The configuration, state, and action data defined in this document
   are designed to be accessed via a management protocol with a secure
   transport layer, such as NETCONF {{!RFC6241}} or RESTCONF {{!RFC8040}}.
   The lowest NETCONF layer is the secure transport layer, and the
   mandatory-to-implement secure transport is Secure Shell (SSH)
   {{!RFC6242}}. The lowest RESTCONF layer is HTTPS, and the mandatory-
   to-implement secure transport is TLS {{!RFC8446}}.

   The NETCONF access control model {{!RFC8341}} provides the means to
   restrict access for particular NETCONF users to a preconfigured
   subset of all available NETCONF protocol operations and content.

   The ietf-mpls-te-types model presented in this document defines common
   types intended to be used as imports by other YANG models. Those other
   models are responsible for considering the security of the objects they
   define using those imports. Writers of those other models should consider
   the vulnerabilities created by exposing information about link characteristics
   and behaviors (such as how packets may be steered onto parallel links),
   and should be aware of the risks of enabling configuration of which labels
   are used on hops within an LSP.

   The ietf-te-mpls-topology model presented in this document defines
   technology-specific objects to describe an MPLS-TE topology. It is intended
   as an aumentation of the te-topology model {{!RFC8795}} and so the core
   security considerations for that model also apply. In addition, this model
   defines objects that could expose information about the network behavior
   or which, if modified by an attacker could disrupt the delivery of
   services in the network.

   The leaf objects defined in ietf-te-mpls-topology are read-only so the
   risk is from unauthorized access to the information, or from misrepresenting
   the information reported from the network elements. The objects are:

   "tet:te-topology/tet-pkt:packet": Unauthorized read access to this simply
   indicates that the network topology is MPLS-TE packet-capable: that information is not
   very valuable to an attacker. Modification of this information might cause
   a path computation element to incorrectly presume that a network is capable or
   incapable of supporting MPLS-TE services.

   "tet-pkt:packet/tet-mpls:mpls-topology/load-balancing-type": Unauthorized read access to this
   indicates the mechanism used by a nework node to share traffic across members
   of a LAG or bundled MPLS-TE link. Such knowledge might help an attacker predict which component
   link is carrying specific traffic making a physical attack slightly easier. Modification
   of this information might cause a path computation element to incorrectly presume that
   a link is suitable or unsuitable for use to provide an MPLS-TP service.

   "tet-pkt:packet/tet-mpls:mpls-topology/uhp-incapable": Unauthorized read access to this will
   give an attacker knowledge about whether PHP is being applied on the final hop of all LSPs to
   a particular node on the associated link: that information is of little use to an attacker
   except it may help them to parse an inflight packet. Modification of this information would
   cause a path computation element to incorrectly consider the associated link as suitable or
   unsuitable for inclusion in the path of an MPLS-TP service.

{: #iana}

# IANA Considerations

This document requests IANA to register the following URIs in the "ns" subregistry within the "IETF XML Registry" {{!RFC3688}}. Following the format in {{!RFC3688}}, the following registrations are requested.

~~~~
      URI:  urn:ietf:params:xml:ns:yang:ietf-mpls-te-types
      Registrant Contact:  The IESG.
      XML: N/A; the requested URI is an XML namespace.

      URI:  urn:ietf:params:xml:ns:yang:ietf-te-mpls-topology
      Registrant Contact:  The IESG.
      XML: N/A; the requested URI is an XML namespace.
~~~~

This document requests IANA to register the following YANG modules in the "IANA Module Names" {{!RFC6020}}. Following the format in {{!RFC6020}}, the following registrations are requested:

~~~~
      name:      ietf-mpls-te-types
      namespace: urn:ietf:params:xml:ns:yang:ietf-mpls-te-types
      prefix:    mpls-te-types
      reference: RFC XXXX

      name:      ietf-te-mpls-topology
      namespace: urn:ietf:params:xml:ns:yang:ietf-te-mpls-topology
      prefix:    tet-mpls
      reference: RFC XXXX
~~~~

RFC Editor: Please replace XXXX with the RFC number assigned to this document.

--- back

{: numbered="false"}

# Acknowledgments

  We thank Loa Andersson for providing useful suggestions for this draft.

  This document was prepared using kramdown.

  Previous versions of this document was prepared using 2-Word-v2.0.template.dot.
