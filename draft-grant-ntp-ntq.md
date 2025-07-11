---
title: "Network Time Security over QUIC"
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

informative:
  RFC5905:
  RFC6335:
  RFC7384:
  RFC8915:
  I-D.draft-ietf-ntp-ntpv5:

...

--- abstract

This document describes the implementation of the Network Time Security protocol over QUIC.

--- middle

# Introduction

Network Time Security (NTS) [RFC8915] defines the 

There are several key reasons to consider the use of QUIC for NTS Key Establishment services; QUIC like NTP is based on UDP, which means that networks or network segments.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

This document uses the terminology established in {{I-D.draft-ietf-ntp-ntpv5}}.

# QUIC Connectivity

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

TODO acknowledge that perhaps this was not the smartest idea.
