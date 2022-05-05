---
title: Game
date: 2022-05-05T05:23:00Z
weight: 20
---

In this game, we receive blocks one by one. Our goal is to
determine if the block is valid and if yes, where it should
be placed in the "blockchain tree". The bonus goal is
to keep track of the longest chain, i.e. the main chain.

{{% notice note %}}
Branch and chain are used interchangeably here.
{{% /notice %}}

A branch is the series of blocks going from a leaf (a block that has no follower) to the first block 

## Block Data

A block will have:
- `hash` value. It serves as its ID.
- `prev_hash` field. It is used to link to the previous block.
- `pow` field. The longest chain is the one that has the highest cumulative POW.
That value is calculated by summing the POW of every block that forms the chain.
- a list of Nullifiers. A Nullifier is also a hash value. It represents the expenditure
of some (hidden) amount of coins. To prevent double spending, we enforce the following
rule:

{{% notice note %}}
On any branch, a nullifier may only appear *ONCE*
{{% /notice %}}

However, it is possible to have a nullifier appearing more than once in the tree
as long as it is on different branches.

## Valid Chains

If the `prev_hash` of an incoming block is the `hash` of a previous block, we
want to place it in the tree regardless of whether it has a double-spend.
But, a chain that has a double-spend MUST be invalid.

## Results

After all the blocks are placed, we want to know which *valid* branch is the longest.

