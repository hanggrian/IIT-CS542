<!-- KaTeX -->
<script
  type="text/javascript"
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {inlineMath: [['$', '$']]},
    messageStyle: 'none',
  });
</script>

<style>ol { list-style-type: lower-alpha; }</style>

# [Homework 2](https://github.com/hanggrian/IIT-CS542/blob/assets/assignments/hw2.pdf)

## Problem 1

> What is the difference between an ARP request and an ARP reply in terms of the
  number of destinations?

According to the ARP process, an ARP request is a broadcast message while an
ARP reply is a unicast message. Therefore, the number of destinations are:

- **ARP request: $\mathbf{N}$,** all devices in the network.
- **ARP reply: $\mathbf{1}$,** only the target device.

## Problem 2

> Give all fields of a UDP header and their sizes.

Datagrams in UDP packets reserve $8 \ \textsf{bytes}$ for the header.

$$
\underbrace{\boxed{1 \dots 8}}_{\textsf{Header}} \ \boxed{9 \dots N}
$$

The fields in a datagram header are:

- **Source port: $\mathbf{2} \ \textsf{bytes}$.** The port number of the packet
  sender.
- **Destination port: $\mathbf{2} \ \textsf{bytes}$.** The receiver's port
  number.
- **Length: $\mathbf{2} \ \textsf{bytes}$.** The value of $N$, the total length
  of the UDP packet, including this header.
- **Checksum: $\mathbf{2} \ \textsf{bytes}$.** Used to verify the integrity of
  the datagram.

## Problem 3

> An IP datagram arrives with $\textsf{HLEN} = \texttt{C}$ (hex) and
  $\textsf{Total length} = \texttt{0038}$ (hex).
>
> 1.  Are there any options?
> 1.  How many bytes of data does this packet carry?

In IPv4, the header length is 4 bytes for each unit in the HLEN field.

$$
\begin{align}
  \textsf{HLEN} &=
    \overbrace{\texttt{1100}}^\texttt{C} \\\\
  &= 2^3 + 2^2 \\\\
  &= 8 + 4 &= \mathbf{12} \\\\
  \textsf{Header length} &=
    \textsf{HLEN} \times 4 \ \textsf{bytes} \\\\
  &= 12 \times 4 \ \textsf{bytes} &= \mathbf{48} \ \textbf{bytes} \\\\
  \textsf{Options length} &= \textsf{HLEN} - \textsf{Min. header length} \\\\
  &= 48 \ \textsf{bytes} - 20 \ \textsf{bytes} &= \mathbf{28} \ \textbf{bytes}
\end{align}
$$

For the total length, the converted decimal value represent the final bytes.

$$
\begin{align}
  \textsf{Total length} &=
    \overbrace{\texttt{0011}}^\texttt{3} \
    \overbrace{\texttt{1000}}^\texttt{8} \
    \textsf{bytes} \\\\
  &= (2^5 + 2^4 + 2^3) \ \textsf{bytes} \\\\
  &= (32 + 16 + 8) \ \textsf{bytes} &= \mathbf{56} \ \textbf{bytes} \\\\
  \textsf{Data length} &= \textsf{Total length} - \textsf{Header length} \\\\
  &= 56 \ \textsf{bytes} - 48 \ \textsf{bytes} &= \mathbf{8} \ \textbf{bytes}
\end{align}
$$

The length of options and data are:

1.  **Options: $\mathbf{28} \ \textbf{bytes}$.** Assuming that the header has a
    fixed minimum length of $20 \ \textsf{bytes}$.
1.  **Data: $\mathbf{8} \ \textbf{bytes}$.** The remaining bytes after the
    header.

## Problem 4

> Compare TCP and UDP in terms of reliability.

TCP is a connection-oriented protocol, it establishes a connection between the
sender and receiver before transmitting packets. Compared to a connectionless
protocol like UDP, which sends packets into datagrams, TCP is more reliable
because it guarantees the delivery of data packets. Moreover, packets are
streamed in order and without duplication in a TCP connection.

## Problem 5

> A host with the IP address $\texttt{173.16.5.9}$ and the physical address
  $\texttt{C1:D4:56:78:9A:BC}$ sends data to the destination with the IP address
  $\texttt{193.168.1.11}$ and the physical address $\texttt{BB:13:56:CA:9A:D2}$.
  The next hop has the IP address $\texttt{173.16.5.1}$ and the physical address
  $\texttt{00:1C:42:AA:BB:CC}$. Show all the fields of the ARP request and reply
  packets. The Ethernet protocol is implemented at the data link layer.

