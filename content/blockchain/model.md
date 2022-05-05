---
title: Data Model
date: 2022-05-05T04:58:40Z
weight: 10
---

As its name suggests, the Blockchain is a set of blocks
roughly organized as a chain. Ideally, every block
would be neatly lined up and form a single linked list.

## Block

A block has the following properties:
- a hash value that serves as its unique identifier. Hash values
are considered unique as long as they refer to different content
- a reference to the previous block as a field `prev_hash`

These two values are enough for linking the blocks.

The rest of the properties are related to the "blockchain rules".

It is not enough for a block to be structurally correct to be
allowed in the blockchain. It must also follow other rules
that enforce the correct business behavior.

## Proof of Work

A block has a proof of work value. It is computed based on the current
block difficulty. A block is accepted if its hash is below a hash value
derived from the difficulty. The higher the difficulty, the lower the
threshold. Miners can affect the block hash by varying the `nonce` field
of the block header. 

## Block Tree

As mentioned earlier, we wish blocks would always follow one another. But
by the nature of decentralized mining, it is possible, in fact, it is a
relatively common occurrence, to see two blocks or more following the same
block.

For example, a miner in Asia and a miner in Europe may both independently
find a suitable `nonce` and produce different but valid blocks.

In this case, we should remember that none of the new blocks is intrinsically
better. The network is split between nodes that received and processed
the "first" new block and the nodes that received and processed the "other".
However, the notion of "first" and "second" is relative. Every node would not 
receive the blocks in the same order due to their geographic and network distance.

We say that the network has a "split-brain" and is not consistent.
The blocks possibly can contain different transactions, leading to some of the nodes
thinking that certain transactions were made but other nodes don't.

It is unfortunate but normal and expected when dealing with decentralized
systems.

Therefore, the blocks do not form a perfect chain but since they can sometimes be
sharing the same predecessor, they form a tree. Typically one of the branches is
very long (it is the main chain), and there are short-lived branches from time to time.

In the next section, we'll describe the "Blockchain Game" that is a simplified
version of the set of blockchain rules.

