---
coding: utf-8

title: >
   Profiles for Traffic Engineering (TE) Topology Data Model and
   Applicability to non-TE Use Cases

abbrev: TE Topology Profiles
docname: draft-ietf-teas-te-topology-profiles-latest
submissiontype: IETF
workgroup: TEAS Working Group
category: info
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
  -
    name: Italo Busi
    org: Huawei
    email: italo.busi@huawei.com
  -
    name: Xufeng Liu
    org: Alef Edge
    email: xufeng.liu.ietf@gmail.com
  -
    name: Igor Bryskin
    org: Individual
    email: i_bryskin@yahoo.com
  -
    name: Tarek Saad
    org: Cisco Systems Inc
    email: tsaad.net@gmail.com
  -
    name: Oscar Gonzalez de Dios
    ins: O. Gonzalez de Dios
    org: Telefonica
    email: oscar.gonzalezdedios@telefonica.com

contributor:
  -
    name: Aihua Guo
    org: Futurewei Inc.
    email: aihuaguo.ietf@gmail.com
  -
    name: Haomian Zheng
    org: Huawei
    email: zhenghaomian@huawei.com
  -
    name: Sergio Belotti
    org: Nokia
    email: sergio.belotti@nokia.com

--- abstract

   This document describes how profiles of the Traffic Engineering (TE)
   Topology Model, defined in RFC8795, can be used to address
   applications beyond "Traffic Engineering".

--- middle

# Introduction {#introduction}

There are many network scenarios being discussed in various IETF
Working Groups (WGs) that are not classified as "Traffic Engineering"
but can be addressed by a sub-set (profile) of the YANG data model, defined in {{!RFC8795}}.

Traffic Engineering (TE) is defined in {{?I-D.ietf-teas-rfc3272bis}} as aspects of
Internet network engineering that deal with the issues of performance
evaluation and performance optimization of operational IP networks.
TE encompasses the application of technology and scientific
principles to the measurement, characterization, modeling, and
control of Internet traffic.

The TE Topology Model is augmenting the Network Topology Model defined in {{!RFC8345}} with generic and technology-agnostic features, some of which are strictly applicable to TE networks, while others applicable to both TE and non-TE networks, and therefore could be considered as core network topology model constructs.

Examples of core network topology model constructs supported by the YANG data model defined in {{!RFC8795}}: inter-domain link discovery (plug-id),  and admin/operational status.

It is also worth noting that also the boundary between the TE-specific model constructs and the core network topology model constructs is also blurred since new happlications may need to leverage on constructs which was originally defined to support TE applications but that are also needed to support these new applications.

An example of a concept that originated from TE application but can be considered a core network topology model construct is the SRLG. New applications such as what-if analysis need to be aware of the SRLG information also for non-TE network topologies to provide reliable results.

It is also worth noting that the TE Topology Model is quite an
extensive and comprehensive model in which most features are
optional. Therefore, even though the full model appears to be
complex, at the first glance, a sub-set of the model (profile) can be
used to address specific scenarios, e.g. suitable also to non-TE use
cases.

The implementation of such TE Topology profiles can simplify and
expedite adoption of the full TE topology YANG data model, and allow
for its reuse even for non-TE use case. The key question being
whether all or some of the attributes defined in the TE Topology
Model are needed to address a given network scenario.

{{examples}} provides examples where profiles of the TE Topology Model
can be used to address some generic use cases applicable to both TE
and non-TE technologies.

# Examples of non-TE scenarios {#examples}

## UNI Topology Discovery {#uni-discovery}

UNI Topology Discovery is independent from whether the network is TE or non-TE.

The YANG data model defined in {{!RFC8795}} supports inter-domain link discovery (including
but not being limited to UNI link discovery) using the plug-id
attribute.

The following profile of the YANG data model defined in {{!RFC8795}} can be used to support the UNI Topology Discovery:

~~~~ ascii-art
   module: ietf-te-topology
     augment /nw:networks/nw:network/nw:network-types:
       +--rw te-topology!
     augment /nw:networks/nw:network/nw:node/nt:termination-point:
       +--rw te-tp-id?   te-types:te-tp-id
       +--rw te!
          +--rw admin-status?
          |       te-types:te-admin-status
          +--rw inter-domain-plug-id?        binary
          +--ro oper-status?                 te-types:te-oper-status
