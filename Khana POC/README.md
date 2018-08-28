# Khana: Proof of Concept

This repo is the Proof of Concept, completed as part of the final project for Consensys Academy 2018.

_Note: I'm not a web developer so this is the first time i've used React, forgive the messy front-end code._

### What is Khana?
Khana is a framework for tokenized community building. It is a framework to incentivise the growth of a community, from communities which are just starting out, to large mature communities. This is not exclusive to online communities.

### How does it work?
##### Community members
Community members can be rewarded, awarded, and incentivised to contribute to the community.
* Rewarded tokens for contributing or participating at community events
* Awarded tokens for completing 'bounties' that the community leaders need completed to help grow the community
* Incentivised with tokens to regularly contribute to the community

##### Community leaders
The community leaders (i.e. admins) 'mint' the tokens and give them to community members. Each 'minting' has an associated reason for minting (e.g. volunteered at Friday's event), which is recorded permanently to IPFS. The IPFS hash of the file is recorded permanently on the Ethereum blockchain via logged events. This serves as an audit trail and ensures responsible minting by community leaders, as anyone can read the audit trail at any time.

##### Value of the token
The economic value of the token comes from ETH stored in a funds contract (BondingCurveFunds.sol), which allows community members to trade in the tokens they have for ETH. The calculation for the ETH returned is based on a simple bonding curve formula which allows liquidity for all community members. This results in the 'token value' being captured by the amount of ETH in the funds contract. If many community members liquidate their tokens and reduce the ETH funds, then the 'token value' is reduced, indicating the economic value of the community, as perceived by the community.

Where does the ETH come from? This should come from activity of the community. For example, a portion of ticket sales, sponsorships, or donations could be directly sent to the funds contract.

There is also the non-economic value of the token, which can be acknowledged by the community in various ways. E.g. community token leaderboards, invites to exclusive events for community members with tokens above a certain threshold, trading tokens for services of the community, etc.

##### The effect of the funds contract
One of the problems when building a community is how to incentivise participation and contributions from community members. With Khana, community members are incentivised by the token, which will increase in economic value if the activities of the community grows. If life gets in the way and a community member can no longer contribute, they still retain their tokens and can receive some of the future value if they trade their tokens into the bonding curve.
Due to the new minting of tokens, we create an 'inflation penalty' or tax for non-active members. For example, an early contributor may hold a large portion of the token supply early on, but if they are in-active, then their portion of the supply will reduce as more tokens are minted. This results in a dynamic which fairly rewards early contributors and at the same time, rewards new contributors with the expanding supply.
A basic simulation of token dynamics can be found here: https://goo.gl/jeJkV5

## How to setup
Requirements:
* node
* ganache-cli
* truffle
* metamask

**Steps**
1. Run ganache: `ganache-cli`
    * take note of the accounts and private keys (especially the first one)
2. In a new terminal window
    * go to the project directory
    * open truffle console: `truffle console`
    * compile contracts: `compile`
    * migrate contracts onto ganache: `migrate`
3. In another terminal window: `npm run start`
4. Open the metamask plugin and select the relevant private network (the one on port 8545). This will connect your metamask with your ganache instance. If you don't see it there, then add a Custom RPC with URL `127.0.01:8545`
5. Once you've connected, make sure you add the ganache accounts to metamask by importing the private keys. The first account listed in ganache is the default owner and admin.

## Running tests
Navigate to the project directory and in terminal: `truffle test`