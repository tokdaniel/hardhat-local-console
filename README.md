# Superfluid Local Console

The Superfluid Developer Console is a great resource when building any Superfluid related project. You can find the hosted version here when working on any live testnet or main network: https://console.superfluid.finance.

However, it's much easier to tinker with new projects locally. This repo will help you run the console locally so that you can make this happen!

## Steps to Run The Console Locally
1. Open the example-project folder in your terminal and run `npm install` then `npx hardhat node --hostname 0.0.0.0` (do this in a separate terminal window)
2. Inside of the example-project folder, run `yarn hardhat run scripts/runDeployContractsAndToken.js --network localhost`. This will deploy the framework to your local env. You should see logs at this point
3. Next, cd into the `subgraph` folder run `yarn` then `yarn prepare-local`. Make sure you have docker available on your machine for step 4. 
4.  Inside of that same folder, run `docker-compose up`. At this stage, you should be able to see some logs in the node terminal window web3_client, etc.
5. finally run: `yarn build-and-deploy-local` inside of the subgraph folder, this will deploy the subgraph and if the previous step went fine then querying `{events {id }}` at your local subgraph endpoint should yield some entities
6. Start up the console locally by running `yarn` then `yarn dev` in the `console` folder
7. Create a stream in the example project folder to test it out by running the `wrapTokens` and `createFlow` scripts and specifying `--network localhost` like this: `npx hardhat run scripts/wrapTokens.js --network localhost` and `npx hardhat run scripts/createFlow.js --network localhost`

You’re up and running! Now you can use the console locally with your other work!

### IF YOU MAKE A MISTAKE

Here’s how to troubleshoot if you make a mistake somewhere in this process and need to re start

1) Kill everything: shut down your hardhat node and your docker container running the subgraph

2) Delete the automatically generated `data` folder inside of the subgraph folder of the ethereum-contracts package. This is caching data from previous networks & deployments

### IF YOU RUN INTO ISSUES

For example:
- the subgraph isn’t indexing data, or the data it is indexing is old
- or your node is quitting immediately after booting up

Possible remedies: 
- Try deleting the automatically generated `data` folder inside of the subgraph folder of the ethereum-contracts package, then try again.
- You may also need to ensure that you don’t have other proccesses running on port 5432 or port 5001 - your container needs these for running IPFS and Postgres on your machine as a part of the subgraph node

If you have any questions, don't hesitate to reach out in the Superfluid Discord's #dev-support channel: https://discord.superfluid.finance