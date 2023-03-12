%%%
title = "CBOR Web Token (CWT) Claims in COSE Headers"
ipr= "trust200902"
area = "Internet"
workgroup = "COSE"
submissiontype = "IETF"
keyword = ["COSE", "JOSE"]

[seriesInfo]
name = "Internet-Draft"
value = "draft-ietf-cose-cwt-claims-in-headers-latest"
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

Section 5.3 of the JWT RFC [@RFC7519] defined a similar mechanism for expressing selected JWT based claims as JOSE header parameters.  This JWT feature was motivated by the desire to have certain claims, such as the Issuer value, be visible to software processing the JWT, even though the JWT is encrypted.  No corresponding feature was standardized for CWTs, which was an omission that this specification corrects.

Directly including CWT claim values as COSE header parameter values would not work, since there are conflicts between the numeric header parameter assignments and the numeric CWT claim assignments.  Instead, this specification defines a single header parameter registered in the IANA "COSE Header Parameters" registry that creates a location to store CWT claims in a COSE header parameter.

# Terminology

# Representation

This document defines the following COSE header parameter:


|   Name          |  Label | Value Type | Value Registry |   Description   |
|-----------------|--------|------------|----------------|-----------------|
|   CWT claims    |  TBD (requested assignment 11)   | map        | [@!IANA.CWT]   | location for CWT claims in  COSE headers   |

The following is a non-normative description for the value type of the CWT claim header parameter using CDDL [@RFC8610].

```
CWT-Claims = {
 * Claim-Label => any
}

Claim-Label = int / text
```

It is RECOMMENDED that the CWT claims header parameter is used only in a protected header to avoid the contents being malleable. The header parameter MUST only occur once in either the protected or unprotected header of a COSE structure.

# Privacy Considerations

Some of the registered CWT claims may contain privacy-sensitive information. Therefore care must be taken when expressing CWT claims in COSE headers.

# Security Considerations

In cases where CWT claims are both present in the payload and the header, an application receiving such as structure MUST verify that their values are identical, unless the application defines other specific processing rules for these claims.

# IANA Considerations

IANA is requested to register the new COSE Header parameter in the table in (#representation) in the "COSE Header Parameters" registry [@!IANA.COSE].

{backmatter}

# Document History

-03

* Added recommendation around header treatment in protected vs unprotected.

-02

* Added CDDL description for CWT claim value.

-01

* Changed example from Key ID to Issuer.

-00

* Created draft-ietf-cose-cwt-claims-in-headers-00 from draft-looker-cose-cwt-claims-in-headers-00 following working group adoption.

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
