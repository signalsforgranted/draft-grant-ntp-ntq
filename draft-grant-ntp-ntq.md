---
title: "Network Time Security over QUIC"
abbrev: "NTS over QUIC"
category: info
docname: draft-grant-ntp-ntq-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: "Internet"
workgroup: "Network Time Protocols"
venue:
  group: "Network Time Protocols"
  type: "Working Group"
  mail: "ntp@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/ntp/"
  github: "signalsforgranted/draft-grant-ntp-ntq"
  latest: "https://signalsforgranted.github.io/draft-grant-ntp-ntq/draft-grant-ntp-ntq.html"
author:
 -
    fullname: Sarah Grant
    email: sarah.grant.ietf@gmail.com

normative:
  RFC8915:

informative:
  RFC5905:
  RFC6335:
  RFC7384:
  RFC8446:
  RFC9000:
  I-D.draft-ietf-ntp-ntpv5:

...

--- abstract

This document describes the use of the Network Time Security protocol over QUIC.

--- middle

# Introduction

Network Time Security (NTS) [RFC8915] defines the NTS Key Establishment (NTS-KE) protocol, which uses TLS 1.3 [RFC8446] over TCP to secure the distribution of NTP server information and cookies.

There are several key reasons to consider the use of QUIC for NTS Key Establishment services; QUIC like NTP is based on UDP, which means that networks or network segments operating time services can restrict

Not all of QUIC's capabilities are applicable to providing key establishment, however these should not pose any notable concerns for implementators who would most likely be using existing QUIC implementations.

**TODO**: Define what QUIC features aren't of use

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# QUIC Connectivity

## Connection Initiation

By default, servers should listen and accept QUIC connections on UDP port 4460, unless there is a mutual agreement to use another port.

NTS key establishment connections are established as described in the QUIC transport specification [RFC9000]. During connection establishment support is indicated with the client offering, and the server accepting the Application-Layer Protocol Negotiation (ALPN) token "ntske/1" as per [RFC8915].

**TODO**: Confirm ALPN reuse

All key establishment requests and responses MUST take place through the use of streams; other types MUST NOT be used. The client must initiate an initial bidirectional stream, starting from stream 0. After each complete key establishment request has been sent, it MUST send a STREAM FIN message to indicate no further data be sent.

All payloads sent within the stream must be in accordance with Section 4, [RFC8915].

## Connection Shutdown

**TODO**: Discuss connection cessation, including GOAWAY behaviour

## Error Handling

**TODO**: Error codes should be specified, however it's worth noting that in NTS the code point 0x0 is an error, whereas in QUIC derived protocols 0x0 usually signals that there is no error.

# Security Considerations

General security considerations for time protocols are discussed in RFC 7384 [RFC7384].

**TODO**: Security considerations

# IANA Considerations

## Service Name and Transport Protocol Port Number Registry

IANA is requested to allocate the following entry in the Service Name and Transport Protocol Port Number Registry [RFC6335]:

  Service Name:
  : ntske

  Transport Protocol:
  : udp

  Assignee:
  : IESG <iesg@ietf.org>

  Contact:
  : IETF Chair <chair@ietf.org>

  Description:
  : Network Time Security Key Establishment

  Reference:
  : This Document

  Port Number:
  : 4460


--- back

# Acknowledgments
{:numbered="false"}

Thanks to Lucas Pardue for early feedback and suggestions.