ARP resolves the hardware and protocol addresses in the local network. Because
the addresses of both host and next hop start with $\texttt{173.16}$, they
belong to the same network.

$$
\textsf{Host} \to
  \textsf{Hop} \to
  \textsf{Destination} \\\\
{\texttt{173.16.5.9} \brack \texttt{C1:D4:56:78:9A:BC}} \to
  {\texttt{173.16.5.1} \brack \texttt{00:1C:42:AA:BB:CC}} \to
  {\texttt{193.168.1.11} \brack \texttt{BB:13:56:CA:9A:D2}}
$$

The fields for the ARP request and reply packets are as follows:

Field | Request packet | Reply packet
--- | --- | ---
Hardware type | $\texttt{0x0001}$ (Ethernet) | $\texttt{0x0001}$ (Ethernet)
Protocol type | $\texttt{0x0800}$ (IPv4) | $\texttt{0x0800}$ (IPv4)
Hardware length | $\texttt{0x06}$ (6 bytes) | $\texttt{0x06}$ (6 bytes)
Protocol length | $\texttt{0x04}$ (4 bytes) | $\texttt{0x04}$ (4 bytes)
Operation | $\texttt{0x0001}$ (request) | $\texttt{0x0002}$ (reply)
Sender hardware address | $\texttt{C1:D4:56:78:9A:BC}$ (host) | $\texttt{00:1C:42:AA:BB:CC}$ (next hop)
Sender protocol address | $\texttt{173.16.5.9}$ (host) | $\texttt{173.16.5.1}$ (next hop)
Target hardware address | $\texttt{00:00:00:00:00:00}$ (ignored) | $\texttt{C1:D4:56:78:9A:BC}$ (host)
Target protocol address | $\texttt{173.16.5.1}$ (next hop) | $\texttt{173.16.5.9}$ (host)

## Problem 6

> An IP packet starts with the following hex digits:
  $\texttt{45000064 1C4620F0}$. It’s the 2nd fragment.
>
> 1.  How many bytes of data does it carry?
> 1.  Is there the next fragment?
> 1.  If yes, what is its offset?

The order of the hex digits defines the fields in the IP header.

$$
\overbrace{\textsf{Version}}^\texttt{4} \
  \overbrace{\textsf{HLEN}}^\texttt{5} \
  \overbrace{\textsf{TOS}}^\texttt{00} \
  \overbrace{\textsf{Total length}}^\texttt{00 64} \
  \overbrace{\textsf{Identification}}^\texttt{1C 46} \
  \overbrace{\textsf{Flags and fragmentation}}^\texttt{20 F0}
$$

The first byte can determine the header length, while the total length is the
last two bytes of the first four bytes.

$$
\begin{align}
  \textsf{Header length} &= \textsf{HLEN} \times \textsf{Version} \\\\
  &= \overbrace{\texttt{0101}}^\texttt{5} \times 4 \ \textsf{bytes} \\\\
  &= (2^2 + 2^0) \times 4 \ \textsf{bytes} \\\\
  &= (4 + 1) \times 4 \ \textsf{bytes} \\\\
  &= 5 \times 4 \ \textsf{bytes} &= \mathbf{20} \ \textbf{bytes} \\\\
  \textsf{Total length} &=
    \overbrace{\texttt{0110}}^\texttt{6} \
    \overbrace{\texttt{0100}}^\texttt{4} \
    \textsf{bytes} \\\\
  &= (2^6 + 2^5 + 2^2) \ \textsf{bytes} \\\\
  &= (64 + 32 + 4) \ \textsf{bytes} &= \mathbf{100} \ \textbf{bytes} \\\\
  \textsf{Data length} &= \textsf{Total length} - \textsf{Header length} \\\\
  &= 100 \ \textsf{bytes} - 20 \ \textsf{bytes} &= \mathbf{80} \ \textbf{bytes}
\end{align}
$$

To find out if there is a next fragment, we need to check the flags and
fragmentation fields.

$$
\begin{align}
  \textsf{Flags and fragmentation} &=
    \overbrace{\texttt{0010}}^\texttt{2} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{1111}}^\texttt{F} \
    \overbrace{\texttt{0000}}^\texttt{0} \\\\
  &=
    \overbrace{\textsf{MF}}^\texttt{001} \
    \overbrace{\textsf{Fragment offset}}^\texttt{0 0000 1111 0000} \\\\
  \textsf{Fragment offset} &=
    \texttt{0 0000 1111 0000} \times 8 \ \textsf{bytes} \\\\
  &= (2^7 + 2^6 + 2^5 + 2^4) \times 8 \ \textsf{bytes} \\\\
  &= (128 + 64 + 32 + 16) \times 8 \ \textsf{bytes} &=
    \mathbf{1,920} \ \textbf{bytes}