~~~~
{:#uni-discovery-tree title="UNI Topology"}

Note: Understanding that the solution is generic would be more straightforward
if the 'inter-domain-plug-id' leaf were defined
under a container with a different name than 'te' or directly under the parent 'termination-point' data node.

It is also worth noting that the UNI links can also be TE (e.g. an OTN UNI) or non-TE (e.g., an Ethernet UNI) as well as multi-function UNI links, supporting both TE and non-TE technologies, such as the UNI links, described in {{Section 4.4 of ?I-D.ietf-ccamp-transport-nbi-app-statement}}, which can be configured either OTN UNI or Ethernet UNI or SDH UNI.

The UNI Topology profiled YANG data model shown in {{uni-discovery-tree}} can also be used with technology-specific UNI augmentations, as described in {{augmentations}}. Technology-specific augmentations can for example describe the capability of the TP to be configured as a UNI for the types of services supported by the UNI (e.g., L2VPN/L3VPN).

For example, in {{?I-D.ietf-ccamp-eth-client-te-topo-yang}},
the eth-svc container is defined to
represent the capabilities of the Termination Point (TP) to be
configured as an Ethernet UNI, together with the Ethernet
classification and VLAN operations supported by that TP.

The {{?I-D.ietf-ccamp-otn-topo-yang}} provides another example, where:

-  the client-svc container is defined to represent the capabilities
   of the TP to be configured as an transparent client UNI (e.g.,
   STM-N, Fiber Channel or transparent Ethernet);

-  the OTN technology-specific Link Termination Point (LTP)
   augmentations are defined to represent the capabilities of the TP
   to be configured as an OTN UNI, together with the information
   about OTN label and bandwidth availability at the OTN UNI.

Te UNI Topology profiled YANG data model shown in {{uni-discovery-tree}} does not require the network to be a TE network and, therefore, it could be used as a core network topology model to discover UNIs (or in general any external link) for TE and non-TE networks as well as multi-layer networks encompassing both TE and non-TE layers.

The advantages of using the UNI Topology profiled YANG data model shown in {{uni-discovery-tree}}
as a core network topology model is to have a common solutions for:

-  discovering UNIs as well as inter-domain NNI links, which is
   applicable to any technology (TE or non TE) used at the UNI or
   within the network;

-  modelling non TE UNIs such as Ethernet, and TE UNIs such as OTN,
   as well as UNIs which can configured as TE or non-TE (e.g., being
   configured as either Ethernet or OTN UNI).

## Administrative and Operational status management {#admin-oper-state}

The management of administrative and operational state is independent from whether the network is TE or non-TE.

The YANG data model defined in {{!RFC8795}} supports the management of administrative and
operational state for nodes, termination points and links.
It also includes the possibility to associate some administrative names to network topologies, nodes, termination points and links.

The following profile of the YANG data model defined in {{!RFC8795}} can be used for
administrative and operational state management:

~~~~
   module: ietf-te-topology
     augment /nw:networks/nw:network/nw:network-types:
       +--rw te-topology!
     augment /nw:networks/nw:network:
       +--rw te-topology-identifier
       |  +--rw provider-id?   te-global-id
       |  +--rw client-id?     te-global-id
       |  +--rw topology-id?   te-topology-id
       +--rw te!
          +--rw name?                     string
     augment /nw:networks/nw:network/nw:node:
       +--rw te-node-id?   te-types:te-node-id
       +--rw te!
          +--rw te-node-attributes
          |  +--rw admin-status?          te-types:te-admin-status
          |  +--rw name?                  string
          +--ro oper-status?              te-types:te-oper-status
     augment /nw:networks/nw:network/nt:link:
       +--rw te!
          +--rw te-link-attributes
          |  +--rw name?                  string
          |  +--rw admin-status?          te-types:te-admin-status
          +--ro oper-status?              te-types:te-oper-status
     augment /nw:networks/nw:network/nw:node/nt:termination-point:
       +--rw te-tp-id?   te-types:te-tp-id
       +--rw te!
          +--rw admin-status?             te-types:te-admin-status
          +--rw name?                     string
          +--ro oper-status?              te-types:te-oper-status
~~~~
{:#admin-oper-state-tree title="Generic Topology with admin and operational state"}

Note: Understanding that the solution is generic would be more straightforward
if the 'name', 'admin-status' and 'oper-status' leafs were defined
under a container with a different name than 'te' (e.g., 'state-management') or directly under the parent data node (e.g., network).

The administrative and operational state management profiled YANG data model shown in {{admin-oper-state-tree}}
does not require the network to be a TE network and, therefore, it could be used as a core network topology model to
manage the administrative and operational state for nodes, termination points and links as well as the administrative names for networks, nodes, termination points and links.

## Overlay and Underlay Topologies {#overlay-underlay}

The navigation of the overlay/underlay relationship for nodes and links is independent from whether the overlay or underlay networks are TE or non-TE.

The YANG data model defined in {{!RFC8795}} supports the management of overlay/underlay
relationship for nodes and links, as described in section 5.8 of
{{!RFC8795}}.

The following profile of the YANG data model defined in {{!RFC8795}} can be used for
to manage overlay/underlay network data:

~~~~
   module: ietf-te-topology
     augment /nw:netorks/nw:network/nw:network-types:
       +--rw te-topology!
     augment /nw:networks/nw:network/nw:node:
       +--rw te-node-id?   te-types:te-node-id
       +--rw te!
          +--rw te-node-attributes
             +--rw underlay-topology {te-topology-hierarchy}?
                +--rw network-ref? -> /nw:networks/network/network-id
     augment /nw:networks/nw:network/nt:link:
       +--rw te!
          +--rw te-link-attributes
             +--rw underlay {te-topology-hierarchy}?
                +--rw enabled?                     boolean
                +--rw primary-path
                   +--rw network-ref?
                   |       -> /nw:networks/network/network-id
                   +--rw path-element* [path-element-id]
                      +--rw path-element-id              uint32
                      +--rw (type)?
                         +--:(numbered-link-hop)
                         |  +--rw numbered-link-hop
                         |     +--rw link-tp-id    te-tp-id
                         |     +--rw hop-type?     te-hop-type
                         |     +--rw direction?    te-link-direction
                         +--:(unnumbered-link-hop)
                            +--rw unnumbered-link-hop
                               +--rw link-tp-id    te-tp-id
                               +--rw node-id       te-node-id
                               +--rw hop-type?     te-hop-type
                               +--rw direction?    te-link-direction
~~~~
{:#overlay-underlay-tree title="Generic Topology with overlay/underlay information"}

Note: Understanding that the solution is generic would be more straightforward
if the 'underlay-topology' container or the 'underlay' container were defined
under a container with a different name than 'te' or directly under the parent 'node' or, respectively, 'link' data node.

The underlay/overlay network profiled YANG data model shown in {{overlay-underlay-tree}}
does not require the network to be a TE network and, therefore, it could be used as a core network topology model to manage the overlay/underlay navigation between different network topologies.

The advantages of using the underlay/overlay network profiled YANG data model shown in {{overlay-underlay-tree}}
as a core network topology model is to have a common solutions for navigating between overlay/underlay network topologies where:

- both the underlay and overlay network topologies are TE networks;
- both the underlay and overlay network topologies are non-TE networks;
- the underlay and overlay network topologies are TE and non-TE networks;
- the underlay or the overlay network topology is a multi-layer network encompassing both TE and non-TE layers.

### Supporting relationships in RFC8345

{{!RFC8345}} defines the modeling constructs for supporting relations, including supporting network (i.e. topology), supporting node, supporting link, and supporting termination point. These relation constructs facilitate network mappings and transformations. One use case is to map a customized topology to a native topology. The customized topology uses different name spaces from the native topology when naming nodes, links, or termination points. There is a supporting relationship between a modeling construct in the customized topography to its counterpart in the native topology. In such a relationship, the modeling constructs at both ends represent the same type of network objects, which can be network (i.e. topology), node, link, or termination point.

{{!RFC8795}} defines the modeling constructs for network overlay and underlay relations. When the network overlay technology is used, some network objects (nodes or links) in the overlay network are built on top of network objects in the underlay network. As a result, the overlay-underlay relationship is created between network objects in the overlay networks and other network objects in the underlay network. Between the network object pairs in the overlay-underlay relationship, the types of the network objects are usually not the same. The network object can be a node in the overlay network, while the related underlay network object is a topology in the underlay network. A link in the overlay network can be related to a path that consists of a sequence of nodes and links in the underlay network.

## Nodes with switching limitations {#switching-limitations}

It is worth noting that a node, as defined in {{!RFC8345}}, does not provide any information about the possible connectivity between its TPs.

A node can have some switching limitations where connectivity is not
possible between all its TP pairs, for example when:

-  the node represents a physical device with switching limitations;

-  the node represents an abstraction of a network topology.

The management of nodes with switching limitations is independent from whether the network is TE or non-TE.

The YANG data model defined in {{!RFC8795}} supports the management of nodes with switching limitations by defining
the node connectivity matrix to represent feasible connections
between termination points across the nodes.

The following profile of the YANG data model defined in {{!RFC8795}} can be used for
modelling nodes with connectivity constraints:

~~~~
   module: ietf-te-topology
     augment /nw:networks/nw:network/nw:network-types:
       +--rw te-topology!
     augment /nw:networks/nw:network/nw:node:
       +--rw te-node-id?   te-types:te-node-id
       +--rw te!
          +--rw te-node-attributes
             +--rw connectivity-matrices
                +--rw number-of-entries?     uint16
                +--rw is-allowed?            boolean
                +--rw connectivity-matrix* [id]
                   +--rw id                  uint32
                   +--rw from
                   |  +--rw tp-ref?               leafref
                   +--rw to
                   |  +--rw tp-ref?               leafref
                   +--rw is-allowed?              boolean
~~~~
{:#switching-limitations-tree title="Generic Topology with connectivity constraints"}

Note: Understanding that the solution is generic would be more straightforward
if the 'connectivity-matrices' container were defined
under a container with a different name than 'te' or directly under the parent 'node' data node.

The node connectivity constraints profiled YANG data model shown in {{switching-limitations-tree}}
does not require the network to be a TE network and, therefore, it could be used as a core network topology model to
manage nodes
with certain connectivity constraints.

## Multipoint links {#mp-links}

The management of multipoint links is independent from whether the links are TE or non-TE.

According to {{Section 4.4.4 of !RFC8345}}, multipoint links can be "represented through pseudonodes (similar to IS-IS, for example)".

Each access point can have different directionality with respect to the multipoint link, as shown in {{mp-link-example}}:
- an access point of a multipoint link can be able to both transmit and receive traffic: this access point can be modelled as a TP (e.g., TP A in {{mp-link-example}}) terminating two links, one incoming link (e.g., Link 1 in {{mp-link-example}}) and one outgoing link (e.g., Link 2 in {{mp-link-example}});
- an access point of a multipoint link can be able only to receive traffic: this access point can be modelled as a TP (e.g., TP B in {{mp-link-example}}) with only one incoming link (e.g., Link 3 in {{mp-link-example}});
- an access point of a multipoint link can be able only to transmit traffic: this access point can be modelled as a TP (e.g., TP C in {{mp-link-example}}) with only one outgoing link (e.g., Link 4 in {{mp-link-example}}).

~~~~ ascii-art
{::include ./figures/mp-link-example.txt}
~~~~
{:#mp-link-example title="Example of a pseudonode modelling a multipoint link"}

The switching limitations of the pseudonode, as defined in {{switching-limitations}}, provides sufficient information to identify the type of multipoint link:
- in case of multipoint links, the connectivity matrix of the pseudnode, reports that connectivity is enabled by default between all the TPs of the node;
- in case of point-to-multipoint links, the connectivity matrix of the pseudnode, reports that connectivity is possible only between the root TP and the leaf TPs
>>
- if the point-to-multipoint link is bidirectional, the connectivity matrix of the pseudonodes reports that connectivity is possible from the root TP to the leaf TPs as well as from the leaf TPs to the root TP;
>>
- the connectivity matrix of the psuedonode can also describe point-to-multipoint links with more than one root (also known as rooted-multipoint links), indicating also whether connectivity between root TPs is allowed or not;
- in case of hybrid multipoint links, as defined in {{?I-D.ietf-nmop-simap-concept}}, the connectivity matrix of the pseunode reports the list of TP pairs for which connectivity is allowed or not allowed.

It is worth noting that the directionality of the access point of a multipoint link overrides the switching limitations of the pseudonode. For example, even if the connectivity matrix of the psuedonode in {{mp-link-example}} indicates that connectivity is possible between TP A and TP B, the traffic entering the pseudonode from TP A cannot be transmitted by TP B since there is no outgoing link from TP B.

Therefore, the connectivity matrix of a pseudonode modelling a point-to-multipoint unidirectional link, does not need to report that connectivity is only possible from the root TP to the leaf TPs but it can report that connectivity is possible by default between all the TPs of the node.
The pseudonode represents a point-to-multipoint unidirectional link, as indicated by a single root TP that can only receive traffic and one or more leaf TPs that can only transmit traffic.

~~~~ ascii-art
{::include ./figures/p2mp-link-example.txt}
~~~~
{:#p2mp-link-example title="Example of a pseudonode modelling an undirectional point-to-multipoint link"}

For example, {{p2mp-link-example}} shows an example of a pseudonode representing an unidirectional point-to-multipoint link where the TP A is the root TP and TPs B and C are the two leaf TPs.

# Technology-specific augmentations {#augmentations}

   There are two main options to define technology-specific Topology
   Models which can use the attributes defined in the TE Topology Model
   {{!RFC8795}}.

   Both options are applicable to any possible profile of the TE
   Topology Model, such as those defined in {{examples}}.

   The first option is to define a technology-specific TE Topology Model
   which augments the TE Topology Model, as shown in {{te-augment-fig}}:

~~~~
                           +-------------------+
                           | Network Topology  |
                           +-------------------+
                                     ^
                                     |
                                     | Augments
                                     |
                         +-----------+-----------+
                         |      TE Topology      |
                         |       (profile)       |
                         +-----------------------+
                                     ^
                                     |
                                     | Augments
                                     |
                          +----------+----------+
                          | Technology-Specific |
                          |     TE Topology     |
                          +---------------------+
~~~~
{:#te-augment-fig title="Augmenting the TE Topology Model"}

This approach is more suitable for cases when the technology-specific
TE topology model provides augmentations to the TE Topology
constructs, such as bandwidth information (e.g., link bandwidth),
tunnel termination points (TTPs) or connectivity matrices. It also
allows providing augmentations to the Network Topology constructs,
such as nodes, links, and termination points (TPs).

This is the approach currently used in {{?I-D.ietf-ccamp-eth-client-te-topo-yang}}
and {{?I-D.ietf-ccamp-otn-topo-yang}}.

It is worth noting that a profile of the technology-specific TE
Topology model not using any TE topology attribute or constructs can
be used to address any use case that do not require these attributes.
In this case, only the 'te-topology' presence container of the TE
Topology Model needs to be implemented because it is the parent container
for the 'network-type' representing the technology-specific topology model.
Other data nodes defined in the TE Topology Model do not need to be implemented by this profile.

The second option is to define a technology-specific Network Topology
Model which augments the Network Topology Model and to rely on the
multiple inheritance capability, which is implicit in the network-
types definition of {{!RFC8345}}, to allow using also the generic
attributes defined in the TE Topology model:

~~~~
                    +-----------------------+
                    |    Network Topology   |
                    +-----------------------+
                        ^               ^
                        |               |
           Augments +---+               +--+ Augments
                    |                      |
          +---------+---+       +----------+----------+
          | TE Topology |       | Technology-specific |
          |  (profile)  |       |  Network Topology   |
          +-------------+       +---------------------+
~~~~
{:#multi-inheritance-fig title="Augmenting the Network Topology Model with multi-inheritance"}

This approach is more suitable in cases where the technology-specific
Network Topology Model provides augmentation only to the constructs
defined in the Network Topology Model, such as nodes, links, and
termination points (TPs). Therefore, with this approach, only the
generic attributes defined in the TE Topology Model could be used.

It is also worth noting that in this case, technology-specific
augmentations for the bandwidth information could not be defined.

In principle, it would be also possible to define both a technology
specific TE Topology Model which augments the TE Topology Model, and
a technology-specific Network Topology Model which augments the
Network Topology Model and to rely on the multiple inheritance
capability, as shown in {{double-augment-fig}}:

~~~~
                    +-----------------------+
                    |    Network Topology   |
                    +-----------------------+
                        ^               ^
                        |               |
           Augments +---+               +--+ Augments
                    |                      |
          +---------+---+       +----------+----------+
          | TE Topology |       | Technology-specific |
          |  (profile)  |       |  Network Topology   |
          +-------------+       +---------------------+
                 ^                         ^
                 |                         |
                 | Augments                | References
                 |                         |
      +----------+----------+              |
      | Technology-Specific +--------------+
      |     TE Topology     |
      +---------------------+
~~~~
{:#double-augment-fig title="Augmenting both the Network and TE Topology Models"}

This option does not provide any technical advantage with respect to
the first option, shown in {{te-augment-fig}}, but could be useful to add
augmentations to the TE Topology constructs and to re-use an already
existing technology-specific Network Topology Model.

It is worth noting that the technology-specific TE Topology model can
reference constructs defined by the technology-specific Network
Topology model but it could not augment constructs defined by the
technology-specific Network Topology model.

## Multi-inheritance {#multi-inheritance}

As described in section 4.1 of {{RFC8345}}, the network types should be defined
using presence containers to allow the representation of network subtypes.

The hierarchy of network subtypes can be single hierarchy, as shown in {{te-augment-fig}}.
In this case, each presence container contains at most one child presence container,
as shows in the JSON code below:

~~~~
{
  "ietf-network:ietf-network": {
    "ietf-te-topology:te-topology": {
      "example-te-topology": {}
    }
  }
}
~~~~

The hierarchy of network subtypes can also be multi-hierarchy, as shown in {{multi-inheritance-fig}} and {{double-augment-fig}}.
In this case, one presence container can contain more than one child presence containers, as show in the JSON codes below:

~~~~
{
  "ietf-network:ietf-network": {
    "ietf-te-topology:te-topology": {}
    "example-network-topology": {}
  }
}
~~~~

~~~~
{
  "ietf-network:ietf-network": {
    "ietf-te-topology:te-topology": {
      "example-te-topology": {}
    }
    "example-network-topology": {}
  }
}
~~~~

Other examples of multi-hierarchy topologies are described in
{{?I-D.ietf-teas-yang-sr-te-topo}}.

## Example (Link augmentation) {#example-link}

This section provides an example on how technology-specific
attributes can be added to the Link construct:

~~~~
      +--rw link* [link-id]
         +--rw link-id            link-id
         +--rw source
         |  +--rw source-node?   -> ../../../nw:node/node-id
         |  +--rw source-tp?     leafref
         +--rw destination
         |  +--rw dest-node?   -> ../../../nw:node/node-id
         |  +--rw dest-tp?     leafref
         +--rw supporting-link* [network-ref link-ref]
         |  +--rw network-ref
         |  |       -> ../../../nw:supporting-network/network-ref
         |  +--rw link-ref       leafref
         +--rw example-link-attributes
         |   <...>
         +--rw te!
            +--rw te-link-attributes
               +--rw name?                             string
               +--rw example-te-link-attributes
               |   <...>
               +--rw max-link-bandwidth
                  +--rw te-bandwidth
                     +--rw (technology)?
                        +--:(generic)
                        |  +--rw generic?   te-bandwidth
                        +--:(example)
                           +--rw example?   example-bandwidth
~~~~
{:#example-link-tree title="Augmenting the Link with technology-specific attributes"}

The technology-specific attributes within the example-link-attributes
container can be defined either in the technology-specific TE
Topology Model (Option 1) or in the technology-specific Network
Topology Model (Option 2 or Option 3). These attributes can only be
non-TE and do not require the implementation of the te container.

The technology-specific attributes within the
example-te-link-attributes container as well as the example
max-link-bandwidth can only be defined in the technology-specific TE
Topology Model (Option 1 or Option 3). These attributes can be TE or
non-TE and require the implementation of the te container.

# Open Issues {#open-issues}

## Implemented profiles {#implement}

When a server implements a profile of the TE topology model, there is no standardized mechanism for the server to report to the client the subset of the model being implemented.

This might not be an issue in case the TE topology profile is read by the the client because the server reports in the operational datastore only the leaves which have been implemented, as described
in section 5.3 of {{!RFC8342}}.

More investigation is instead required in case the TE topology profile is configured by the client, to  avoid that the client tries to write an attribute not used in the TE Topology profile implemented by the server.

It is also worth noting that the supported profile may also depend on other attributes
(for example the network type), so the YANG deviation mechanism is not applicable to this scenario.

Note: that this issue is also tracked in github as issue #161.

## Applicability to non-TE use cases

Extending the applicability of RFC8795 to non-TE use cases is important. However, it is desirable to avoid any debate about whether these use cases in section 2 are or are not TE.

Note: that this issue is also tracked in github as issue #276.

### Update UNI topology discovery use case

{{uni-discovery}} points to individual drafts and does reflect the progress made since then. For example, the UNI draft was replaced by other drafts that then led to the SAP model {{?RFC9408}}, which covers both UNI and NNI.

Note: that this issue is also tracked in github as issue #275.

# Security Considerations {#security}

This document provides only information about how the TE Topology
Model, as defined in {{!RFC8795}}, can be profiled to address some
scenarios which are not considered as TE.

As such, this document does not introduce any additional security
considerations besides those already defined in {{!RFC8795}}.

# IANA Considerations {#iana}

This document requires no IANA actions.

{: numbered="false"}

# Acknowledgments

The authors would like to thank Vishnu Pavan Beeram, Daniele Ceccarelli, Jonas Ahlberg and Scott Mansfield 
for providing useful suggestions for this draft.

This document was prepared using kramdown.

Initial versions of this document were prepared using 2-Word-v2.0.template.dot.
