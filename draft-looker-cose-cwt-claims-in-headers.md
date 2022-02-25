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

This specification describes how to use CBOR Web Token (CWT) claims in the header of any COSE structure. This functionality helps to facilitate applications that wish to make use of CBOR Web Token (CWT) claims in encrypted COSE structures and or COSE structures featuring detached signatures.

{mainmatter}

# Introduction

In some applications of COSE (todo definition)...

Cite the section 5.3 from JWT

State why technically you cannot do this with CBOR without it.

Why???

When a COSE structure is an encrypted CWT

When a COSE structure is leveraging a detached signature

This normal intended to be used when the object is a CWT and you are replicating the claims into the header.
However detached signature is also a case

# Terminology

# Representation

TODO example but human readable

# Privacy Considerations

Not advisable to replicated privacy sensitive claims into the COSE header

Dont put MUSTs here, but you can provide guidance.

# Security Considerations

TODO any application of claims in CWT?

Possibility of data structures being created where replicated claims are not the same as the body, software processing should attempt to equate claims and reject if they are not the same.

Don't put MUSTs here, but you can provide guidance.

# IANA Considerations

## CWT Claim

This section registers the following values in the IANA "CBOR Web Token (CWT) Claims" registry [@!IANA.CWT].

- Claim Name: Replicated CWT Claims
- Claim Description: CWT claims
- JWT Claim Name: N/A
- Claim Key: TBD
- Claim Value Type(s): map
- Change Controller: TBD
- Specification Document(s): {#representation}

{backmatter}

# Document History

-00

<reference anchor="IANA.CWT" target="https://www.iana.org/assignments/cwt/cwt.xhtml">
 <front>
   <title>CBOR Web Token (CWT) Claims</title>
   <author><organization>IANA</organization></author>
 </front>
</reference>
