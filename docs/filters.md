# Wireshark Display Filters

These are the display filters I used while working through the capture.
They helped me focus on one protocol or connection at a time. A display filter
changes which packets Wireshark shows; it does not remove packets from the
capture.

## DNS

```text
dns && dns.qry.name == "example.com"
```

I used this filter to find the DNS query and response for `example.com`.

## ICMP

```text
icmp && ip.addr == 1.1.1.1
```

This showed the ping requests to `1.1.1.1` and the replies coming back.

## TCP Stream

```text
tcp.stream == 6
```

This let me follow the HTTPS connection without the other traffic in the
capture. My connection was stream 6; the number can be different in another
capture.

```text
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

I used this to find the SYN packets that start TCP connections. The ACK check
keeps SYN-ACK replies out of the results.

## TLS Handshake

```text
tcp.stream == 6 && tls.handshake.type == 1
```

This showed the Client Hello for the connection I was studying.

```text
tcp.stream == 6 && tls.handshake.type == 2
```

Changing the handshake type to `2` showed the Server Hello.

## TLS Application Data

```text
tcp.stream == 6 && tls.app_data
```

I used this filter to find TLS Application Data in the same connection.

## Connection Closure

```text
tcp.stream == 6 && (tcp.flags.fin == 1 || tcp.flags.reset == 1)
```

This helped me check how the connection ended. FIN packets are part of a
normal shutdown, while RST packets indicate a reset. The filter does not show
packets that contain only an ACK. To follow the complete closing exchange,
I need to look at the full stream as well.
