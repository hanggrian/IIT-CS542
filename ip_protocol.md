<!-- KaTeX -->
<script
  type="text/javascript"
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({ tex2jax: { inlineMath: [['$', '$']] }, messageStyle: 'none' });
</script>

# IP protocol

IP is an unreliable and connectionless datagram protocol &mdash; the best effort
delivery service.

IP does its best to deliver the packets to the destination, but with no
guarantees.

An IP datagram is a variable-length packet consisting of two parts: header and
data. The header is $20 \dots 60 \ \textsf{bytes}$ in length and contains
information essential to routing and delivery.

### IP header format

- **Version:** This is a 4-bit field that defines the version of the IP
  protocol.
- **Header length:** This 4-bit field defines the total length of the datagram
  header in 4-byte words.
- **Service type:** The first $3 \ \textsf{bits}$ are called
  *precedence bits.* The next $4 \ \textsf{bits}$ are called *TOS bits,* and the
  last bit is not used.
  - **Precedence:** A 3-bit subfield ranging from
    $0 \ (\texttt{000} \ \textsf{in binary}) \dots 7 \ (\texttt{111} \ \textsf{in binary})$.
    The precedence defines the priority of the datagram in issues such as
    congestion.
  - **TOS:** A 4-bit subfield. We have 5 different types of services requested
    by application programs.
- **Total length:** This is a 16-bit field that defines the total length
  (header + data) of the IP datagram in bytes. The total length of the IP
  datagram is limited to $65,535 \ \textsf{bytes}$, of which
  $20 \dots 60 \ \textsf{bytes}$ are the header and the rest is data.
- Fragmentation-related:
  - Identification
  - Flags
  - Fragmentation offset
- **Time to live:** This field is used to control the maximum numbner of hops
  (routers) visited by the datagram. When a source host sends the datagram, it
  stores a number in this fields. Each router that processes the datagram
  decreases this number by 1. If this value is zero, the router discards the
  datagram. This field limits the lifetime of a datagram.
- **Protocol:** This 8-bit field defines the higher-level protocol that uses the
  services of IP.
- **Checksum:** Used for detection.
- Source IP address.
- Destination IP address.
- **Options:** This field can be used to request special treatment for the
  packet. It consists of a series of entries each corresponding to a requested
  option.
