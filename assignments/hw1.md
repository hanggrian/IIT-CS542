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
  subnets if the desired number is:
>
> 1.  6 subnets
> 1.  62 subnets
> 1.  122 subnets
> 1.  250 subnets

In a fixed-length subnetting, $2^n$ subnets are created where $n$ bits are
borrowed. To find the minimum number of created subnets, find the smallest $n$
where $2^n$ is greater than (or equal to) the target number of subnets.

$$
\begin{align}
  n &= 2 && 2^2 = 4 < 6 & \textsf{NO} \\\\
  n &= 3 && 2^3 = 8 \geq 6 & \textbf{YES} \\\\
  n &= 5 && 2^5 = 32 < 62 & \textsf{NO} \\\\
  n &= 6 && 2^6 = 64 \geq 62 & \textbf{YES} \\\\
  & && 2^6 = 64 < 122 & \textsf{NO} \\\\
  n &= 7 && 2^7 = 128 \geq 122 & \textbf{YES} \\\\
  & && 2^7 = 128 < 250 & \textsf{NO} \\\\
  n &= 8 && 2^8 = 256 \geq 250 & \textbf{YES}
\end{align}
$$

Therefore, the minimum number of created subnets for each case is:

1.  **6 subnets: $\mathbf{8} \ \textbf{addresses}$.**
1.  **62 subnets: $\mathbf{64} \ \textbf{addresses}$.**
1.  **122 subnets: $\mathbf{128} \ \textbf{addresses}$.**
1.  **250 subnets: $\mathbf{256} \ \textbf{addresses}$.**

## Problem 3

> If you subnet the network $\texttt{11.0.0.0}$ with a subnet mask of
  $\texttt{255.255.240.0}$, what is the maximum number of subnets and usable
  addresses per subnet? A usable address is an address that can be assigned to a
  host or a router. Assume classful addressing.

The first byte of the network $\texttt{11.0.0.0}$ determines the class.

$$
0 \leq 11 \leq 127 \Rightarrow \textbf{Class A}
$$

In class A, the first byte is used for net ID while the remaining three bytes
are used for host ID.

$$
\begin{align}
  \textsf{Default mask} &=
  \underbrace{\texttt{255}}_{128 + 64 + 32 + 16 + 8 + 4 + 2 + 1} .
  \texttt{0.0.0} \\\\
  &= (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad 0 . \\\\
  &\quad 0 . \\\\
  &\quad 0 \\\\
  &= \texttt{11111111.00000000.00000000.00000000} &= \mathbf{8} \ \textbf{bits}
\end{align}
$$

$$
\begin{align}
  \textsf{Subnet mask} &=
  \texttt{255} .
  \texttt{255} .
  \underbrace{\texttt{240}}_{128 + 64 + 32 + 16} .
  \texttt{0} \\\\
  &= (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4) . \\\\
  &\quad 0 \\\\
  &= \texttt{11111111.11111111.11110000.00000000} &= \mathbf{20} \ \textbf{bits}
\end{align}
$$

The difference between the bits of the subnet mask and the default mask
determines the borrowed bits. Then, the maximum number of subnets can be
calculated as $2^\textsf{Borrowed bits}$.

$$
\begin{align}
  \textsf{Borrowed bits} &= \textsf{Network bits} - \textsf{Default mask bits} \\\\
  &= 20 - 8 &= \textbf{12} \\\\
  \textsf{Max. subnets} &= 2^\textsf{Borrowed bits} \\\\
  &= 2^{12} &= \mathbf{4,096}
\end{align}
$$

For usable addresses per subnet, find the remaining host bits and calculate
using the formula $2^\textsf{Host bits} - 2$, where the two
subtracted addresses are the network address and the broadcast address.

$$
\begin{align}
  \textsf{Host bits} &= 32 - \textsf{Network bits} \\\\
  &= 32 - 20 &= \mathbf{12} \\\\
  \textsf{Total addresses} &= 2^\textsf{Host bits} \\\\
  &= 2^{12} &= \mathbf{4,096} \\\\
  \textsf{Usable addresses} &= \textsf{Total addresses} - 2 \\\\
  &= 4,096 - 2 &= \mathbf{4,094}
\end{align}
$$

## Problem 4

> Convert the IP address $\texttt{0xDA0121C8}$ to the dotted decimal notation.
  What is the class of this IP address?

First, we convert the hexadecimal $\texttt{0xDA0121C8}$ to binary notation,
dividing it into 4 bytes. The decimal values are summed up for each byte.

$$
\begin{align}
  \overbrace{\texttt{1101}}^\textsf{D} \overbrace{\texttt{1010}}^\textsf{A} \ . \
  \overbrace{\texttt{0000}}^\textsf{0} \overbrace{\texttt{0001}}^\textsf{1} \ . \
  \overbrace{\texttt{0010}}^\textsf{2} \overbrace{\texttt{0001}}^\textsf{1} \ . \
  \overbrace{\texttt{1100}}^\textsf{C} \overbrace{\texttt{1000}}^\textsf{8} &= \\\\
  (2^7 + 2^6 + 2^4 + 2^3 + 2^1) . \\\\
  2^0 . \\\\
  (2^5 + 2^0) . \\\\
  (2^7 + 2^6 + 2^3) &= \\\\
  (128 + 64 + 16 + 8 + 2) . \\\\
  1 . \\\\
  (32 + 1) . \\\\
  (128 + 64 + 8) &= \texttt{218.1.33.200}
\end{align}
$$

Finally, the first byte determines the class of the IP address.

$$
192 \leq 218 \leq 223 \Rightarrow \textbf{Class C}
$$

## Problem 5

> In the network $\texttt{112.0.0.0/15}$
>
> 1.  A router wants to send a packet to every host in this network. What should
      be the destination IP address?
> 1.  A host wants to send a packet to every host in this network. What should
      be the destination IP address?

Convert the address $\texttt{112.0.0.0}$ to binary notation. The subnet mask
$\texttt{/15}$ means that the first 15 bits are used for the network ID.

$$
\begin{align}
  \textsf{Address} &= \underbrace{112}_{64 + 32 + 16} . \texttt{0.0.0} \\\\
  &= (2^6 + 2^5 + 2^4) . \\\\
  &\quad 0 . \\\\
  &\quad 0 . \\\\
  &\quad 0 \\\\
  &= \texttt{01110000.00000000.00000000.00000000} \\\\
  \textsf{Subnet mask (/15)} &= \underline{\texttt{11111111.11111110.00000000.00000000}} \\\\
  \textsf{Network address} &= \texttt{01110000.00000000.00000000.00000000}
\end{align}
$$

To find the broadcast address, set the host bits to $1$ and perform OR
operation.

$$
\begin{align}
  \textsf{Network address} &= \texttt{01110000.00000000.00000000.00000000} \\\\
  \textsf{Inv. subnet mask} &= \underline{\texttt{00000000.00000001.11111111.11111111}} \\\\
  \textsf{Broadcast address} &= \texttt{01110000.00000001.11111111.11111111} \\\\
  &= (2^6 + 2^5 + 2^4) . \\\\
  &\quad 2^0 . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) \\\\
  &= (64 + 32 + 16) . \\\\
  &\quad 1 . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) &= \texttt{112.1.255.255}