\end{align}
$$

The offset to the next fragment is the current fragment offset combined with
data length.

$$
\begin{align}
  \textsf{Next fragment offset} &=
    \textsf{Fragment offset} + \textsf{Data length} \\\\
  &= 1,920 \ \textsf{bytes} + 80 \ \textsf{bytes} &=
    \mathbf{2,000} \ \textbf{bytes}
\end{align}
$$

The answer to each question is:

1.  **Data length: $\mathbf{80} \ \textbf{bytes}$.** The total length subtracted
    by the header length.
1.  **Next fragment: MF.** The first three bits of the flags and fragmentation
    indicates that there is a next fragment.
1.  **Next fragment offset: $\mathbf{2,000} \ \textbf{bytes}$.** The fragment
    offset plus data carried by the current fragment.

## Problem 7

> An IP datagram with no options whose total length is $5,000 \ \textsf{bytes}$
  needs to be fragmented. $\textsf{MTU} = 1,500 \ \textsf{bytes}$. All but the
  last fragment are max-sized.
>
> 1.  How many fragments are there?
> 1.  How many bytes of data does each fragment carry?
> 1.  What is the offset of the 3rd fragment?
> 1.  What is the total size of the last fragment?

Determine the data length of fragment and datagram, then check how many
fragments can fit into the datagram.

$$
\begin{align}
  \textsf{Fragment data length} &= \textsf{MTU} - \textsf{Header length} \\\\
  &= 1,500 \ \textsf{bytes} - 20 \ \textsf{bytes} &=
    \mathbf{1,480} \ \textbf{bytes} \\\\
  \textsf{Datagram data length} &=
    \textsf{Datagram total length} - \textsf{Header length} \\\\
  &= 5,000 \ \textsf{bytes} - 20 \ \textsf{bytes} &=
    \mathbf{4,980} \ \textbf{bytes} \\\\
  \textsf{Datagram fragments} &=
    \left\lceil
    \frac{\textsf{Datagram data length}}{\textsf{Fragment data length}}
    \right\rceil \\\\
  &=
    \left\lceil
    \frac{4,980 \ \textsf{bytes}}{1,480 \ \textsf{bytes}}
    \right\rceil &=
    \mathbf{4} \ \textbf{fragments}
\end{align}
$$

Because the fragments cannot be proportionally distributed, the last fragment
is smaller than the rest.

