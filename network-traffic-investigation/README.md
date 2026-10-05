# Network Traffic Investigation

## Objective

Analyse captured network traffic and identify communicating hosts, protocols, ports, DNS activity, and TCP connection establishment.

The goal of this project is to practise basic network traffic analysis using packet captures and Wireshark.

## Environment

* Linux VM
* Wireshark
* PCAP/PCAPNG network capture

## Tools

* Wireshark
* Linux networking tools

## Methodology

The investigation focuses on:

1. Identifying client and server hosts
2. Analysing source and destination ports
3. Identifying DNS requests and resolved IP addresses
4. Inspecting TCP three-way handshakes
5. Distinguishing HTTP from HTTPS/TLS traffic

## Key Findings

The analysed traffic contained:

* DNS resolution of a Mozilla-related domain
* A complete TCP three-way handshake
* TCP communication to destination port 443
* TLS/HTTPS traffic between the identified client and server

## Outcome

This project demonstrates the ability to use Wireshark to identify basic network communication patterns and correlate DNS resolution with subsequent TCP/TLS traffic.
