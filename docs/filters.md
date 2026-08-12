# Wireshark Display Filters

## DNS

```text
dns && dns.qry.name == "example.com"
```

Isolates DNS packets containing a query for `example.com`.

## ICMP

```text
icmp && ip.addr == 1.1.1.1
```

Shows ICMP traffic in either direction involving `1.1.1.1`.

## TCP stream

```text
tcp.stream == 6
```

Shows every packet Wireshark assigned to the controlled TCP conversation.
Stream indexes are capture-local values and can differ in another capture.

```text
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

Shows initial SYN packets while excluding SYN-ACK packets.

## TLS handshake

```text
tcp.stream == 6 && tls.handshake.type == 1
```

Shows the TLS Client Hello in the controlled TCP stream.

```text
tcp.stream == 6 && tls.handshake.type == 2
```

Shows the TLS Server Hello in the controlled TCP stream.

## TLS application data

```text
tcp.stream == 6 && tls.app_data
```

Shows encrypted TLS application records in the controlled stream.

## TCP termination

```text
tcp.stream == 6 && (tcp.flags.fin == 1 || tcp.flags.reset == 1)
```

Shows FIN or RST packets used to close or abruptly terminate the connection.