$$
\begin{align}
  \textsf{Fragment \#4 data length} &=
    \textsf{Datagram data length} \mod \textsf{Fragment data length} \\\\
  &= 4,980 \ \textsf{bytes} \mod 1,480 &= \mathbf{540} \ \textbf{bytes}
\end{align}
$$

$$
\boxed{1,980 \ \textsf{bytes}} \
\dots \
\boxed{540 \ \textsf{bytes}}
$$

To calculate the offset of the 3rd fragment, we can use the formula:

$$
\begin{align}
  \textsf{Fragment \#3 offset} &=
    \frac{(\textsf{Current \#} - 1) \times \textsf{Fragment data length}}
      {8 \ \textsf{bytes}} \\\\
  &= \frac{(3 - 1) \times 1,480 \ \textsf{bytes}}{8 \ \textsf{bytes}} \\\\
  &= \frac{2 \times 1,480 \ \textsf{bytes}}{8 \ \textsf{bytes}}
    &= \mathbf{370} \ \textbf{bytes}
\end{align}
$$

The data length is combined with the header length to get the total size of
the last fragment.

$$
\begin{align}
  \textsf{Fragment \#4 total length} &=
    \textsf{Fragment \#4 data length} + \textsf{Header length} \\\\
  &= 540 \ \textsf{bytes} + 20 \ \textsf{bytes} &= \mathbf{560} \ \textbf{bytes}
\end{align}
$$

1.  **Datagram fragments: $\mathbf{4} \ \textbf{fragments}$.** A rounded up
    value of datagram data length divided by fragment data length.
1.  **Fragment data length: $\mathbf{1,480} \ \textbf{bytes}$ (3 fragments) and
    $\mathbf{540} \ \textbf{bytes}$ (4th fragment).** This means that there are
    three full-sized fragments.
1.  **3rd fragment offset: $\mathbf{370} \ \textbf{bytes}$.** Data length of all
    previous fragments measured in 8-byte units.
1.  **Last fragment total length: $\mathbf{560} \ \textbf{bytes}$.** The
    remaining payload with the header length included.

## Problem 8

> Consider a TCP client with $\textsf{rwnd} = 3,000$, $\textsf{cwnd} = 3,500$,
  and last received $\textsf{ACK} = 1,000$.
>
> 1.  Draw and explain the sliding window diagram.
> 1.  What data can be sent now?

The sliding window diagram can be visualized as follows:

![Figure 1](https://github.com/hanggrian/IIT-CS542/raw/assets/assignments/hw2_1.svg)

There are $4,000 \ \textsf{bytes}$ of data spanning from acknowledged portion
to the sendable window. Because the range is inclusive, the last byte is not
counted in the sent data.

$$
\begin{align}
  \textsf{Sent data} &=
    \textsf{ACK} + \min(\textsf{rwnd}, \textsf{cwnd}) - 1 \\\\
  &= 1,000 \ \textsf{bytes} +
    \min(3,000 \ \textsf{bytes}, 3,500 \ \textsf{bytes})
    - 1 \ \textsf{byte} \\\\
  &= 1,000 \ \textsf{bytes} + 3,000 \ \textsf{bytes} - 1 \ \textsf{byte}
    &= \mathbf{3,999} \ \textbf{bytes}
\end{align}
$$

## Problem 9

> An IP packet arrives with $\textsf{HLEN} = \texttt{1110}$ (binary). Is this
  a valid IP packet?

Convert the binary notation to decimal value to determine the header length.

$$
\begin{align}
  \textsf{HLEN} &= \texttt{1110} \\\\
  &= 2^3 + 2^2 + 2^1 \\\\
  &= 8 + 4 + 2 &= \mathbf{14} \\\\
  \textsf{Header length} &= \textsf{HLEN} \times \textsf{Version} \\\\
  &= 14 \times 4 \ \textsf{bytes} &= \mathbf{56} \ \textbf{bytes}
\end{align}
$$

The IP packet header length falls within the range of
$20 \to 60 \ \textsf{bytes}$. Therefore, it is a valid IP packet.

## Problem 10

> A UDP datagram with the destination port $61,284$ has arrived. The
  control-block table shows that this port is IN-USE but no queue has been
  assigned to it. Is it possible?

Yes, it is possible that a port is in use but has no assigned queue. When a port
is opened and registered in the control-block table, it means that an
application is actively listening, but no data has arrived yet.

## Problem 11

> Consider an ARP packet with $\textsf{OPERATION} = 1$ and a the target hardware
  address field filled with a valid address. Is it possible? Explain your
  answer.

No, a valid address does not belong in the target hardware address in this
scenario. When the operation field is set to $1$, it indicates that the packet
type is an ARP request. In most cases, the target hardware address is set to
$\texttt{00:00:00:00:00:00}$ because the sender does not know the target
hardware address at that point.

## Problem 12

> The last TCP acknowledgment that a client successfully sent to a server is
  $12,623$. The server sends $1,000 \ \textsf{bytes}$ of data in each segment.
  At subsequent moments $t_1 < t_2 < t_3$ the client received from the server
  TCP segments with the following sequence numbers:
>
> - $t_1: 13,623$
> - $t_2: 14,623$
> - $t_3: 12,623$
>
> The 3rd segment was delayed. What acknowledgment did the client send after
  receiving each of these three segments?

The segment data length is compared to the expected sequence number at each
turn. If the current turn is greater than the expected, the client sends a
duplicate acknowledgment while keeping track of the missing segments.

$$
\begin{align}
  \textsf{Missing segments} &= 0 &&& t_1 > 12,633 &&
    \textsf{out of order} \\\\
  &&& \textsf{ACK}_1 &= \mathbf{12,633} \\\\
  &= 1,000 &&& t_2 > 12,633 &&
    \textsf{out of order} \\\\
  &&& \textsf{ACK}_2 &= \mathbf{12,633} \\\\
  &= 2,000 &&& t_3 = 12,633 &&
    \textsf{expected} \\\\
  &&& \textsf{ACK}_3 &= t_3 + \textsf{Missing segments} +
    \textsf{Data length} \\\\
  &&& &= 12,633 + 2,000 + 1,000 = \mathbf{15,633}
\end{align}
$$

Therefore, the acknowledgment numbers sent by the client are:

1.  **After $t_1$: $\mathbf{12,633}$.**
1.  **After $t_2$: $\mathbf{12,633}$.**
1.  **After $t_3$: $\mathbf{15,633}$.**

## Problem 13

> Here is a TCP header in the hex format:
>
> $$
> \texttt{0532 0035 0000 0050 0000 00A1 5002 2000 0270 0000}
> $$
>
> 1.  What is the source port and the destination port?
> 1.  What is the sequence number?
> 1.  What does the acknowledgment number mean?
> 1.  What is the header length in bytes?
> 1.  Which TCP flags are set, and what do they indicate?
> 1.  What is the window size?

Given the TCP header:

$$
\overbrace{\textsf{Source port}}^\texttt{0532} \
  \overbrace{\textsf{Destination port}}^\texttt{0035} \
  \overbrace{\textsf{Sequence number}}^\texttt{0000 0050} \
  \overbrace{\textsf{ACK}}^\texttt{0000 00A1} \\\\\
\overbrace{\textsf{HLEN and flags}}^\texttt{5002} \
  \overbrace{\textsf{Window size}}^\texttt{2000} \
  \overbrace{\textsf{Checksum}}^\texttt{0270} \
  \overbrace{\textsf{Urgent pointer}}^\texttt{0000}
$$

Convert the hexadecimal notation to decimal values.

$$
\begin{align}
  \textsf{Source port} &= \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0101}}^\texttt{5} \
    \overbrace{\texttt{0011}}^\texttt{3} \
    \overbrace{\texttt{0010}}^\texttt{2} \\\\
  &= 2^{10} + 2^8 + 2^5 + 2^4 + 2^1 \\\\
  &= 1024 + 256 + 32 + 16 + 2 &= \mathbf{1,330} \\\\
  \textsf{Destination port} &= \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0011}}^\texttt{3} \
    \overbrace{\texttt{0101}}^\texttt{5} \\\\
  &= 2^5 + 2^4 + 2^2 + 2^0 \\\\
  &= 32 + 16 + 4 + 1 &= \mathbf{53} \\\\
  \textsf{Sequence number} &= \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0101}}^\texttt{5} \
    \overbrace{\texttt{0000}}^\texttt{0} \\\\
  &= 2^6 + 2^4 \\\\
  &= 64 + 16 &= \mathbf{80} \\\\
  \textsf{ACK} &= \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{1010}}^\texttt{A} \
    \overbrace{\texttt{0001}}^\texttt{1} \\\\
  &= 2^7 + 2^5 + 2^0 \\\\
  &= 128 + 32 + 1 &= \mathbf{161} \\\\
  \textsf{HLEN} &= \overbrace{\texttt{0101}}^\texttt{5} \\\\
  &= 2^2 + 2^0 \\\\
  &= 4 + 1 &= \mathbf{5} \\\\
  \textsf{Flags} &= \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0010}}^\texttt{2} \\\\
  &= 2^1 \\\\
  &= 2 &= \mathbf{2} \\\\
  \textsf{Window size} &= \overbrace{\texttt{0010}}^\texttt{2} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \\\\
  &= 2^{13} &= \mathbf{8,192} \\\\
  \textsf{Checksum} &= \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0010}}^\texttt{2} \
    \overbrace{\texttt{0111}}^\texttt{7} \
    \overbrace{\texttt{0000}}^\texttt{0} \\\\
  &= 2^9 + 2^6 + 2^5 + 2^4 \\\\
  &= 512 + 64 + 32 + 16 &= \mathbf{624} \\\\
  \textsf{Urgent pointer} &= \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} \
    \overbrace{\texttt{0000}}^\texttt{0} &= \mathbf{0}
