# Analyst Findings

## Scope

This was a controlled analysis of normal traffic generated from a macOS
endpoint. The objective was to demonstrate protocol analysis, not to identify
malicious activity.

## DNS

Captured an A-record query generated with `dig example.com`, correlated it with
the matching response through transaction ID `0x9226`, and verified the queried
name, record type, and class.

## ICMP

Identified four Echo requests and four matching replies for `1.1.1.1`.
Identifiers and sequence numbers linked each request to its reply, confirming
ICMP reachability at the time of capture.

## TCP

Isolated the controlled HTTPS connection as TCP stream 6 and validated its
SYN, SYN-ACK, and ACK handshake. Verified independent sequence-number spaces
and corresponding acknowledgment behavior. Confirmed a graceful four-packet
FIN/ACK shutdown initiated by the client, with no reset observed.

## TLS

Identified SNI for `example.com`, client offers for TLS versions and ALPN
protocols, and the X25519 key share. Verified the server's selection of TLS 1.3
and `TLS_CHACHA20_POLY1305_SHA256`. Observed encrypted TLS Application Data in
both directions.

## Privacy

The raw capture is intentionally excluded. Evidence screenshots redact local
IP addresses, MAC addresses, and resolved device/vendor identifiers. Public
targets and protocol fields relevant to the analysis remain visible.

