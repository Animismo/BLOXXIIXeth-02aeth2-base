---
description: Blocks 'n' roots
---

# Block view

_This post is going to lay out data, Ethereum 2.0 explorers such as_ [_beaconcha.in_](https://beaconcha.in/) _visualise_

## Overview

\_\_[_Epoch_](https://kb.beaconcha.in/glossary#epoch)_,_ [_Slot_](https://i.imgur.com/y8tVVUr.png)_,_ [_Status_](https://kb.beaconcha.in/glossary#validator-lifecycle)_,_ [_Proposer_](https://kb.beaconcha.in/glossary#validator-lifecycle) _are covered in the_ [_glossary_](https://kb.beaconcha.in/glossary)

### Block root

The hash-tree-root of the [BeaconBlock](https://github.com/ethereum/eth2.0-specs/blob/dev/specs/phase0/beacon-chain.md#beaconblock).

### State root

The hash-tree-root of the [BeaconState](https://github.com/ethereum/eth2.0-specs/blob/dev/specs/phase0/beacon-chain.md#beacon-state).

### Signature

The BLS signature [obtained by](https://github.com/ethereum/eth2.0-specs/blob/dev/specs/phase0/validator.md#packaging-into-a-signedbeaconblock) using the BeaconState, BeaconBlock and private key.

`def get_block_signature(state: BeaconState, block: BeaconBlock, privkey: int)   
-> BLSSignature`

### Randao Reveal

_TODO_

### Grafitti

A block proposer can include 32 byte long message to its block proposal.

### Eth 1 Data

_Received Eth1 Block headers and Deposit data_ 

* **Block Hash:** The Hash of the received Eth1 Block.
* **Deposit Count:** Amount of validator deposits to the deposit contract in this block.
* **Deposit Root:** The root of the merkle tree of deposits.

### Attestations

Amount of attestations included in this block by the block proposer.

### Deposits

Amount of validator deposits which have been included in this block by the block proposer

### Voluntary Exits

Amount of voluntary Exits which have been included in this block by the block proposer.

### Slashings

Amount of slashings which have been included in this block by the block proposer.  


![](../.gitbook/assets/image%20%28176%29.png)

##  Votes

Represents the total amount of votes in a specific block. In the example below there were 128 attestations. These attestations received a **total** of 2802 votes. The aggregation bit is an additional way of representing the votes.  


![](../.gitbook/assets/image%20%28177%29.png)

## Attestations

### Slot

Is the slot number to which the validator is attesting. The slot number points to the same block as the beacon-block-root.

### Committee Index

Every epoch the total number of validators is split up in committees and one or more individual committees are responsible to attest to each slot. The committee Index is the identifier for this specific committee during a slot.

### Aggregation Bits

Represents the aggregated attestation of all participating validators in this attestation.  
Each "1" bit is a successful attestation submitted by the validator. "0" bits visualise missed attestations.

![](../.gitbook/assets/image%20%28181%29.png)

### Validators

Validators who have submitted their attestation and have been included by the block proposer.

### Beacon Block Root

The beacon block root points to the block to which validators are attesting. The difference between the block number in which the attestation has been included, and the one the beacon block root is pointing to, causes the attestation inclusion delay.

### Source & Target

These are two additional votes a validator has to submit. The source points to the latest justified epoch, and the target to the latest epoch boundary.

### Signature

![](../.gitbook/assets/image%20%28175%29.png)

