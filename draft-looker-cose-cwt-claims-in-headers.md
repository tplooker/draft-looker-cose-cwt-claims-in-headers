%%%
title = "CBOR Web Token (CWT) Claims in COSE Headers"
ipr= "trust200902"
area = "Internet"
workgroup = "COSE"
submissiontype = "IETF"
keyword = ["COSE", "JOSE"]

[seriesInfo]
name = "Internet-Draft"
value = "draft-looker-cose-cwt-claims-in-headers-latest"
status = "standard"

[pi]
toc = "yes"

[[author]]
initials = "T."
surname = "Looker"
fullname = "Tobias Looker"
#role = "editor"
organization = "Mattr"
  [author.address]
  email = "tobias.looker@mattr.global"

[[author]]
initials = "M."
surname = "Jones"
fullname = "Michael B. Jones"
organization = "Microsoft"
  [author.address]
  email = "mbj@microsoft.com"
  uri = "https://self-issued.info/"

%%%

.# Abstract

This document describes how to use CBOR Web Token (CWT) claims in the header of any COSE structure. This functionality helps to facilitate applications that wish to make use of CBOR Web Token (CWT) claims in encrypted COSE structures and or COSE structures featuring detached signatures.

{mainmatter}

# Introduction

In some applications of COSE it is useful to have a standard representation of [CWT] claims available in the header. These include encrypted COSE structures which may or may not be an encrypted CWT and or those featuring a detached signature.

Section 5.3 of the [JWT] RFC defined a similar mechanism for expressing JWT based claims in JOSE headers. However because the COSE and CWT RFC's were standardized at different times and as such have separate IANA registries for registration, including the assignment of the same numeric labels for distinct purposes, they are in effect different namespaces. This means the same approach taken by the [JWT] RFC which was to have awareness of registrations across the two registries to ensure they never collided cannot be accomplished with COSE and CWT. Instead this document defines a single header parameter in the COSE header IANA registry which creates a location to store CWT claims in a COSE header.

# Terminology

# Representation

This document defines the following header parameter


|   Name          |  Label | Value Type | Value Registry |   Description   |
|-----------------|--------|------------|----------------|-----------------|
|   cwt claims    |  TBD   | map        | [@!IANA.CWT]   | location for CWT claims in  COSE headers   |


# Privacy Considerations

Some of the registered CWT claims may contain privacy-sensitive information. Therefore care MUST be taken when expressing CWT claims in COSE headers.

# Security Considerations

In cases where CWT claims are both present in the payload and the header, an application receiving such as structure SHOULD verify that their values are identical, unless the application defines other specific processing rules for these claims.

# IANA Considerations

IANA is requested to register the new COSE Header parameters in Table 1 in the "COSE Header Parameters" registry. The "Value Registry" field is empty for all of the items. For each item, the 'Reference' field points to this document.

IANA is requested to register the new COSE Header parameter in the table present in (#representation) in the "COSE Header Parameters" registry [@!IANA.COSE].

{backmatter}

# Document History

-00

<reference anchor="IANA.COSE" target="https://www.iana.org/assignments/cose/cose.xhtml#header-parameters">
 <front>
   <title>COSE Header Parameters</title>
   <author><organization>IANA</organization></author>
 </front>
</reference>

<reference anchor="IANA.CWT" target="https://www.iana.org/assignments/cwt/cwt.xhtml">
 <front>
   <title>CBOR Web Token (CWT) Claims</title>
   <author><organization>IANA</organization></author>
 </front>
</reference>