\end{align}
$$

Using the formula above, we can determine the header length in bytes.

$$
\begin{align}
  \textsf{Header length} &= \textsf{HLEN} \times \textsf{Version} \\\\
  &= 5 \times 4 \ \textsf{bytes} &= \mathbf{20} \ \textbf{bytes}
\end{align}
$$

The flags for TCP are:

Binary | Decimal | Flag
--- | --- | ---
$\texttt{0000 0001}$ | $1$ | FIN
$\texttt{0000 0010}$ | $2$ | SYN
$\texttt{0000 0100}$ | $4$ | RST
$\texttt{0000 1000}$ | $8$ | PSH
$\texttt{0001 0000}$ | $16$ | ACK
$\texttt{0010 0000}$ | $32$ | URG
$\texttt{0100 0000}$ | $64$ | ECE
$\texttt{1000 0000}$ | $128$ | CWR

Therefore, the answers are:

1.  Ports
    - **Source port: $\mathbf{1,330}$.**
    - **Destination port: $\mathbf{53}$.**
1.  **Sequence number: $\mathbf{80}$.**
1.  **Acknowledgment number: $\mathbf{161}$,** meaning that the sender
    has received all data up to $160$.
1.  **Header length: $\mathbf{20} \ \textbf{bytes}$.**
1.  **Flags: $\mathbf{2}$,** indicating that the SYN flag is set.
