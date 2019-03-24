---
title: Gopher over HTTPS (GoH)
abbrev: GoH
docname: draft-sebdeckers-gopher-over-https-latest
area: art
category: exp
ipr: trust200902

stand_alone: yes
pi:
  toc: yes
  tocdepth: 2
  sortrefs: yes
  symrefs: yes

author:
-
  ins: S. Deckers
  name: Sebastiaan Deckers
  org: Commons Host
  email: sebdeckers83@gmail.com
-
  ins: B. English
  name: Bryan English
  org: Independent
  email: bryan@bryanenglish.com

--- abstract

This document describes a protocol for sending Gopher requests and receiving Gopher responses over HTTPS. Each Gopher request-response pair is mapped to an HTTPS exchange.

--- middle

# Introduction

This document defines a specific protocol, Gopher over HTTPS (GoH), for sending Gopher {{!RFC1436}} requests, as Gopher {{!RFC4266}} URIs, and receiving Gopher responses over HTTPS {{!RFC7540}}, using https {{!RFC2818}} URIs (and therefore TLS {{!RFC8446}} security for integrity and confidentiality). Each Gopher request-response pair is mapped into an HTTPS exchange.

# Terminology

{::boilerplate bcp14}

A server that supports this protocol is called a "GoH server" to differentiate it from a "Gopher server". Similarly, a client that supports this protocol is called a "GoH client".

# HTTP and Gopher URL

A GoH client is configured with a URI Template {{!RFC6570}} which describes how to construct the URL to use for the HTTP request. Discovery of the URI Template is beyond the scope of this protocol. The single variable "url" refers to the Gopher URI of the request.

When an HTTPS request is constructed using the URI template, the Gopher URI MUST be percent-encoded.

Example URI Template:

    https://goh.example.com/gopher-proxy{?url}

Given the Gopher URI of the Gopher request:

    gopher://gopher.example.com

The resulting HTTPS request URI is:

    https://goh.example.com/gopher-proxy?url=gopher%3A%2F%2Fgopher.example.com

# The HTTP Exchange

## The HTTP Request

A GoH client encodes a single Gopher request into an HTTP request. The HTTP request MUST use the GET method. A GoH client SHOULD include an HTTP Accept request header field with the media type "application/gopher".

    Accept: application/gopher

## The HTTP Response

A GoH server must include an HTTP Content-Type response header field with the media type "application/gopher" to indicate the body contains a Gopher response.

    Content-Type: application/gopher

A GoH server's HTTP response message has the Gopher response as its message body.

# IANA Considerations

## Registration of the "application/gopher" Media Type

Type name: application

Subtype name: gopher

Required parameters: N/A

Optional parameters: N/A

Encoding considerations: This is either in text or binary format. The contents are a Gopher response as defined in RFC1436.

Security considerations: The content is a Gopher response. Security issues are not discussed in RFC1436.

Interoperability considerations: None.

Published specification: RFC XXXX.

Applications that use this media type:
  Gopher over HTTPS clients and servers, or other systems using Gopher responses.

Additional information:

  Deprecated alias names for this type: N/A
  Magic number(s): N/A
  File extension(s): N/A
  Macintosh file type code(s): N/A

Person & email address to contact for further information:
  Sebastiaan Deckers <sebdeckers83@gmail.com>

Intended usage: COMMON

Restrictions on usage: N/A

Author: Sebastiaan Deckers <sebdeckers83@gmail.com>

Change controller: IESG

# Privacy Considerations

# Security Considerations

# Operational Considerations
