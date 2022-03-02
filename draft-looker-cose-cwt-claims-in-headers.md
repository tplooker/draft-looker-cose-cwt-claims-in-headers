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

This document describes how to include CBOR Web Token (CWT) claims in the header parameters of any COSE structure. This functionality helps to facilitate applications that wish to make use of CBOR Web Token (CWT) claims in encrypted COSE structures and/or COSE structures featuring detached signatures, while having some of those claims be available before decryption and/or without inspecting the detached payload.

{mainmatter}

# Introduction

In some applications of COSE, it is useful to have a standard representation of CWT claims [@RFC8392] available in the header parameters. These include encrypted COSE structures, which may or may not be an encrypted CWT and/or those featuring a detached signature.

Section 5.3 of the JWT RFC [@RFC7519] defined a similar mechanism for expressing selected JWT based claims as JOSE header parameters.  This JWT feature was motivated by the desire to have certain claims, such as Key ID values, be visible to software processing the JWT, even though the JWT is encrypted.  No corresponding feature was standardized for CWTs, which was an omission that this specification corrects.

Directly including CWT claim values as COSE header parameter values would not work, since there are conflicts between the numeric header parameter assignments and the numeric CWT claim assignments.  Instead, this specification defines a single header parameter registered in the IANA "COSE Header Parameters" registry that creates a location to store CWT claims in a COSE header parameter.

# Terminology

# Representation

This document defines the following COSE header parameter:


|   Name          |  Label | Value Type | Value Registry |   Description   |
|-----------------|--------|------------|----------------|-----------------|
|   cwt claims    |  TBD (requested assignment 11)   | map        | [@!IANA.CWT]   | location for CWT claims in  COSE headers   |


# Privacy Considerations

Some of the registered CWT claims may contain privacy-sensitive information. Therefore care must be taken when expressing CWT claims in COSE headers.

# Security Considerations

In cases where CWT claims are both present in the payload and the header, an application receiving such as structure MUST verify that their values are identical, unless the application defines other specific processing rules for these claims.

# IANA Considerations

IANA is requested to register the new COSE Header parameter in the table in (#representation) in the "COSE Header Parameters" registry [@!IANA.COSE].

{backmatter}

# Document History

-00

* Initial version

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