\end{align}
$$

Considering the scenario:

- **Router to every host: $\texttt{112.1.255.255}$.** The router needs to reach
  all hosts in $\texttt{112.0.0.0/15}$. It uses the local broadcast address
  calculated above.
- **Host to every host: $\texttt{112.1.255.255}$.** Hosts use the same local
  broadcast address to reach other hosts in the same network.

## Problem 6

> Find the network address, the direct broadcast address, and the total number
  of addresses in the network, if one of the addresses is
  $\texttt{183.70.230.23/20}$.

The network address can be found by performing AND operation between the
address $\texttt{183.70.230.23}$ and the subnet mask $\texttt{/20}$.

$$
\begin{align}
  \textsf{Address} &= \texttt{183.70.230.23} \\\\
  &= (128 + 32 + 16 + 4 + 2 + 1) . \\\\
  &\quad (64 + 4 + 2) . \\\\
  &\quad (128 + 64 + 32 + 4 + 2) . \\\\
  &\quad (16 + 4 + 2 + 1) \\\\
  &= (2^7 + 2^5 + 2^4 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^6 + 2^2 + 2^1) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^2 + 2^1) . \\\\
  &\quad (2^4 + 2^2 + 2^1 + 2^0) \\\\
  &= \texttt{10110111.01000110.11100110.00010111} \\\\
  \textsf{Subnet mask (/20)} &= \underline{\texttt{11111111.11111111.11110000.00000000}} \\\\
  \textsf{Network address} &= \texttt{10110111.01000110.11100000.00000000} \\\\
  &= (2^7 + 2^5 + 2^4 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^6 + 2^2 + 2^1) . \\\\
  &\quad (2^7 + 2^6 + 2^5) . \\\\
  &\quad 0 \\\\
  &= (128 + 32 + 16 + 4 + 2 + 1) . \\\\
  &\quad (64 + 4 + 2) . \\\\
  &\quad (128 + 64 + 32) . \\\\
  &\quad 0 &= \texttt{183.70.224.0}
\end{align}
$$

For the direct broadcast address, we can perform OR operation between the
network address and the inverted subnet mask.

$$
\begin{align}
  \textsf{Network address} &= \texttt{10110111.01000110.11100000.00000000} \\\\
  \textsf{Inv. subnet mask} &= \underline{\texttt{00000000.00000000.00001111.11111111}} \\\\
  \textsf{Broadcast address} &= \texttt{10110111.01000110.11101111.11111111} \\\\
  &= (2^7 + 2^5 + 2^4 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^6 + 2^2 + 2^1) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) \\\\
  &= (128 + 32 + 16 + 4 + 2 + 1) . \\\\
  &\quad (64 + 4 + 2) . \\\\
  &\quad (128 + 64 + 32 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) &= \texttt{183.70.239.255}
\end{align}
$$

The total number of addresses in the network is found by
$2^\textsf{Host bits}$.

$$
\begin{align}
  \textsf{Host bits} &= 32 - \textsf{Network bits} \\\\
  &= 32 - 26 &= \mathbf{6} \\\\
  \textsf{Total addresses} &= 2^\textsf{Host bits} \\\\
  &= 2^{6} &= \mathbf{64}
\end{align}
$$

## Problem 7

> The network $\texttt{126.154.24.0/21}$ is divided into $32 \ \textsf{subnets}$.
  Can the following IP addresses be assigned to hosts? Explain your answers.
>
> 1.  $\texttt{126.154.24.0}$
> 1.  $\texttt{126.154.24.128}$
> 1.  $\texttt{126.154.25.120}$
> 1.  $\texttt{126.154.31.255}$

We need to determine the new subnet mask from the original subnet
$\texttt{/21}$, using the additional bits borrowed from the host part to create
subnets.

$$
\begin{align}
  \textsf{Subnets} &= 2^\textsf{Borrowed bits} \\\\
  32 &= 2^\textsf{Borrowed bits} \\\\
  \textsf{Borrowed bits} &= 5 \ \textsf{bits} \\\\
  \textsf{New subnet mask} &= \textsf{Original subnet} + \textsf{Borrowed bits} \\\\
  &= /21 + 5 \ \textsf{bits} &= \mathbf{/26}
\end{align}
$$

With the new subnet mask of $\texttt{/26}$, we can calculate the number of bits
and number of addresses per subnet.

$$
\begin{align}
  \textsf{Host bits} &= 32 - \textsf{Network bits} \\\\
  &= 32 - 26 &= \mathbf{6} \\\\
  \textsf{Total addresses} &= 2^\textsf{Host bits} \\\\
  &= 2^{6} &= \mathbf{64}
\end{align}
$$

There are $64 \ \textsf{addresses}$ in each $32 \ \textsf{subnet}$, covering
the range:

