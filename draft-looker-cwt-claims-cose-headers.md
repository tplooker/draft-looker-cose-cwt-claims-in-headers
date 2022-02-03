%%%
title = "CBOR Web Token (CWT) Claims in COSE Headers"
ipr= "none"
area = "Internet"
workgroup = "none"
submissiontype = "IETF"
keyword = [""]

[seriesInfo]
name = "Individual-Draft"
value = "draft-looker-cwt-claims-cose-headers-latest"
status = "informational"

[[author]]
initials = "T."
surname = "Looker"
fullname = "Tobias Looker"
#role = "editor"
organization = "Mattr"
  [author.address]
  email = "tobias.looker@mattr.global"
%%%

.# Abstract

This specification describes how to use CBOR Web Token (CWT) claims in the header of any COSE structure. This functionality helps to facilitate applications that wish to make use of CBOR Web Token (CWT) claims in encrypted COSE structures and or COSE structures featuring detached signatures.

{mainmatter}

# Introduction

In some applications of COSE (todo definition)...

When a COSE structure is an encrypted CWT

When a COSE structure is leveraging a detached signature

# Terminology

# Representation

TODO

# Security Considerations

TODO

# IANA Considerations

TODO

## CWT Claim

- Claim Name: cwt
- Claim Description: CWT claims
- JWT Claim Name: N/A
- Claim Key: TBD
- Claim Value Type(s): map
- Change Controller: TBD
- Specification Document(s): {#representation}

# Acknowledgments

TODO