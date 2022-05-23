---
description: This page is all about how the communication between these chains and the
---

# Nahmii⇌Ethereum

### L1 ⇌ L2 communication

Nahmii 2.0 provides a number of contracts on L1 to interact with the L2 and vice versa. The metadata of these contracts can be found [here](https://meta.testnet.nahmii.io/addresses.json).

The main contract that is relevant for developers is the AddressManager. The AddressManager provides easy access to all the other contracts and exposes their addresses. For examples of how to interact with the Nahmii 2.0 L2 contracts, please see the provided [examples](hello-world.md).

### Token Bridges

Bridges have come to stay within the multichain world and are basically a set of contracts that helps users in moving assets from one chain (Ethereum) to another (Nahmii).\
Deposits into Nahmii take less time, about 10-15 mins depending on the network state of the root chain, in this case, Ethereum, while on withdrawal from Nahmii, a [7-day challenge period](../learn/security-model.md) is initiated necessary for fraud-proofing these transactions and state commit.

Here's the link to the [official bridge](https://bridge.nahmii.io), there are a couple of other bridging services that offer a [fast withdrawal](../learn/fast-withdrawals.md), this will be subsequently updated within the bridge address.
