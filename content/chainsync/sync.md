---
title: Sync Mode
date: 2022-05-02T12:21:13Z
weight: 20
---

## State

- Peers
    - PeerId
    - Listen address
    - Hash, Height
- Peer Leader: Peer that has the highest height, only peer
we request headers from
- Headers
    - Headers are requested sequentially from Leader
    - Response headers begin in DETACHED state

## Chain Fragment Header State
- List of headers received from GetHeaders
- DETACHED: headers have hash but no height, not validated and not connected to blockchain
- PARTIAL_LINKED: prev_hash links with hash of previous header. Headers
form a list. No POW check, no timestamp check. Chain is not anchored yet.
Trim headers that do not link and move them to INVALID state
- ANCHORED: First header links to a known tip. We can perform more validation
    - timestamp
    - POW
    - nonce
    - Then trim the headers that fail validation
    - Remaining headers => Get Block using BlockSync
- Send header fragment to block sync downloader

## Header
- INVALID: Header failed validation and is rejected

## Block Sync

- Download blocks from multiple peers

## Block
- Validate if block is right after current best tip
    - if block validates, 
        - advance tip, 
        - update best tip if needed
        - look for next block and repeat
    - if block does not validate, 
        - mark remaining blocks/headers as INVALID
        - evict Leader
        - end CHAIN_SYNC
        - retry CHAIN_SYNC with next best peer
- If no more header fragments, end SYNC

## Peer API

- GetLastHeight -> height, hash
- GetHeaders(start_height, start_hash, num_headers) -> [BlockHeader]
    Return up to num_headers from given (start_height, start_hash)
    Error if start header is not known
- GetBlock(hash) -> Block

