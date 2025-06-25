<!-- KaTeX -->
<script
  type="text/javascript"
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({ tex2jax: { inlineMath: [['$', '$']] }, messageStyle: 'none' });
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
\underbrace{1 \dots 8}_{\textsf{Header}} \quad 9 \dots N
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

> An IP datagram arrives with $HLEN = C \ (\textsf{hex})$ and
  $\textsf{Total length} = \texttt{0038} \ (\textsf{hex})$.
>
> 1.  Are there any options?
> 1.  How many bytes of data does this packet carry?

## Problem 4

> Compare TCP and UDP in terms of reliability.

## Problem 5

> A host with the IP address $\texttt{173.16.5.9}$ and the physical address
  $\texttt{C1:D4:56:78:9A:BC}$ sends data to the destination with the IP address
  $\texttt{193.168.1.11}$ and the physical address $\texttt{BB:13:56:CA:9A:D2}$.
  The next hop has the IP address $\texttt{173.16.5.1}$ and the physical address
  $\texttt{00:1C:42:AA:BB:CC}$. Show all the fields of the ARP request and reply
  packets. The Ethernet protocol is implemented at the data link layer.

## Problem 6

> An IP packet starts with the following hex digits:
  $\texttt{45000064 1C4620F0}$. It’s the 2nd fragment.
>
> 1.  How many bytes of data does it carry?
> 1.  Is there the next fragment?
> 1.  If yes, what is its offset?

## Problem 7

> An IP datagram with no options whose total length is $5,000 \ \textsf{bytes}$
  needs to be fragmented. $MTU = 1,500 \ \textsf{bytes}$. All but the last
  fragment are max-sized.
>
> 1.  How many fragments are there?
> 1.  How many bytes of data does each fragment carry?
> 1.  What is the offset of the 3rd fragment?
> 1.  What is the total size of the last fragment?

## Problem 8

> Consider a TCP client with $rwnd = 3,000$, $cwnd = 3,500$, and last received
  $ACK = 1,000$.
>
> 1.  Draw and explain the sliding window diagram.
> 1.  What data can be sent now?

## Problem 9

> An IP packet arrives with $HLEN = 1,110 \ (\textsf{binary})$. Is this a valid
  IP packet?

## Problem 10

> A UDP datagram with the destination port $61,284$ has arrived. The
  control-block table shows that this port is IN-USE but no queue has been
  assigned to it. Is it possible?

## Problem 11

> Consider an ARP packet with $OPERATION = 1$ and a the target hardware address
  field filled with a valid address. Is it possible? Explain your answer.

## Problem 12

> The last TCP acknowledgment that a client successfully sent to a server is
  $12,623$. The server sends $1,000 \ \textsf{bytes}$ of data in each segment.
  At subsequent moments $t_1 < t_2 < t_3$ the client received from the server
  TCP segments with the following sequence numbers:
>
> - $t_1: 13,623$
> - $t_2 :14,623$
> - $t_3 :12,623$
>
> The 3rd segment was delayed. What acknowledgment did the client send after
  receiving each of these three segments?

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
