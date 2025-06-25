<!-- KaTeX -->
<script
  type="text/javascript"
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({ tex2jax: { inlineMath: [['$', '$']] }, messageStyle: 'none' });
</script>

# ARP and RARP

A **logical address** is an internetwork address. Its jurisdiction is universal.
A logical address is unique universally.

A **physical address** is a logical address. Its jurisdiction is a logical
network. It should be unique locally, but not necessarily universally.

Each time a host resolves a logical address, it can use a protocol to find the
physical address.

The Address Resolution Protocol (ARP) maps a logical address to a physical
address.

### ARP operation

The sender asks the receiver to announce its physical address when needed.
**ARP** is designed for this purpose.

Anytime a host or a router needs to find the physical address if another host or
router, it sends an **ARP request packet.** This packet is broadcasted over the
network. Every host or router in the network receives and processes the ARP
request packet, but only the intended recipient recognizes its IP address and
sends back an ARP response packet.

### ARP packet format

- **Hardware type:** This is a 16-bit field defining the type of the network in
  which ARP is running. Ethernet is given the type 1.
- **Protocol type:** This is a 16-bit field defining the protocol. The value of
  this field for the IPv4 protocol is $0800_{16}$.
- **Hardware length:** This is an 8-bit field defining the length of the
  physical address in bytes. For Ethernet, the value is 6.
- **Protocol length:** This is an 8-bit field defining the length of the logical
  address in bytes. For the IPv4 protocol, the value is 4.
- **Operation:** This is a 16-bit field defining the type of packet.
  - ARP request &mdash; 1
  - ARP response &mdash; 2
- **Sender hardware address:** This is a variable-length field defining the
  physical address of the sender. For Ethernet, this field is 6-bytes long.
- **Sender protocol address:** This is a variable-length field defining the
  logical address of the sender. For the IP protocol, this field is 4-bytes
  long.
- **Target hardware address:** This is a variable-length field defining the
  physical address of the target. For Ethernet, this field is 6-bytes long. For
  an ARP request packet, this field is all 0s because the sender does not know
  the physical address of the target.
- **Target protocol address:** A variable-length field defining the logical
  address of the target. For the IPv4 protocol, this field is 4-bytes long.

### ARP process

1.  The sender know the IP address of the target.
1.  IP asks ARP to create an ARP request packet.
1.  This packet is encapsulated in a frame using the physical broadcast address
    as the desination address.
1.  All devices except the one targeted drop the packet.
1.  The target device replies with an ARP reply packet that contains its
    physical address. This packet is unicast.
1.  The sender receives the reply packet.
1.  The IP datagram is now encapsulated in a frame and is unicast to the target
    device.

## ARP components

The ARP package has the following components:

- Cache table
- Queues
- Output module
- Input module
- Cache-control module

It is inefficient to use the ARP protocol for each datagram destined for the
same host or router. When a host or router receives the corresponding physical
address for an IP datagram, the address can be saved in the **cache table.**
This address can be used for the datagrams destined for the same receiver within
the next few minutes.

Each entry in the **cache table** contains the following fields:

- State
  - **Free:** Means that the time-to-live for this entry has expired. This space
    can be used for a new entry.
  - **Pending:** Means a request for this entry has been sent, but the reply has
    not been received yet.
  - **Resolved:** Means that the entry is complete.
- **Queue Number:** ARP uses numbered queues to enqueue the packets waiting for
  address resolution. Packets for the same target address are enqueued in the
  same queue.
- **Attempts:** This field shows the number of times an ARP request is sent out
  for this entry.
- **Time-out:** This field shows the lifetime of an entry in seconds.
- **Protocol address:** This field shows the target IP address.
- **Hardware address:** This field shows the target hardware address. It remains
  empty until resolved by an ARP reply.

### Output module

1.  Sleep until an IP packet is received from IP software.
1.  Check the cache table for an entry corresponding to the next hop of this IP
    packet.
1.  If found:
    1.  If the state is **Resolved:**
        - Extract the value of the hardware address from this entry.
        - Send the packet and the hardware address to the data link layer.
    1.  If the state is **Pending:**
        - Enqueue the packet in the corresponding queue.
1.  If not found:
    1.  Create a cache entry with the state set to **Pending** and **Attempts**
        set to 1.
    1.  Create a queue.
    1.  Enqueue the packet.
    1.  Send an ARP request.

### Input module

1.  Sleep until an ARP packet (request or reply) arrives. Check the cache table
    to find an entry corresponding to this ARP packet.
1.  If found:
    1.  Update the entry.
    1.  If the state was **Pending:**
        - Dequeue a packet.
        - Send the packet and the hardware address to the data link layer.
1.  If not found:
    1.  Create an entry.
    1.  Add the entry to the table.
1.  If the packet is a request:
    - Send an ARP reply (or ignore the request).

### Cache-control module

1.  Sleep until the periodic timer expires.
1.  For every entry in the cache table:
    1.  If the state is **Free,** continue.
    1.  If the state is **Pending:**
        1.  Increase the value of **Attempts** by 1.
        1.  If **Attempts** is greater than max:
            - Change the state to **Free.**
            - Destroy the corresponding queue.
        1.  Else:
            - Send an ARP request.
    1.  If the state is **Resolved:**
        1.  Decrease the value of the timeout by the value of elapsed time.
        1.  If the timeout is less or equal to zero:
            - Change the state to **Free.**
            - Destroy the corresponding queue.
