---
docname: draft-hanson-well-known-dns-subdomain-00
category: std

title: Well-Known DNS Subdomain
abbrev: Well-Known DNS
author:
  -
    ins: J. Hanson
    name: Jared Hanson
    org: Okta
    email: jared.hanson@okta.com

area: Security
workgroup: Web Authorization Protocol

--- abstract

This memo defines a subdomain for "well-known locations", "well-known".

--- middle

# Introduction

Web-based protocols often require the discovery of resources or metadata
associated with a host.  Use of Well-Known Uniform Resource Identifers (URIs)
{{!RFC8615}} addresses this problem by reserving a path prefix, "/.well-known/",
which can be used by protocols that need to define a resource for such metadata.

This prefix has been adopted by numerous protocols, either directly or
indirectly through discovery protocols such as WebFinger {{!RFC7033}}.  For
example, OpenID Connect uses well-known locations to discover the identity
provider for a person as well as to discover metadata about the identity
provider.

The hosting of services that implement these protocols is often delegated to a
third-party service provider.  For instance, acme.example may delegate identity
services to idaas.example.  Typically, such delegation is accompanied by a DNS
CNAME record aliasing id.acme.example to acme.idaas.example.

While it is possible to delegate the service itself, discovery of that service
using well-known URIs remains undelegated, as it occurs via the well-known location
on the parent domain.  For instance, acme.example must provide a WebFinger service
at 'https://acme.example/.well-known/webfinger' to allow applications to discover
the delegation of OpenID Connect to acme.idaas.example.

Deployment experience suggests that the inability to delegate discovery in the
same manner as delegating the service to be discovered negatively impacts the
discovery of such protocols - to the point of discovery not being deployed and
therefore unavailable to applications.

To address this, this memo reserves a DNS subdomain, "well-known".  Protocols
can register their use of this subdomain in order to host resources or metadata
needed for discovery.

# Notational Conventions

{::boilerplate bcp14}

# Well-Known Subdomains

A well-known subdomain is a domain name that contains the label "well-known",
prefixed by a label registered to an application utilizing well-known
subdomains.

For example, if an application registers the label 'example', the corresponding
well-known subdomain of 'example.com' would be 'example.well-known.example.com'.

Resources or metadata obtained from a well-known subdomain are associated with
the parent domain above the "well-known" label.  Effectively, this is a naming
convention for hosting of resources that provide metadata about the parent
domain.

