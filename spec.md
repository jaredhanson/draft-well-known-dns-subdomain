---
docname: draft-hanson-well-known-dns-subdomain-00
category: std

title: Well-Known DNS Subdomain
abbrev: OAuth 2.0 SCSS
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
indirectly through higher-level discovery protocols such as WebFinger
{{!RFC7033}}.  For example, OpenID Connect uses well-known locations to discover
the identity provider for a person as well as to discover metadata about the
identity provider.

The hosting of services that implement these protocols is often delegated to a
third-party service provider.  For instance, acme.example may delegate identity
services to idaas.example.  Typically, such delegation is accompanied by a DNS
CNAME record from id.acme.example to acme.idaas.example.

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


