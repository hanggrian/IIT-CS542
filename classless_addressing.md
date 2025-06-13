# Classless addressing

In classless addressing, variable-length blocks are assigned that belong to no
class. We can have a block of $2 \ \textsf{addresses}$,
$4 \ \textsf{addresses}$, $128 \ \textsf{addresses}$ and so on. In this
architecture, the entire address space ($2^{32} \ \textsf{addresses}$) is
divided into blocks of different sizes.

1.  The number of addresses in a block must be a power of $2$.
    ($2, 4, 8, 16, \dots$)
1.  The first address in the block must be evenly divisible by the number of
    addresses. For example, if a block contains $4 \ \textsf{addresses}$, the
    first address must be divisible by $4$. If a block contains
    $16 \ \textsf{addresses}$, the first address must be divisible by $16$.

> #### Example 1
>
> > Which of the following addresses can be the beginning address of a block
    that contains $16 \ \textsf{addresses}$?
