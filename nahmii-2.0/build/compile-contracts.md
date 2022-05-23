---
description: >-
  Nahmii and Optimism share certain similarities due to the forking of the OVM,
  hence inherited a lot of their architecture.
---

# compile-contracts

Nahmii is meant to feel and behave like Ethereum, but faster and cheaper. For developers building on Nahmii, we aim to make transitioning very fluid and seamless. Existing Solidity smart contracts can run on L2 just like they run on L1, with a few exceptions.

Similarly, off-chain code (i.e., UIs and wallets), should be able to interact with L2 contract with an updated RPC endpoint.

### Opcode Support

A subset of smart contract opcodes isn't supported in Nahmii due to the security mechanisms built into the Nahmii Virtual Machine (NVM).

Now, as most smart contracts are written in the Solidity programming language, this is usually manageable. Compliant bytecode is generated as output using [Optimism's modified Solidity compiler](https://github.com/ethereum-optimism/solc-bin) to compile smart contracts. The bytecode contains replacements for most unsupported EVM opcodes.

The compilation with a modified compiler is facilitated by a HardHat plugin [@nahmii/hardhat-nvm](https://www.npmjs.com/package/@nahmii/hardhat-nvm).

Below is the set of opcodes disallowed in contract bytecode deployed to the Nahmii L2:

* `ADDRESS`
* `BALANCE`
* `BLOCKHASH`
* `CALLCODE`
* `CALLER`\*
* `CALL`\*
* `CHAINID`
* `COINBASE`
* `CREATE2`
* `CREATE`
* `DELEGATECALL`
* `DIFFICULTY`
* `EXTCODECOPY`
* `EXTCODEHASH`
* `EXTCODESIZE`
* `GASLIMIT`
* `GASPRICE`
* `NUMBER`
* `ORIGIN`
* `REVERT`\*
* `SELFBALANCE`
* `SELFDESTRUCT`
* `SLOAD`
* `SSTORE`
* `STATICCALL`
* `TIMESTAMP`

\* The `CALLER`, `CALL`, and `REVERT` opcodes are also disallowed, except in the special case that they appear as part of one of the following strings of bytecode:

1. `CALLER PUSH1 0x00 SWAP1 GAS CALL PC PUSH1 0x0E ADD JUMPI RETURNDATASIZE PUSH1 0x00 DUP1 RETURNDATACOPY RETURNDATASIZE PUSH1 0x00 REVERT JUMPDEST RETURNDATASIZE PUSH1 0x01 EQ ISZERO PC PUSH1 0x0a ADD JUMPI PUSH1 0x01 PUSH1 0x00 RETURN JUMPDEST`
2. `CALLER POP PUSH1 0x00 PUSH1 0x04 GAS CALL`

Opcodes which are not yet assigned in the EVM are also disallowed.
