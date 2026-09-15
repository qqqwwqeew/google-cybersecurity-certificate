# Wireshark SYN Flood Analysis

## Overview

This project analyzes network traffic from a simulated **SYN flood Denial-of-Service (DoS) attack** using Wireshark TCP/HTTP logs.

The investigation focuses on identifying abnormal TCP connection attempts, analyzing the three-way handshake, and determining how the attack affected legitimate website visitors.

## Investigation

The network traffic analysis identified:

* **Attacker IP:** `203.0.113.0`
* **Target server:** `192.0.2.1`
* **Target port:** `443`
* **Protocol:** TCP
* **Attack type:** SYN flood
* **Impact:** Website connection failures and timeouts

The attacker repeatedly sent SYN packets to TCP port 443 at a high rate. The server initially responded with SYN/ACK packets, but eventually became unable to handle legitimate connection attempts.

## TCP Three-Way Handshake

A normal TCP connection follows three steps:

```text
Client → Server: SYN
Server → Client: SYN/ACK
Client → Server: ACK
```

After the connection is established, the client can send an HTTP request and receive a response from the web server.

## Attack Pattern

The traffic showed a clear difference between normal and malicious behavior.

### Normal traffic

```text
SYN → SYN/ACK → ACK → HTTP GET → 200 OK
```

### SYN flood traffic

```text
SYN
SYN
SYN
SYN
SYN
...
```

The attacker continued sending SYN requests instead of behaving like a normal website visitor.

## Impact

As the attack continued, legitimate users began experiencing connection failures.

The logs contained:

* `RST, ACK` packets
* `504 Gateway Time-out` errors
* Failed connection attempts from legitimate users
* A large number of repeated SYN packets from the attacker

Eventually, the web server stopped responding to legitimate visitor traffic while the attack traffic continued.

## Key Finding

Because the SYN flood originated from a single IP address, this event is classified as a **direct DoS attack**, rather than a distributed denial-of-service (DDoS) attack.

## Tools Used

* Wireshark
* TCP/HTTP traffic analysis
* TCP three-way handshake analysis
* Network security fundamentals

## Evidence

The repository contains the incident analysis and supporting traffic evidence used to identify the SYN flood attack.
