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
  RFC9000:

informative:
  RFC5905:
  RFC6335:
  RFC7384:
  RFC8446:
  I-D.draft-ietf-ntp-ntpv5:

...

--- abstract

This document describes the use of the Network Time Security protocol over QUIC.

--- middle

# Introduction

Network Time Security (NTS) [RFC8915] defines the NTS Key Establishment (NTS-KE) protocol, which uses TLS 1.3 [RFC8446] over TCP to secure the distribution of NTP server information and cookies.

There are several reasons to consider the use of QUIC [RFC9000] for NTS Key Establishment services, namely QUIC just like NTP is based on UDP leading to a potential simplification in implementation and network management. Implementers can also choose to enable 0-RTT and connection resumption, minimising the amount of traffic to a key establishment server in order to maintain or resume a connection.

Not all of QUIC's capabilities are applicable to providing key establishment for secure time, however these should not pose any notable concerns for implementators who would most likely be using existing QUIC implementations.

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

The following error codes are defined for use when abruptly terminating streams, for use as application protocol error codes when aborting reading of streams, or for immediately closing connections.

Unrecognised Critical Record (0x0):
 : The server received an NTS record with critical bit set, which could not be understood by the server.

Bad Request (0x1):
 : The server received a request that is not complete or syntactically well-formed.

Internal Server Error (0x2):
 : The server MUST respond with this error if it is unable to respond properly due to an internal condition.

No Error (0x1023):
 : No error. This is used when the connection or stream needs to be closed, but there is no error to signal.

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

Thanks to {{{Lucas Pardue}}} for early feedback and suggestions.