Subnet # | Network range
---: | ---
1 | $\texttt{126.154.24.0} \to \texttt{126.154.24.63}$
2 | $\texttt{126.154.24.64} \to \texttt{126.154.24.127}$
3 | $\texttt{126.154.24.128} \to \texttt{126.154.24.191}$
4 | $\texttt{126.154.24.192} \to \texttt{126.154.24.255}$
5 | $\texttt{126.154.25.0} \to \texttt{126.154.25.63}$
6 | $\texttt{126.154.25.64} \to \texttt{126.154.25.127}$
7 | $\texttt{126.154.25.128} \to \texttt{126.154.25.191}$
8 | $\texttt{126.154.25.192} \to \texttt{126.154.25.255}$
9 | $\texttt{126.154.26.0} \to \texttt{126.154.26.63}$
10 | $\texttt{126.154.26.64} \to \texttt{126.154.26.127}$
11 | $\texttt{126.154.26.128} \to \texttt{126.154.26.191}$
12 | $\texttt{126.154.26.192} \to \texttt{126.154.26.255}$
13 | $\texttt{126.154.27.0} \to \texttt{126.154.27.63}$
14 | $\texttt{126.154.27.64} \to \texttt{126.154.27.127}$
15 | $\texttt{126.154.27.128} \to \texttt{126.154.27.191}$
16 | $\texttt{126.154.27.192} \to \texttt{126.154.27.255}$
17 | $\texttt{126.154.28.0} \to \texttt{126.154.28.63}$
18 | $\texttt{126.154.28.64} \to \texttt{126.154.28.127}$
19 | $\texttt{126.154.28.128} \to \texttt{126.154.28.191}$
20 | $\texttt{126.154.28.192} \to \texttt{126.154.28.255}$
21 | $\texttt{126.154.29.0} \to \texttt{126.154.29.63}$
22 | $\texttt{126.154.29.64} \to \texttt{126.154.29.127}$
23 | $\texttt{126.154.29.128} \to \texttt{126.154.29.191}$
24 | $\texttt{126.154.29.192} \to \texttt{126.154.29.255}$
25 | $\texttt{126.154.30.0} \to \texttt{126.154.30.63}$
26 | $\texttt{126.154.30.64} \to \texttt{126.154.30.127}$
27 | $\texttt{126.154.30.128} \to \texttt{126.154.30.191}$
28 | $\texttt{126.154.30.192} \to \texttt{126.154.30.255}$
29 | $\texttt{126.154.31.0} \to \texttt{126.154.31.63}$
30 | $\texttt{126.154.31.64} \to \texttt{126.154.31.127}$
31 | $\texttt{126.154.31.128} \to \texttt{126.154.31.191}$
32 | $\texttt{126.154.31.192} \to \texttt{126.154.31.255}$

The first address in each subnet is the network address while the last address
is the broadcast address. Considering whether the given addresses can be
assigned to hosts:

1.  **$\texttt{126.154.24.0}$: No.** This address is reserved as the network
    address for *Subnet #1.*
1.  **$\texttt{126.154.24.128}$: No.** Like the previous case, this address also
    serves as the network address for *Subnet #3.*
1.  **$\texttt{126.154.25.120}$: Yes.** This address can be assigned in
    *Subnet #6.*
1.  **$\texttt{126.154.31.255}$: No.** This address is used as the broadcast
    address for *Subnet #32.*

## Problem 8

> Find the $2,149 \textsf{th address}$ and the last address of the block
  $\texttt{123.0.0.0/18}$.

Using the subnet mask $\texttt{/18}$, we can evaluate the host bits and the
total number of addresses in the block.

$$
\begin{align}
  \textsf{Host bits} &= 32 - \textsf{Network bits} \\\\
  &= 32 - 18 &= \mathbf{14} \\\\
  \textsf{Total addresses} &= 2^\textsf{Host bits} \\\\
  &= 2^{14} &= \mathbf{16,384}
\end{align}
$$

The network address can be calculated by performing AND operation between the
address and the subnet mask $\texttt{/18}$.

$$
\begin{align}
  \textsf{Address} &= \texttt{123.0.0.0} \\\\
  &= (64 + 32 + 16 + 8 + 2 + 1) . \\\\
  &\quad 0 . \\\\
  &\quad 0 . \\\\
  &\quad 0 \\\\
  &= (2^6 + 2^5 + 2^4 + 2^3 + 2^1 + 2^0) . \\\\
  &\quad 0 . \\\\
  &\quad 0 . \\\\
  &\quad 0 \\\\
  &= \texttt{01111011.00000000.00000000.00000000} \\\\
  \textsf{Subnet mask (/18)} &= \underline{\texttt{11111111.11111111.11000000.00000000}} \\\\
  \textsf{Network address} &= \texttt{01111011.00000000.00000000.00000000} \\\\
  &= (2^6 + 2^5 + 2^4 + 2^3 + 2^1 + 2^0) . \\\\
  &\quad 0 . \\\\
  &\quad 0 . \\\\
  &\quad 0 \\\\
  &= (64 + 32 + 16 + 8 + 2 + 1) . \\\\
  &\quad 0 . \\\\
  &\quad 0 . \\\\
  &\quad 0 &= \texttt{123.0.0.0}
\end{align}
$$

The broadcast address is computed by performing OR operation between the network
address and the inverted subnet mask.

$$
\begin{align}
  \textsf{Network address} &= \texttt{01111011.00000000.00000000.00000000} \\\\
  \textsf{Inv. subnet mask} &= \underline{\texttt{00000000.00000000.00111111.11111111}} \\\\
  \textsf{Broadcast address} &= \texttt{01111011.00000000.00111111.11111111} \\\\
  &= (2^6 + 2^5 + 2^4 + 2^3 + 2^1 + 2^0) . \\\\
  &\quad 0 . \\\\
  &\quad (2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) \\\\
  &= (64 + 32 + 16 + 8 + 2 + 1) . \\\\
  &\quad 0 . \\\\
  &\quad (32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) &= \texttt{123.0.63.255}
\end{align}
$$

We need to find the $2149 \textsf{th address}$ in the block, starting from the
network address $\texttt{123.0.0.0}$ and must not exceed the broadcast
address $\texttt{123.0.63.255}$. Convert the network address to integer, append
the $2149 \textsf{th address} - 1 \ \textsf{address}$, where the addition is the
reserved network address.

$$
\begin{align}
  \textsf{Network address} &= \texttt{123.0.0.0} \\\\
  &= (123 \times 256^3) + \\\\
  &\quad 0 + \\\\
  &\quad 0 + \\\\
  &\quad 0 \\\\
  &= (123 \times 16,777,216) . \\\\
  &\quad 0 . \\\\
  &\quad 0 . \\\\
  &\quad 0 &= \mathbf{2,063,597,568} \\\\
  2149 \textsf{th address} &= \textsf{Network address} + (2149 - 1) \\\\
  &= 2,063,597,568 + 2,148 &= \mathbf{2,063,599,716}
\end{align}
$$

Convert the integer back to dotted decimal notation.

