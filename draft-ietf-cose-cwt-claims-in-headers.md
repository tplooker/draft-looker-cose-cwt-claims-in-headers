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
organization = "Self-Issued Consulting"
  [author.address]
  email = "michael_b_jones@hotmail.com"
  uri = "https://self-issued.info/"

%%%

.# Abstract

This document describes how to include CBOR Web Token (CWT) claims in the header parameters of any COSE structure. This functionality helps to facilitate applications that wish to make use of CBOR Web Token (CWT) claims in encrypted COSE structures and/or COSE structures featuring detached signatures, while having some of those claims be available before decryption and/or without inspecting the detached payload.

{mainmatter}

# Introduction

In some applications of COSE, it is useful to have a standard representation of CWT claims [@!RFC8392] available in the header parameters. These include encrypted COSE structures, which may or may not be an encrypted CWT and/or those featuring a detached signature.

Section 5.3 of JSON Web Token (JWT) [@RFC7519] defined a similar mechanism for expressing selected JWT based claims as JOSE header parameters.  This JWT feature was motivated by the desire to have certain claims, such as the Issuer value, be visible to software processing the JWT, even though the JWT is encrypted.  No corresponding feature was standardized for CWTs, which was an omission that this specification corrects.

Directly including CWT claim values as COSE header parameter values would not work, since there are conflicts between the numeric header parameter assignments and the numeric CWT claim assignments.  Instead, this specification defines a single header parameter registered in the IANA "COSE Header Parameters" registry that creates a location to store CWT claims in a COSE header parameter.

## Requirements Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 [@!RFC2119] [@!RFC8174] when, and only when, they appear in all capitals, as shown here.

# Representation

This document defines the following COSE header parameter:


|   Name          |  Label | Value Type | Value Registry |   Description   |
|-----------------|--------|------------|----------------|-----------------|
|   CWT Claims    |  TBD (requested assignment 15)   | map        | [@!IANA.COSE]  | Location for CWT Claims in COSE Header Parameters |

The following is a non-normative description for the value type of the CWT claim header parameter using CDDL [@RFC8610].

```
CWT-Claims = {
 * Claim-Label => any
}

Claim-Label = int / text
```

In cases where CWT claims are present both in the payload and the header of a CWT, an application receiving such a structure MUST verify that their values are identical, unless the application defines other specific processing rules for these claims.

It is RECOMMENDED that the CWT Claims header parameter is used only in a protected header to avoid the contents being malleable. The header parameter MUST only occur once in either the protected or unprotected header of a COSE structure.

The CWT Claims header parameter MAY be used in any COSE object using header parameters, such as COSE_Sign objects.  Its use is not restricted to CWTs.

# Privacy Considerations

Some of the registered CWT claims may contain privacy-sensitive information. Since CWT claims in COSE headers are not encrypted, when privacy-sensitive information is present in these claims, applications and protocols using them should ensure that these COSE objects are only made visible to parties for which it is appropriate for them to have access to this sensitive information.

# Security Considerations

Implementers should also review the security considerations for CWT, which are documented in Section 8 of [@!RFC8392].

As described in [@RFC9052], if the COSE payload is transported separately ("detached content"), then it is the responsibility of the application to ensure that it will be transported without changes.

The reason for applications to verify that CWT claims that are present both in the payload and the header of a CWT are identical, unless it defines other specific processing rules for these claims, is to eliminate potential confusion that might arise by having different values for the same claim, which could result in inconsistent processing of such claims.

Profiles define how to use CWT claims for particular applications, whether they are in the COSE payload or the CWT Claims header parameter, or both.  Therefore, understanding how to process the CWT Claims requires unambiguously knowing the profile being used.  A recommended way to include this information in the COSE structure is use of the `typ` (type) Header Parameter [@I-D.ietf-cose-typ-header-parameter].  Other methods for determining the profile can also be used.

# IANA Considerations

IANA is requested to register the new COSE header parameter "CWT Claims" in the table in (#representation) in the "COSE Header Parameters" registry [@!IANA.COSE].

{backmatter}

# Acknowledgements {#Acknowledgements}

We would like to thank
Daisuke Ajitomi,
Claudio Allocchio,
Carsten Bormann,
Laurence Lundblade,
Ivaylo Petrov,
Ines Robles,
Orie Steele,
Hannes Tschofenig,
Paul Wouters,
and
Peter Yee
for their valuable contributions to this specification.

# Document History

-08

* Added Security Consideration about profiles and processing CWT claims.

-07

* Added Privacy Consideration about unencrypted claims in header parameters.
* Added Security Consideration about detached content.
* Added Security Consideration about claims that are present both in the payload and the header of a CWT.
* Changed requested IANA COSE Header Parameter assignment number from 13 to 15 due to subsequent assignments of 13 and 14.
* Acknowledged last call reviewers.

-06

* Changed requested IANA COSE Header Parameter assignment number from 11 to 13 due to Countersignature being allocated 11.
* Reference correct registry IANA COSE Header Parameters.

-05

* Added Acknowledgements section.
* Addressed WGLC feedback.  Specifically...
* Added statement about being able to use the header parameter in any COSE object.
* Moved statment about verifing that claim values present in both the header and payload are identical from the Security Considerations to the body of the specification.

-04

* Update author affiliation.
* Add standard reference to RFC terminology.
* Added reference to security considerations from RFC8392.

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
