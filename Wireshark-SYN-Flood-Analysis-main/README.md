# Wireshark SYN Flood Analysis

A simulated network-security investigation of a SYN flood Denial-of-Service (DoS) attack using Wireshark TCP/HTTP traffic data.

## Objective

Identify abnormal TCP connection attempts, determine the attack pattern, and document its effect on legitimate website traffic.

## Investigation

| Indicator | Value |
|---|---|
| Attacker IP | 203.0.113.0 |
| Target server | 192.0.2.1 |
| Target port | 443 |
| Protocol | TCP |
| Attack type | SYN flood |
| Impact | Connection failures and timeouts |

The attacker repeatedly sent SYN packets to TCP port 443 at a high rate. The server initially responded with SYN/ACK packets, but legitimate connection attempts subsequently failed.

## TCP Three-Way Handshake

A normal TCP connection follows:

Client → Server: SYN
Server → Client: SYN/ACK
Client → Server: ACK

### Normal traffic

SYN → SYN/ACK → ACK → HTTP GET → 200 OK

### Observed SYN flood pattern

SYN
SYN
SYN
SYN
SYN
...

The repeated SYN requests without normal connection completion were a key indicator of the attack.

## Impact

Observed evidence included:

- repeated SYN packets from the attacker
- RST, ACK packets
- 504 Gateway Time-out responses
- failed connections from legitimate users

The traffic indicated that legitimate users were affected while the attack traffic continued.

## Key Finding

The observed SYN flood originated from a single source IP in the simulated scenario, so it was classified as a direct DoS rather than a distributed DDoS event.

## Investigation Workflow

1. Examine TCP connection attempts.
2. Identify abnormal SYN traffic.
3. Compare suspicious traffic with legitimate connections.
4. Analyze TCP flags and server responses.
5. Determine the attack type.
6. Document impact and supporting evidence.

## Tools

- Wireshark
- TCP/HTTP traffic analysis
- TCP three-way handshake analysis

## Evidence

- Wireshark TCP_HTTP log - TCP log.pdf
- Cybersecurity incident report.pdf

This project was completed as part of the Google Cybersecurity Certificate coursework.