$$
\begin{align}
  \textsf{current} &= 2,063,599,716 && \textsf{Byte \#}4 = 2,063,599,716 \mod 256 &= \mathbf{100} \\\\
  &= \left\lfloor \frac{2,063,599,716}{256} \right\rfloor = 8,060,936 && \textsf{Byte \#}3 = 8,060,936 \mod 256 &= \mathbf{8} \\\\
  &= \left\lfloor \frac{8,060,936}{256} \right\rfloor = 31,488 && \textsf{Byte \#}2 = 31,488 \mod 256 &= \mathbf{0} \\\\
  &= \left\lfloor \frac{31,488}{256} \right\rfloor = 123 && \textsf{Byte \#}1 &= \mathbf{123} \\\\
  & && 2149 \textsf{th address} = \texttt{123.0.8.100} & \hookleftarrow
\end{align}
$$

## Problem 9

> The addresses of two hosts in a certain network are $\texttt{187.93.25.97}$
  and $\texttt{187.93.127.230}$. Assume classful addressing. How many addresses
  are there:
>
> 1.  Between these two addresses?
> 1.  In the entire network?

The difference between the two addresses can be found by subtracting the integer
form of each address.

$$
\begin{align}
  \textsf{Address \#} 1 &= \texttt{187.93.25.97} \\\\
  &= (187 \times 256^3) + \\\\
  &\quad (93 \times 256^2) + \\\\
  &\quad (25 \times 256^1) + \\\\
  &\quad 97 \\\\
  &= (187 \times 16,777,216) + \\\\
  &\quad (93 \times 65,536) + \\\\
  &\quad (25 \times 256) + \\\\
  &\quad 97 \\\\
  &= 3,137,339,392 + 6,094,848 + 6,400 + 97 &= \mathbf{3,143,440,737} \\\\
  \textsf{Address \#} 2 &= \texttt{187.93.127.230} \\\\
  &= (187 \times 256^3) + \\\\
  &\quad (93 \times 256^2) + \\\\
  &\quad (127 \times 256^1) + \\\\
  &\quad 230 \\\\
  &= (187 \times 16,777,216) + \\\\
  &\quad (93 \times 65,536) + \\\\
  &\quad (127 \times 256) + \\\\
  &\quad 230 \\\\
  &= 3,137,339,392 + 6,094,848 + 32,512 + 230 &= \mathbf{3,143,466,982} \\\\
  \textsf{Addresses between} &= \textsf{Address \#} 2 - \textsf{Address \#} 1 \\\\
  &= 3,143,466,982 - 3,143,440,737 &= \mathbf{26,245} \\\\
  \textsf{Usable addresses} &= \textsf{Addresses between} - 2 \\\\
  &= 26,245 - 2 &= \mathbf{26,243}
\end{align}
$$

In a classful addressing, the first byte of both addresses determines the class.

$$
\begin{align}
  128 \leq 187 \leq 191 \Rightarrow \textbf{Class B}
\end{align}
$$

The netid portion of a class B address is the first two bytes, while the rest
are used for the hostid portion. The host $16 \ \textsf{bits}$ determine the
total number of addresses in the network.

$$
\begin{align}
  \textsf{Total addresses} &= 2^\textsf{Host bits} \\\\
  &= 2^{16} &= \mathbf{65,536} \\\\
\end{align}
$$

Gathering the results:

1.  **Between the two addresses: $\mathbf{26,243} \ \textbf{addresses}$.**
    $2 \ \textsf{addresses}$ are excluded for the network address and the
    broadcast address.
1.  **In the entire network: $\mathbf{65,536} \ \textbf{addresses}$.**

## Problem 10

> An organization is allocated a block of addresses $\texttt{25.4.32.0/22}$ and
  needs $7 \ \textsf{subnets}$. Find the number of addresses in this block and
  design the following subnets. Give the mask and the range of addresses for
  each of them.
>
> 1.  1 subnet of 512 addresses
> 1.  2 subnets of 128 addresses
> 1.  2 subnets of 64 addresses
> 1.  2 subnets of 32 addresses

Using previous exercises, we can find the number of addresses in the block
with the subnet mask $\texttt{/22}$.

$$
\begin{align}
  \textsf{Total addresses} &= 2^{32 - 22} \\\\
  &= 2^{10} &= \mathbf{1,024}
\end{align}
$$

Next, find out the subnet mask for each of the $7 \ \textsf{subnets}$.

$$
\begin{align}
  \textsf{Subnet host bits \#} 1 &= \log_2 512 &= \mathbf{9} \\\\
  \textsf{Subnet network bits \#} 1 &= 32 - 9 &= \mathbf{23} \\\\
  \textsf{Subnet mask \#} 1 \ \textsf{(/23)} &= \texttt{11111111.11111111.11111110.00000000} \\\\
  &= (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1) . \\\\
  &\quad 0 \\\\
  &= (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2) . \\\\
  &\quad 0 &= \texttt{255.255.254.0} \\\\
  \textsf{Subnet host bits \#} 2–3 &= \log_2 128 &= \mathbf{7} \\\\
  \textsf{Subnet network bits \#} 2–3 &= 32 - 7 &= \mathbf{25} \\\\
  \textsf{Subnet mask \#} 2–3 \ \textsf{(/25)} &= \texttt{11111111.11111111.11111111.10000000} \\\\
  &= (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad 2^7 \\\\
  &= (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad 128 &= \texttt{255.255.255.128} \\\\
  \textsf{Subnet host bits \#} 4–5 &= \log_2 64 &= \mathbf{6} \\\\
  \textsf{Subnet network bits \#} 4–5 &= 32 - 6 &= \mathbf{26} \\\\
  \textsf{Subnet mask \#} 4–5 \ \textsf{(/26)} &= \texttt{11111111.11111111.11111111.11000000} \\\\
  &= (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6) \\\\
  &= (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64) &= \texttt{255.255.255.192} \\\\
  \textsf{Subnet host bits \#} 6–7 &= \log_2 32 &= \mathbf{5} \\\\
  \textsf{Subnet network bits \#} 6–7 &= 32 - 5 &= \mathbf{27} \\\\
  \textsf{Subnet mask \#} 6–7 \ \textsf{(/27)} &= \texttt{11111111.11111111.11111111.11100000} \\\\
  &= (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5) \\\\
  &= (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32) &= \texttt{255.255.255.224}
\end{align}
$$

Then, we can design the subnets by incrementing the required number of addresses
from the network address $\texttt{25.4.32.0}$.

$$
\begin{align}
  \textsf{current} &= \texttt{25.4.32.0} \to \texttt{25.4.32.255} && \textsf{Subnet \#} 1 &= 512 - 256 & \\\\
  &= \texttt{25.4.33.0} \to \texttt{25.4.33.255} && &= 256 - 256 &= \mathbf{0} \\\\
  &= \texttt{25.4.34.0} \to \texttt{25.4.34.127} && \textsf{Subnet \#} 2 &= 128 - 128 &= \mathbf{0} \\\\
  &= \texttt{25.4.34.128} \to \texttt{25.4.34.255} && \textsf{Subnet \#} 3 &= 128 - 128 &= \mathbf{0} \\\\
  &= \texttt{25.4.35.0} \to \texttt{25.4.35.63} && \textsf{Subnet \#} 4 &= 64 - 64 &= \mathbf{0} \\\\
  &= \texttt{25.4.35.64} \to \texttt{25.4.35.127} && \textsf{Subnet \#} 5 &= 64 - 64 &= \mathbf{0} \\\\
  &= \texttt{25.4.35.128} \to \texttt{25.4.35.159} && \textsf{Subnet \#} 6 &= 32 - 32 &= \mathbf{0} \\\\
  &= \texttt{25.4.35.160} \to \texttt{25.4.35.191} && \textsf{Subnet \#} 7 &= 32 - 32 &= \mathbf{0}
\end{align}
$$

Therefore, the range of addresses for each subnet is:

1.  **1 subnet of 512 addresses:
    $\texttt{25.4.32.0} \to \texttt{25.4.33.255}$.**
1.  **2 subnets of 128 addresses:
    $\texttt{25.4.34.0} \to \texttt{25.4.34.255}$.**
1.  **2 subnets of 64 addresses:
    $\texttt{25.4.35.0} \to \texttt{25.4.35.127}$.**
1.  **2 subnets of 32 addresses:
    $\texttt{25.4.35.128} \to \texttt{25.4.35.191}$.**

## Problem 11

> An organization has received an IP address block for its internal network. The
  IP address $\texttt{154.101.43.163}$ is identified as the
  $36 \textsf{th address}$ within this block. The organization requires
  $72 \ \textsf{IP addresses}$ to accommodate hosts and networking devices.
>
> 1.  Determine the full range of IP addresses allocated to this organization.
> 1.  Are there any unused IP addresses in this allocation? If so, calculate the
      number of such addresses.

Knowing that $72 \ \textsf{addresses}$ are required, we need to find the host
bits so that the total number of addresses is at least $72$.

$$
\begin{align}
  n &= 6 && 2^6 = 64 < 72 & \textsf{NO} \\\\
  n &= 7 && 2^7 = 128 \geq 72 & \textbf{YES}
\end{align}
$$

The subnet mask can be found by subtracting the host bits from all available
bits in an IPv4 address, which is $32$ bits.

$$
\begin{align}
  \textsf{Network bits} &= 32 - \textsf{Host bits} \\\\
  &= 32 - 7 = \mathbf{25}
\end{align}
$$

Using the subnet mask, we can find the network address and broadcast address
using AND and OR operations, respectively.

$$
\begin{align}
  \textsf{Address} &= \texttt{154.101.43.163} \\\\
  &= (128 + 16 + 8 + 2) . \\\\
  &\quad (64 + 32 + 4 + 1) . \\\\
  &\quad (32 + 8 + 2 + 1) . \\\\
  &\quad (128 + 32 + 2 + 1) \\\\
  &= (2^7 + 2^4 + 2^3 + 2^1) . \\\\
  &\quad (2^6 + 2^5 + 2^2 + 2^0) . \\\\
  &\quad (2^5 + 2^3 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^5 + 2^1 + 2^0) \\\\
  &= \texttt{10011010.01100101.00101011.10100011} \\\\
  \textsf{Subnet mask (/25)} &= \underline{\texttt{11111111.11111111.11111111.10000000}} \\\\
  \textsf{Network address} &= \texttt{10011010.01100101.00101011.10000000} \\\\
  &= (2^7 + 2^4 + 2^3 + 2^1) . \\\\
  &\quad (2^6 + 2^5 + 2^2 + 2^0) . \\\\
  &\quad (2^5 + 2^3 + 2^1 + 2^0) . \\\\
  &\quad 2^7 \\\\
  &= (128 + 16 + 8 + 2) . \\\\
  &\quad (64 + 32 + 4 + 1) . \\\\
  &\quad (32 + 8 + 2 + 1) . \\\\
  &\quad 128 &= \texttt{154.101.43.128}
\end{align}
$$

$$
\begin{align}
  \textsf{Network address} &= \texttt{10011010.01100101.00101011.10000000} \\\\
  \textsf{Inv. subnet mask} &= \underline{\texttt{00000000.00000000.00000000.01111111}} \\\\
  \textsf{Broadcast address} &= \texttt{10011010.01100101.00101011.11111111} \\\\
  &= (2^7 + 2^4 + 2^3 + 2^1) . \\\\
  &\quad (2^6 + 2^5 + 2^2 + 2^0) . \\\\
  &\quad (2^5 + 2^3 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) \\\\
  &= (128 + 16 + 8 + 2) . \\\\
  &\quad (64 + 32 + 4 + 1) . \\\\
  &\quad (32 + 8 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) &= \texttt{154.101.43.255}
\end{align}
$$

To calculate the amount of unused addresses, we subtract the required number
of addresses from the total available addresses in the block, minus the network
and broadcast addresses.

$$
\begin{align}
  \textsf{Total addresses} &= \textsf{Required addresses} + \textsf{Unused addresses} + 2 \\\\
  128 &= 72 + \textsf{Unused addresses} + 2 \\\\
  \textsf{Unused addresses} &= 128 - 72 - 2 \\\\
  &= 128 - 74 &= \mathbf{54}
\end{align}
$$

Therefore, the answers are:

1.  **Full range: $\texttt{154.101.43.128} \to \texttt{154.101.43.255}$.**
    Starting from the network address to the broadcast address.
1.  **Unused addresses: $\mathbf{54} \ \textbf{addresses}$.** Which is the
    difference between the total addresses and the required addresses, excluding
    the reserved $2 \ \textsf{addresses}$.

## Problem 12

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
>
> Mask | Network Address | Interface
> --- | --- | ---
> $\texttt{/25}$ | $\texttt{187.123.224.0}$ | M0
> $\texttt{/18}$ | $\texttt{201.4.0.0}$ | M1
> $\texttt{/17}$ | $\texttt{201.4.128.0}$ | M2
> $\texttt{/15}$ | $\texttt{180.74.0.0}$ | M3
> Default | Default | M4

Given the network address and mask, we can determine the broadcast address for
each interface.

$$
\begin{align}
  \textsf{M0 network address} &= \texttt{187.123.224.0} \\\\
  &= (128 + 32 + 16 + 8 + 2 + 1) . \\\\
  &\quad (64 + 32 + 16 + 8 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32) . \\\\
  &\quad 0 \\\\
  &= (2^7 + 2^5 + 2^4 + 2^3 + 2^1 + 2^0) . \\\\
  &\quad (2^6 + 2^5 + 2^4 + 2^3 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5) . \\\\
  &\quad 0 \\\\
  &= \texttt{10111011.01111011.11100000.00000000} \\\\
  \textsf{M0 inv. subnet mask (/25)} &= \underline{\texttt{00000000.00000000.00000000.01111111}} \\\\
  \textsf{M0 broadcast address} &= \texttt{10111011.01111011.11100000.01111111} \\\\
  &= (2^7 + 2^5 + 2^4 + 2^3 + 2^1 + 2^0) . \\\\
  &\quad (2^6 + 2^5 + 2^4 + 2^3 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5) . \\\\
  &\quad (2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) \\\\
  &= (128 + 32 + 16 + 8 + 2 + 1) . \\\\
  &\quad (64 + 32 + 16 + 8 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32) . \\\\
  &\quad (64 + 32 + 16 + 8 + 4 + 2 + 1) &= \texttt{187.123.224.127} \\\\
  \textsf{M1 network address} &= \texttt{201.4.0.0} \\\\
  &= (128 + 64 + 8 + 1) . \\\\
  &\quad 4 . \\\\
  &\quad 0 . \\\\
  &\quad 0 . \\\\
  &= (2^7 + 2^6 + 2^3 + 2^0) . \\\\
  &\quad 2^2 . \\\\
  &\quad 0 . \\\\
  &\quad 0 . \\\\
  &= \texttt{11001001.00000100.00000000.00000000} \\\\
  \textsf{M1 inv. subnet mask (/18)} &= \underline{\texttt{00000000.00000000.00111111.11111111}} \\\\
  \textsf{M1 broadcast address} &= \texttt{11001001.00000100.00111111.11111111} \\\\
  &= (2^7 + 2^6 + 2^3 + 2^0) . \\\\
  &\quad 2^2 . \\\\
  &\quad (2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &= (128 + 64 + 8 + 1) . \\\\
  &\quad 4 . \\\\
  &\quad (32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) &= \texttt{201.4.63.255} \\\\
  \textsf{M2 network address} &= \texttt{201.4.128.0} \\\\
  &= (128 + 64 + 8 + 1) . \\\\
  &\quad 4 . \\\\
  &\quad 128 . \\\\
  &\quad 0 . \\\\
  &= (2^7 + 2^6 + 2^3 + 2^0) . \\\\
  &\quad 2^2 . \\\\
  &\quad 2^7 . \\\\
  &\quad 0 . \\\\
  &= \texttt{11001001.00000100.10000000.00000000} \\\\
  \textsf{M2 inv. subnet mask (/17)} &= \underline{\texttt{00000000.00000000.01111111.11111111}} \\\\
  \textsf{M2 broadcast address} &= \texttt{11001001.00000100.11111111.11111111} \\\\
  &= (2^7 + 2^6 + 2^3 + 2^0) . \\\\
  &\quad 2^2 . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) \\\\
  &= (128 + 64 + 8 + 1) . \\\\
  &\quad 4 . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) &= \texttt{201.4.255.255} \\\\
  \textsf{M3 network address} &= \texttt{180.74.0.0} \\\\
  &= (128 + 32 + 16 + 4) . \\\\
  &\quad (64 + 8 + 2) . \\\\
  &\quad 0 . \\\\
  &\quad 0 . \\\\
  &= (2^7 + 2^5 + 2^4 + 2^2) . \\\\
  &\quad (2^6 + 2^3 + 2^1) . \\\\
  &\quad 0 . \\\\
  &\quad 0 . \\\\
  &= \texttt{10110100.01001010.00000000.00000000} \\\\
  \textsf{M3 inv. subnet mask (/15)} &= \underline{\texttt{00000000.00000001.11111111.11111111}} \\\\
  \textsf{M3 broadcast address} &= \texttt{10110100.01001011.11111111.11111111} \\\\
  &= (2^7 + 2^5 + 2^4 + 2^2) . \\\\
  &\quad (2^6 + 2^3 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) \\\\
  &= (128 + 32 + 16 + 4) . \\\\
  &\quad (64 + 8 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) &= \texttt{180.75.255.255}
\end{align}
$$

The new table with the network range:

Interface | Mask | Network Range
--- | --- | ---
M0 | $\texttt{/25}$ | $\texttt{187.123.224.0} \to \texttt{187.123.224.127}$
M1 | $\texttt{/18}$ | $\texttt{201.4.0.0} \to \texttt{201.4.63.255}$
M2 | $\texttt{/17}$ | $\texttt{201.4.128.0} \to \texttt{204.4.255.255}$
M3 | $\texttt{/15}$ | $\texttt{180.74.0.0} \to \texttt{180.75.255.255}$
M4 | Default | Default | Default

Consider the following destination IP addresses:

1.  $\texttt{187.123.224.131} \Rightarrow \textbf{M4}$: Although the first three
    bytes match the network address of M0, the last byte is outside the range.
    There is no other match, so the default interface is used.
1.  $\texttt{172.15.45.12} \Rightarrow \textbf{M4}$: The first byte does not
    match any of the network addresses, so the default interface is used.
1.  $\texttt{201.4.200.20} \Rightarrow \textbf{M2}$: This address falls within
    the calculated range of M2.
1.  $\texttt{187.123.224.50} \Rightarrow \textbf{M0}$: The first three bytes
    match the network and broadcast addresses of M0, and the last byte is within
    the range.
1.  $\texttt{180.75.20.10} \Rightarrow \textbf{M3}$: In range of the interface
    M3. Specifically, the first two bytes match the broadcast address while the
    remaining bytes are always within the range ($\texttt{255.255}$).

## Problem 13

> The block of addresses $\texttt{146.157.224.0/19}$ is divided into
  $3 \ \textsf{subblocks}$. The $1\textsf{st subblock}$ is allocated to a group
  of $12\ \textsf{customers}$, each of which needs $64 \ \textsf{ addresses}$.
  The $2\textsf{nd subblock}$ is allocated to a group of
  $9 \ \textsf{customers}$, each of which needs $32 \ \textsf{addresses}$. The
  $3\textsf{rd subblock}$ is allocated to a group of $5 \ \textsf{customers}$,
  each of which needs $16 \ \textsf{addresses}$.
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

The subnet mask $\texttt{/19}$ determines the total number of addresses for the
entire block.

$$
\begin{align}
  \textsf{Host bits} &= 32 - \textsf{Network bits} \\\\
  &= 32 - 19 &= \mathbf{13} \\\\
  \textsf{Entire total addresses} &= 2^{\textsf{Host bits}} \\\\
  &= 2^{13} &= \mathbf{8,192}
\end{align}
$$

The required number of addresses for each subblock is calculated by multiplying
the number of customers by the number of addresses each customer needs.

$$
\begin{align}
  \textsf{Block \#1 required addresses} &= 12 \times 64 &= \mathbf{768} \\\\
  \textsf{Block \#2 required addresses} &= 9 \times 32 &= \mathbf{288} \\\\
  \textsf{Block \#3 required addresses} &= 5 \times 16 &= \mathbf{80}
\end{align}
$$

Find the total addresses that can support the required number of addresses in
each subblock.

$$
\begin{align}
  n &= 6 && 2^6 = 64 < 80 & \textsf{NO} \\\\
  n &= 7 && 2^7 = 128 \geq 80 & \textbf{YES} \\\\
  n &= 8 && 2^8 = 256 < 288 & \textsf{NO} \\\\
  n &= 9 && 2^9 = 512 \geq 288 & \textbf{YES} \\\\
  & && 2^9 = 512 < 768 & \textsf{NO} \\\\
  n &= 10 && 2^{10} = 1,024 \geq 768 & \textbf{YES}
\end{align}
$$

Subtract the total addresses of all subblocks from the entire block to find the
remaining addresses still available for the original block.

$$
\begin{align}
  \textsf{Entire remaining addresses} &= \textsf{Entire total addresses} - \\\\
  &\quad \textsf{Block \#1 total addresses} - \\\\
  &\quad \textsf{Block \#2 total addresses} - \\\\
  &\quad \textsf{Block \#3 total addresses} \\\\
  &= 8,192 - 1,024 - 512 - 128 &= \mathbf{6,528}
\end{align}
$$

Find the unused addresses by subtracting the required addresses from the total
addresses. Because a subblock does not reserve addresses for the network and
broadcast addresses, there is no further subtraction.

$$
\begin{align}
  \textsf{Block \#1 total addresses} &= \textsf{Block \#1 required addresses} - \textsf{Block \#1 unused addresses} \\\\
  1,024 &= 768 - \textsf{Block \#1 unused addresses} \\\\
  \textsf{Block \#1 unused addresses} &= 1,024 - 768 &= \mathbf{256} \\\\
  \textsf{Block \#2 total addresses} &= \textsf{Block \#2 required addresses} - \textsf{Block \#2 unused addresses} \\\\
  512 &= 288 - \textsf{Block \#2 unused addresses} \\\\
  \textsf{Block \#2 unused addresses} &= 512 - 288 &= \mathbf{224} \\\\
  \textsf{Block \#3 total addresses} &= \textsf{Block \#3 required addresses} - \textsf{Block \#3 unused addresses} \\\\
  128 &= 80 - \textsf{Block \#3 unused addresses} \\\\
  \textsf{Block \#3 unused addresses} &= 128 - 80 &= \mathbf{48}
\end{align}
$$

We can find the network bits using the calculated host bits, and in turn, the
subnet mask.

$$
\begin{align}
  \textsf{Block \#1 network bits} &= 32 - \textsf{Block \#1 host bits} \\\\
  &= 32 - 10 &= \mathbf{22} \\\\
  \textsf{Block \#1 subnet mask (/22)} &= \texttt{1111111.11111111.11111100.00000000} \\\\
  &= (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2) . \\\\
  &\quad 0 . \\\\
  &= (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4) . \\\\
  &\quad 0 &= \texttt{255.255.252.0} \\\\
  \textsf{Block \#2 network bits} &= 32 - \textsf{Block \#2 host bits} \\\\
  &= 32 - 9 &= \mathbf{23} \\\\
  \textsf{Block \#2 subnet mask (/23)} &= \texttt{11111111.11111111.11111110.00000000} \\\\
  &= (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1) . \\\\
  &\quad 0 . \\\\
  &= (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2) . \\\\
  &\quad 0 &= \texttt{255.255.254.0} \\\\
  \textsf{Block \#3 network bits} &= 32 - \textsf{Block \#3 host bits} \\\\
  &= 32 - 7 &= \mathbf{25} \\\\
  \textsf{Block \#3 subnet mask (/25)} &= \texttt{11111111.11111111.11111111.10000000} \\\\
  &= (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) . \\\\
  &\quad 2^7 . \\\\
  &= (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) . \\\\
  &\quad 128 &= \texttt{255.255.255.128}
\end{align}
$$

Starting from the network address $\texttt{146.157.224.0}$, we can find the
broadcast address by performing OR operation with the inverted subnet mask. The
next network address starts after the previous broadcast address.

$$
\begin{align}
  \textsf{Block \#1 address} &= \texttt{146.157.224.0} \\\\
  &=  (128 + 16 + 2) . \\\\
  &\quad (128 + 16 + 8 + 4 + 1) . \\\\
  &\quad (128 + 64 + 32) . \\\\
  &\quad 0 . \\\\
  &= (2^7 + 2^4 + 2^1) . \\\\
  &\quad (2^7 + 2^4 + 2^3 + 2^2 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5) . \\\\
  &\quad 0 . \\\\
  &= \texttt{10010010.10011101.11100000.00000000} \\\\
  \textsf{Block \#1 inv. subnet mask (/22)} &= \underline{\texttt{00000000.00000000.00000011.11111111}} \\\\
  \textsf{Block \#1 broadcast address} &= \texttt{10010010.10011101.11100011.11111111} \\\\
  &= (2^7 + 2^4 + 2^1) . \\\\
  &\quad (2^7 + 2^4 + 2^3 + 2^2 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^1 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) \\\\
  &= (128 + 16 + 2) . \\\\
  &\quad (128 + 16 + 8 + 4 + 1) . \\\\
  &\quad (128 + 64 + 32 + 2 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) &= \texttt{146.157.227.255} \\\\
  \textsf{Block \#2 address} &= \texttt{146.157.228.0} \\\\
  &=  (128 + 16 + 2) . \\\\
  &\quad (128 + 16 + 8 + 4 + 1) . \\\\
  &\quad (128 + 64 + 32 + 4) . \\\\
  &\quad 0 . \\\\
  &= (2^7 + 2^4 + 2^1) . \\\\
  &\quad (2^7 + 2^4 + 2^3 + 2^2 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^2) . \\\\
  &\quad 0 . \\\\
  &= \texttt{10010010.10011101.11100100.00000000} \\\\
  \textsf{Block \#2 inv. subnet mask (/23)} &= \underline{\texttt{00000000.00000000.00000001.11111111}} \\\\
  \textsf{Block \#2 broadcast address} &= \texttt{10010010.10011101.11100101.11111111} \\\\
  &= (2^7 + 2^4 + 2^1) . \\\\
  &\quad (2^7 + 2^4 + 2^3 + 2^2 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^2 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) \\\\
  &= (128 + 16 + 2) . \\\\
  &\quad (128 + 16 + 8 + 4 + 1) . \\\\
  &\quad (128 + 64 + 32 + 4 + 1) . \\\\
  &\quad (128 + 64 + 32 + 16 + 8 + 4 + 2 + 1) &= \texttt{146.157.229.255} \\\\
  \textsf{Block \#3 address} &= \texttt{146.157.230.0} \\\\
  &=  (128 + 16 + 2) . \\\\
  &\quad (128 + 16 + 8 + 4 + 1) . \\\\
  &\quad (128 + 64 + 32 + 4 + 2) . \\\\
  &\quad 0 . \\\\
  &= (2^7 + 2^4 + 2^1) . \\\\
  &\quad (2^7 + 2^4 + 2^3 + 2^2 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^2 + 2^1) . \\\\
  &\quad 0 . \\\\
  &= \texttt{10010010.10011101.11100110.00000000} \\\\
  \textsf{Block \#3 inv. subnet mask (/25)} &= \underline{\texttt{00000000.00000000.00000000.01111111}} \\\\
  \textsf{Block \#3 broadcast address} &= \texttt{10010010.10011101.11100110.01111111} \\\\
  &= (2^7 + 2^4 + 2^1) . \\\\
  &\quad (2^7 + 2^4 + 2^3 + 2^2 + 2^0) . \\\\
  &\quad (2^7 + 2^6 + 2^5 + 2^2 + 2^1) . \\\\
  &\quad (2^6 + 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0) \\\\
  &= (128 + 16 + 2) . \\\\
  &\quad (128 + 16 + 8 + 4 + 1) . \\\\
  &\quad (128 + 64 + 32 + 4 + 2) . \\\\
  &\quad (64 + 32 + 16 + 8 + 4 + 2 + 1) &= \texttt{146.157.230.127}
\end{align}
$$

Now, we have the range of addresses for each subblock:

Block # | Customers | Addresses per customer | Network Range
---: | --- | --- | ---
1 | $12$ | $64$ | $\texttt{146.157.224.0} \to \texttt{146.157.227.255}$
2 | $9$ | $32$ | $\texttt{146.157.228.0} \to \texttt{146.157.229.255}$
3 | $5$ | $16$ | $\texttt{146.157.230.0} \to \texttt{146.157.230.127}$

List the network range for all customers:

Customer # | Network Range
---: | ---
**Block #1** |
1 | $\texttt{146.157.224.0} \to \texttt{146.157.224.63}$
2 | $\texttt{146.157.224.64} \to \texttt{146.157.224.127}$
3 | $\texttt{146.157.224.128} \to \texttt{146.157.224.191}$
4 | $\texttt{146.157.224.192} \to \texttt{146.157.224.255}$
5 | $\texttt{146.157.225.0} \to \texttt{146.157.225.63}$
6 | $\texttt{146.157.225.64} \to \texttt{146.157.225.127}$
7 | $\texttt{146.157.225.128} \to \texttt{146.157.225.191}$
8 | $\texttt{146.157.225.192} \to \texttt{146.157.225.255}$
9 | $\texttt{146.157.226.0} \to \texttt{146.157.226.63}$
10 | $\texttt{146.157.226.64} \to \texttt{146.157.226.127}$
11 | $\texttt{146.157.226.128} \to \texttt{146.157.226.191}$
12 | $\texttt{146.157.226.192} \to \texttt{146.157.226.255}$
**Block #2** |
1 | $\texttt{146.157.228.0} \to \texttt{146.157.228.31}$
2 | $\texttt{146.157.228.32} \to \texttt{146.157.228.63}$
3 | $\texttt{146.157.228.64} \to \texttt{146.157.228.95}$
4 | $\texttt{146.157.228.96} \to \texttt{146.157.228.127}$
5 | $\texttt{146.157.228.128} \to \texttt{146.157.228.159}$
6 | $\texttt{146.157.228.160} \to \texttt{146.157.228.191}$
7 | $\texttt{146.157.228.192} \to \texttt{146.157.228.223}$
8 | $\texttt{146.157.228.224} \to \texttt{146.157.228.255}$
9 | $\texttt{146.157.229.0} \to \texttt{146.157.229.31}$
**Block #3** |
1 | $\texttt{146.157.230.0} \to \texttt{146.157.230.15}$
2 | $\texttt{146.157.230.16} \to \texttt{146.157.230.31}$
3 | $\texttt{146.157.230.32} \to \texttt{146.157.230.47}$
4 | $\texttt{146.157.230.48} \to \texttt{146.157.230.63}$
5 | $\texttt{146.157.230.64} \to \texttt{146.157.230.79}$

Answering the questions:

1.  **Subnet masks:** The values are obtained from subtracting the host bits
    from $32$.
    - Block #1 (/22): **$\texttt{255.255.252.0}$.**
    - Block #2 (/23): **$\texttt{255.255.254.0}$.**
    - Block #3 (/25): **$\texttt{255.255.255.128}$.**
1.  **10th customer in the 1st subblock:
    $\texttt{146.157.226.64} \to \texttt{146.157.226.127}$.**
1.  **5th customer in the 2nd subblock:
    $\texttt{146.157.228.128} \to \texttt{146.157.228.159}$.**
1.  **3rd customer in the 3rd subblock:
    $\texttt{146.157.230.32} \to \texttt{146.157.230.47}$.**
1.  **Each unused addresses:** The network and broadcast addresses are not
    reserved in the subblocks, so the value is not further subtracted by
    $2 \ \textsf{addresses}$.
    - Block #1: **$\mathbf{256} \ \textbf{addresses}$.**
    - Block #2: **$\mathbf{224} \ \textbf{addresses}$.**
    - Block #3: **$\mathbf{48} \ \textbf{addresses}$.**
1.  **Total unused addresses: $\mathbf{6,528} \ \textbf{addresses}$.** The three
    subblocks require $1,664 \ \textsf{addresses}$ from the available
    $8,192 \ \textsf{addresses}$.

## Problem 14

> What are the main duties of the Presentation Layer?

The Open System Interconnection (OSI) model defines a framework of network
communication that is divided into seven layers. At sixth layer, the
Presentation Layer is responsible for data preparation to make it presentable
for the Application Layer. Its services include:

- **Data conversion:** Translates data into a standardized format.
- **Encryption and decryption:** In an encrypted communication, the
  Presentation Layer encodes the data before sending it and decodes it upon
  receiving.
- **Data compression:** Depending on the protocol, the Presentation Layer may
  compress data to reduce the transmission time and improve efficiency.
