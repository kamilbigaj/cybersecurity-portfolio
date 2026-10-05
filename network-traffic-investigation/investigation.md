# Network Traffic Investigation

## Investigation Scope

The purpose of this investigation was to identify basic network communication patterns in a PCAP file, including DNS resolution, TCP connection establishment, and TLS/HTTPS traffic.

## Findings

### Client

`10.10.57.178`

### Server

`34.117.237.239`

### Protocol

`TCP / TLS`

### Ports

* Source port: `46742`
* Destination port: `443`

## DNS Analysis

* Client: `10.10.57.178`
* DNS Server: `10.0.0.2`
* Domain: `contile.services.mozilla.com`
* Resolved IP: `34.117.237.239`

The DNS request resolved `contile.services.mozilla.com` to `34.117.237.239`.

## TCP Three-Way Handshake

The TCP connection was established using the standard three-way handshake:

1. SYN — packet `16873`
2. SYN/ACK — packet `16874`
3. ACK — packet `16875`

The first SYN was sent by `10.10.57.178`, identifying it as the client initiating the connection.

## TLS / HTTPS Analysis

The client then communicated with `34.117.237.239` using TCP destination port `443`.

Wireshark identified TLS traffic, indicating an HTTPS connection.

Because the application data was protected by TLS, the contents of the HTTP communication were not directly visible as plaintext in the packet capture.

## Investigation Flow

The observed communication can be summarised as:

```text
contile.services.mozilla.com
        ↓
DNS query
        ↓
34.117.237.239
        ↓
TCP SYN
        ↓
TCP SYN/ACK
        ↓
TCP ACK
        ↓
TCP 46742 → 443
        ↓
TLS / HTTPS
```

## Conclusion

The client `10.10.57.178` first queried the DNS server `10.0.0.2` to resolve `contile.services.mozilla.com`.

The DNS response provided the IP address `34.117.237.239`, after which the client initiated a TCP connection to that address on destination port `443`.

The connection completed the TCP three-way handshake, followed by TLS-protected communication. The observed traffic is therefore consistent with an HTTPS connection between the identified client and server.

## Key Takeaways

* DNS resolution can be correlated with subsequent network connections.
* The first SYN identifies the host initiating a TCP connection.
* Source and destination ports help identify the client side and target service.
* TCP port `443` is commonly used for HTTPS, but protocol identification should be supported by packet analysis rather than the port number alone.
* TLS protects application data, making the contents of HTTPS traffic significantly harder to inspect than plaintext HTTP.
