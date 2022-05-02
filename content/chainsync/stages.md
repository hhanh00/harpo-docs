---
title: Stages
date: 2022-05-02T11:58:32Z
weight: 10
---

ChainSync: CS

## Purpose of ChainSync CS
- Download and process blocks from peers
- Synchronize the blockchain
- Update chain state

## Stages
- CS starts when node boots and stops when the node stops
- CS is normally is mode CS_FOLLOW
- CS starts in CS_INIT
- If the chain is too far behind the current tip, CS switches to
CS_SYNC

### CS_INIT

- Tip is set to last known best, or latest checkpoint or genesis
block

### CS_SYNC

- Indicates that our node is too far behind and should quickly
download and sync up
- Sync relies on a "torrent" like download mechanism
- Mode is entered when the median of the height of the
peers is farther than 1 block from tip, for 30 seconds
- Mode is exited when at the end of the sync process, node is no
longer in the above situation

### CS_FOLLOW

- Receives blocks through Gossip protocol and process them