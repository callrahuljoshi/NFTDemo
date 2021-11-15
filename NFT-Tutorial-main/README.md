# NFT-Tutorial
Deploy an NFT project on Ethereum

This Tutorial assumes you have installed nodejs and npm

## Pre requisites
1.  Install Metamask
2.  Some ethers in rinkbey faucet (Have it by tagging rinkbey on twitter and get things)
3.  Alchemy account for blockchain node provider and create an app there

![image](https://user-images.githubusercontent.com/4149775/141731821-5bc7f36b-4aba-4e20-bde8-3c6c2bed3072.png)


## Start Hardhat Project

Create a new directory and install hardhat
```
mkdir NftDemoFinal
cd NftDemoFinal
npm install --save-dev hardhat
```

I recommend reviewing the [hardhat documentation and tutorial](https://hardhat.org).

Next, start a hardhat project

```
npx hardhat NFT-Tutorial-main
```

Select "Create a sample hardhat project". You can say yes to everything.

Now you have a hardhat project ready to go!

## Write NFT Contract Code

First, install Open Zeppelin contracts

```
npm install @openzeppelin/contracts
```

You can delete Greeter.sol.

In the contracts folder, create a new solidity file called NFTee.sol and add the code from the [sample NFTee.sol contract](https://github.com/callrahuljoshi/NFTDemo/blob/main/NFT-Tutorial-main/contracts/NFTee.sol) in this repo.

Try customizing the solidity code with the name of your NFT.

## Compile the contract

To compile the contract, just go

```
npx hardhat compile
```

## Configuring Deployment

We are going to deploy the NFT contract on the Rinkeby Testnet.

First, make sure you get some rinkeby testnet Ether.  You can get some here: https://faucet.rinkeby.io/

![image](https://user-images.githubusercontent.com/4149775/141732171-13bf57f5-65ed-4452-92fe-199909b77aa0.png)


Next, set up a rinkeby provider. You can get one from alchemyapi.io
It should look like: https://eth-rinkeby.alchemyapi.io/v2/......

![image](https://user-images.githubusercontent.com/4149775/141732232-d5702efb-6efc-429e-8a06-e23ef978b36b.png)

Next, configure module.exports in hardhat.config.js

```
defaultNetwork: "rinkeby",
networks: {
  hardhat: {
  },
  rinkeby: {
    url: "",
    accounts: [""]
  }
},
solidity: {
  version: "0.8.0"
},
paths: {
  sources: "./contracts",
  tests: "./test",
  cache: "./cache",
  artifacts: "./artifacts"
},
mocha: {
  timeout: 20000
}
```

You must add your own account private key and provider url to the config

## Deploy Contract

First, you must write a deploy script. Go to deploy.js in the scripts folder.

Inside function main(), add the code to deploy your contract similar to [deploy.js](https://github.com/BlockDevsUnited/NFT-Tutorial/blob/main/scripts/deploy.js) in this repo

```
async function main() {
  // We get the contract to deploy
  const GameItem = await ethers.getContractFactory("GameItem");
  const gameItem = await GameItem.deploy();
}
```

If everything is configured properly, you can now deploy. In your terminal, run the deploy command

```
npx hardhat run --network rinkeby scripts/deploy.js
```

To see if your contract has been deployed, check your account in etherscan.io. A new transaction should appear, and the transaction should deploy a new contract!

## Verify on Etherscan

To verify your contract on etherscan, you must first flatten your entire contract.

```
npx hardhat flatten
```

Take the code, and clean it up, then verify it on etherscan.

## Play with your new NFT contract

   - Mint token
   - Transfer Token


## View your NFT on OpenSea

- get a metadata link
- Upload to Opensea
- view on opensea
