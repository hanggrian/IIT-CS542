<!-- Mermaid -->
<script
  type="text/javascript"
  src="https://cdn.jsdelivr.net/npm/mermaid@10.4.0/dist/mermaid.min.js">
</script>

# Network layers

Each layer uses the services of the layer below it.

The internet model sometimes called the TCP/IP protocol suite is composed of 5
ordered layers: physical (layer 1), data link (layer 2), network (layer 3),
transport (layer 4), and application (layer 5).

In developing the model, the designers distilled the process of transmitting
data to its most fundamental elements, identified the networking functions and
collected those functions into discrete groups that became the **layers.** Each
layer defines a family of functions distinct from those of the other layers.

Within each device, each layer calls upon services of the layer below it. Layer
3, for example, uses the services provided by layer 2 and provides services to
layer 4.

Layer $X$ on one device communicates with layer $X$ on another device. This
communication is governed by protocols.

As long as a layer provides the expected services to the layer above it, the
specific implementation of its functions can be modified or replaced without
requiring changes to the surrounding layers.

At each layer, a header can be added to the data unit. At layer 2, a trailer is
added as well.

### Physical layer duties

- Physical characteristics of interfaces and media
- Representation of bits
- Data rate
- Synchronization of bits
- Line configuration defines the connection of devices to the media.
  - Point-to-point configuration: Two devices are connected through a dedicated
    link.
  - Multipoint configuration: A link is shared between several devices.
- Physical topology defines how devices are connected to make a network.
  - Mesh topology
  - Star topology
  - Ring topology
  - Bus topology
- Transmission mode defines the direction of transmission between two devices.
  - Simplex mode
    ```mermaid
    flowchart LR
      A --> B
    ```
  - Half-duplex mode
    ```mermaid
    flowchart LR
      A --> B
      B --> A
    ```
  - Full-duplex mode
    ```mermaid
    flowchart LR
      A <--> B
    ```

### Data link layer duties

- Framing: The data link layer divides the stream of bits into manageable data
  units called **frames.**
- Physical addressing: The data link layer adds a header to the frame to define
  the sender and receiver of the frame.
- Flow control: If the data rate absorbed by the receiver is less than the rate
  produced by the sender, the data link layer imposes a flow control mechanism
  to prevent overwhelming the receiver.
- Error control: The data link layer adds mechanisms to detect and retransmit
  damaged or lost frames and to prevent duplication of frames. Error control is
  achieved through a trailer added to the end of the frame.
- Access control: When many devices are connected to the same link, the data
  link layer protocols are necessary to determine which device has control over
  the link at any given time.

### Network layer duties

- Logical addressing: The network layer adds a header to the data unit coming
  from the upper layer that includes the logical addresses of the sender and
  receiver.
- Routing: When independent networks are connected to create an internetwork,
  the routers route the packets to their final destination. The network layer
  provides this mechanism.
- Internetworking
- Packetizing
- Fragmentation
- Address resolution

### Transport layer duties

- Port addressing: The transport layer header includes the port address. The
  network layer gets each packet to the correct device (computer, laptop,
  tablet), the transport layer gets the entire message to the correct process on
  that device.
- Segmentation and reassembly: A message is divided into transmitable segments,
  each segment containing a sequence number. These numbers enable the transport
  layer to reassemble the message upon arrival at the destination.
- Correction control: The transport layer can be either connectionless or
  connection-oriented. In a connectionless transport layer, each data unit is
  independently delivered to the transport layer at the destination device. A
  connection-oriented transport layer makes a connection with the transport
  layer at the destination device before delivering the segments. After all the
  data are transferred, the connection is terminated.
- Flow control: Flow control at this layer is performed end-to-end rather than
  across a single link.
- Error control

## OSI Model

The Open Systems Interconnection (OSI) model was designed by the international
organization for standardization. The OSI model is a theoretical model designed
to show how a protocol stack should be implemented.

- Session layer: Establishes sessions between communicating applications on the
  communicating devices (computers).
- Presentation layer: Translates data to a standard format, manages encryption
  and data compression.

The **network layer** in the internet model is responsible for host-to-host
delivery, for carrying packets through the internet, through several physical
networks.

The network layer receives services from the data link layer and provides
services to the transport layer.

- Internetworking: The logical gluing of heterogeneous physical networks
  together to make them look like a single network.
- Addressing: The addresses used by the network layer must uniquely and
  universally define the connection of a host (computer) or router to the
  internet.
- Routing: Each IP packet can reach its destination via several routes. The
  routers connecting local networks make the routing decisions.
- Packetizing: The network layer encapsulates data units received from upper
  layer protocols and makes packet of them.
- Fragmentation: Each router decapsulates the IP packet from the received frame,
  processes it and then encapsulates it in another frame. If the packet is too
  large, it is fragmented.
- Address resolution: The network layer provides host-to-host addressing. The
  data link layer needs physical addresses for node-to-node delivery. These
  addresses are mapped to each other.

The **network layer at the source** is responsible for creating a packet that
carries two universal addresses: a source address and a destination address. If
the packet is too large, it is fragmented.

The **network layer at the router** is responsible for routing the packet. The
router finds the interface from which the packet must be sent. In addition, the
packet may go through another fragmentation, if necessary.

The **network layer at the destination** makes sure that the destination address
of the packet is the same as the address of the host. Then, the packet is
reassembled and data are delivered to the transport layer.
