<!-- KaTeX -->
<script
  type="text/javascript"
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({ tex2jax: { inlineMath: [['$', '$']] }, messageStyle: 'none' });
</script>

<style>ol { list-style-type: lower-alpha; }</style>

# [Homework 1](https://github.com/hanggrian/IIT-CS542/blob/assets/assignments/hw1.pdf)

## Problem 1

> What is the range of addresses of the $65\textsf{th block}$ of Class A?

The first byte of a Class A address ranges from $0$ to $127$. Therefore, the
$65\textsf{th block}$ of Class A addresses starts from $\texttt{65.0.0.0}$ and
ends at $\texttt{65.255.255.255}$.

## Problem 2

> Consider fixed-length subnetting. What is the minimum number of created
  subnets if the desired number of subnets is:
>
> 1.  $6$
> 1.  $62$
> 1.  $122$
> 1.  $250$

## Problem 3

> If you subnet the network $\texttt{11.0.0.0}$ with a subnet mask of
  $\texttt{255.255.240.0}$, what is the maximum number of subnets and usable
  addresses per subnet? A usable address is an address that can be assigned to a
  host or a router. Assume classful addressing.

## Problem 4

> Convert the IP address $\texttt{0xDA0121C8}$ to the dotted decimal notation.
  What is the class of this IP address?

First, we convert the hexadecimal $\texttt{0xDA0121C8}$ to binary notation,
dividing it into 4 bytes. Then, we sum the calculated decimal values of each
byte to get the dotted decimal notation.

$$
\overbrace{\texttt{1101}}^\textsf{D}\overbrace{\texttt{1010}}^\textsf{A} \ . \
\overbrace{\texttt{0000}}^\textsf{0}\overbrace{\texttt{0001}}^\textsf{1} \ . \
\overbrace{\texttt{0010}}^\textsf{2}\overbrace{\texttt{0001}}^\textsf{1} \ . \
\overbrace{\texttt{1100}}^\textsf{C}\overbrace{\texttt{1000}}^\textsf{8} = \\\\
2^7 + 2^6 + 2^4 + 2^3 + 2^1 \ . \
2^0 \ . \
2^5 + 2^0 \ . \
2^7 + 2^6 + 2^3 = \\\\
128 + 64 + 16 + 8 + 2 \ . \
1 \ . \
32 + 1 \ . \
128 + 64 + 8 = \\\\
\texttt{218.1.33.200}
$$

## Problem 5

> In the network $\texttt{112.0.0.0/15}$
>
> 1.  A router wants to send a packet to every host in this network. What should
      be the destination IP address?
> 1.  A host wants to send a packet to every host in this network. What should
      be the destination IP address?

## Problem 6

> Find the network address, the direct broadcast address, and the total number
  of addresses in the network, if one of the addresses is
  $\texttt{183.70.230.23/20}$.

## Problem 7

> The network $\texttt{126.154.24.0/21}$ is divided into $32\ \textsf{subnets}$.
  Can the following IP addresses be assigned to hosts? Explain your answers.
>
> 1.  $\texttt{126.154.24.0}$
> 1.  $\texttt{126.154.24.128}$
> 1.  $\texttt{126.154.25.120}$
> 1.  $\texttt{126.154.31.255}$

## Problem 8

> Find the $2149\textsf{th} address$ and the last address of the block
  $\texttt{123.0.0.0/18}$.

## Problem 9

> The addresses of two hosts in a certain network are $\texttt{187.93.25.97}$
  and $\texttt{187.93.127.230}$. Assume classful addressing. How many addresses
  are there:
>
> 1.  Between these two addresses?
> 1.  In the entire network?

## Problem 10

> An organization is allocated a block of addresses $\texttt{25.4.32.0/22}$ and
  needs $7\ \textsf{subnets}$. Find the number of addresses in this block and
  design the following subnets. Give the mask and the range of addresses for
  each of them.
>
> 1.  $1\ \textsf{subnets}$ of $512\ \textsf{addresses}$
> 1.  $2\ \textsf{subnets}$ of $128\ \textsf{addresses}$
> 1.  $2\ \textsf{subnets}$ of $64\ \textsf{addresses}$
> 1.  $2\ \textsf{subnets}$ of $32\ \textsf{addresses}$

## Problem 11

> An organization has received an IP address block for its internal network. The
  IP address $\texttt{154.101.43.163}$ is identified as the
  $36\textsf{th address}$ within this block. The organization requires
  $72\ \textsf{IP addresses}$ to accommodate hosts and networking devices.
>
> 1.  Determine the full range of IP addresses allocated to this organization.
> 1.  Are there any unused IP addresses in this allocation? If so, calculate the
      number of such addresses.

# Problem 12

> A routing table of a certain router (the next-hop addresses have been omitted)
  is given below. For each of the following destination IP addresses, determine
  which interface the router would use to forward the packet. Explain each
  answer.
>
> 1.  $\texttt{187.123.224.131}$
> 1.  $\texttt{172.15.45.12}$
> 1.  $\texttt{201.4.200.20}$
> 1.  $\texttt{187.123.224.50}$
> 1.  $\texttt{180.75.20.10}$

Mask | Network Address | Interface
--- | --- | ---
$\texttt{/25}$ | $\texttt{187.123.224.0}$ | M0
$\texttt{/18}$ | $\texttt{201.4.0.0}$ | M1
$\texttt{/17}$ | $\texttt{201.4.128.0}$ | M2
$\texttt{/15}$ | $\texttt{180.74.0.0}$ | M3
Default | Default | M4

## Problem 13

> The block of addresses $\texttt{146.157.224.0/19}$ is divided into
  $3\ \textsf{subblocks}$. The $1\textsf{st subblock}$ is allocated to a group
  of $12\ \textsf{customers}$, each of which needs $64\ \textsf{ addresses}$.
  The $2\textsf{nd subblock}$ is allocated to a group of
  $9\ \textsf{customers}$, each of which needs $32\ \textsf{addresses}$. The
  $3\textsf{rd subblock}$ is allocated to a group of $5\ \textsf{customers}$,
  each of which needs $16\ \textsf{addresses}$.
>
> 1.  Design the three subblocks. Find the mask for each of them (i.e. for each
      subblock not for each customer).
> 1.  What is the range of addresses (find the first and last of them) allocated
      to the $10\textsf{th customer}$ in the $1\textsf{st subblock}$?
> 1.  What is the range of addresses (find the first and last of them) allocated
      to the $5\textsf{th customer}$ in the $2\textsf{nd subblock}$?
> 1.  What is the range of addresses (find the first and last of them) allocated
      to the $3\textsf{rd customer}$ in the $3\textsf{rd subblock}$?
> 1.  How many addresses are still available after this allocation in each
      of the three subblocks?
> 1.  How many addresses in the entire original block are still available for
      allocation?

## Problem 14

> What are the main duties of the Presentation Layer?
