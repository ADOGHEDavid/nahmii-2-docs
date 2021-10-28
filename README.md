# Getting started with the Nahmii 2.0 testnet

## About Nahmii 2.0

Nahmii 2.0 is a layer 2 scaling solution for Ethereum built around the Nahmii Virtual Machine, NVM. This upgraded version of Nahmii provides generalised smart contract support and full composability between them. Nahmii leverages patent-pending state pool technology which gives unprecedented scalability. This makes Nahmii the only commercially viable scaling solution for Ethereum.

## Connecting to the Nahmii 2.0 testnet

The current testnet iteration of Nahmii 2.0 works with both the Ropsten public testnet and an L2 network. It is thus required to connect to two RPC networks.

### Network details

L1 testnet
- Network name: Nahmii 2.0 L1 testnet
- RPC URL: https://l1.testnet.nahmii.io/ (or any other node on the Ropsten public testnet)
- ChainID: 3
- Symbol: ETH
- Block explorer URL: https://ropsten.etherscan.io

L2 testnet
- Network name: Nahmii 2.0 L2 testnet
- RPC URL: https://l2.testnet.nahmii.io/
- ChainID: 5553
- Symbol: ETH
- Block explorer URL: https://explorer.testnet.nahmii.io

### Connect with the press of a button

Navigate to the [connect-nahmii-2](https://nahmii-community.github.io/connect-nahmii-2/) web app and press on the `ADD NAHMII L1` and `ADD NAHMII L2` buttons. The app will request you to add both networks. Approve the requests. The networks should be added to your Ethereum provider.

### Connect manually via MetaMask

1. Open the MetaMask browser extension.
2. Click on the network name.
3. When the networks window pops up, click on 'Custom RPC'.
4. A new window will popup where you can fill in the connection details. Fill in the details provided above for the first network and click save.
5. Do this again for the second network listed above.

## Nahmii 2.0 Meta contracts L1 <-> L2

Nahmii 2.0 provides a number of contracts on L1 to interact with the L2 and vica versa. The meta data of these contracts can be found [here](https://meta.testnet.nahmii.io/addresses.json).

The main contract that is relevant for developers is the AddressManager. The AddressManager provides easy access to all the other contracts and exposes their addresses. For examples on how to interact with the Nahmii 2.0 L2 contracts, please see the provided examples.

## Configuring a project to run on Nahmii 2.0

To compile the correct bytecode to work with the Nahmii virtual machine, the hardhat-nvm dependency is required due to the differences between certain opcodes in the EVM and the NVM.

1. Install the NVM hardhat plugin.

```js
yarn add @nahmii/hardhat-nvm
```

2. Edit `hardhat.config.js` to use the NVM package.

```js
// hardhat.config.js
require("@nomiclabs/hardhat-waffle");
require('@nahmii/hardhat-nvm');

...
```

3. In the same file, add `nahmii` to the list of networks:

```js
...

module.exports = {
  solidity: "0.7.6",
  networks: {
    nahmii: {
      url: 'https://l2.testnet.nahmii.io/',
      accounts: { mnemonic: 'test test test test test test test test test test test junk' },
      gasPrice: 15000000,
      nvm: true
    }
  }
};
```
---

**Note**

In order for an account to deploy smart contracts to the Nahmii testnet its address has to be whitelisted. Please reach out to us at [support@nahmii.io](mailto:support@nahmii.io), on [Telegram](https://t.me/nahmii) or [Discord](https://discord.com/invite/GKTsUTH) to request whitelisting of your provided address

---

4. To test contracts on the live Nahmii L2, compile it with hardhat:

```
npx hardhat --network nahmii test
```

5. To interact with the smart contracts manually, use the console. The JavaScript console can be ran with the following command:

```
npx hardhat --network nahmii console
```
