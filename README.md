# CCIP Rebase Token

This is a section of the Cyfrin Advanced Foundry Course.

*[⭐️ Updraft | CCIP Rebase Token](https://updraft.cyfrin.io/courses/advanced-foundry/cross-chain-rebase-token/rebase-token-code-structure)*

# About

This is a rebase token that can be operated across chains using Chainlink's trusted oracle network.

1. A protocol that allows users to deposit into a vault and in return, receive rebase tokens that represent their underlying balance
2. Rebase token -> balanceOf is dynamic to show the changing balance with time
  - balance increases linearly with time
  - mint tokens to our users everytime they perform an action (minting, burning, transferring, or bridging)
3. Interest rate
  - Individually set an interest rate for each user based on some global interest rate of the protocol at the time the user deposits into the vault
  - This global interest rate can only decrease to incentivize/reward early adopters

- [CCIP Rebase Token](#ccip-rebase-token)
- [Getting Started](#getting-started)
  - [Requirements](#requirements)
  - [Quickstart](#quickstart)
- [Usage](#usage)
  - [Deploy](#deploy)
  - [Testing](#testing)
    - [Test Coverage](#test-coverage)
- [Deployment to a testnet or mainnet](#deployment-to-a-testnet-or-mainnet)
- [Deploying to a local anvil chain](#Deploying-to-local-anvil-chain)
  - [Scripts](#scripts)
    - [Withdraw](#withdraw)
  - [Estimate gas](#estimate-gas)


# Getting Started

## Requirements

- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
  - You'll know you did it right if you can run `git --version` and you see a response like `git version x.x.x`
- [foundry](https://getfoundry.sh/)
  - You'll know you did it right if you can run `forge --version` and you see a response like `forge 0.2.0 (816e00b 2023-03-16T00:05:26.396218Z)`


## Quickstart

```
git clone https://github.com/LightPat/foundry-fund-me.git
cd foundry-fund-me
make
```

# Usage

## Deploy

```
forge script script/DeployFundMe.s.sol
```

## Testing

```
forge test
```

or 

```
// Only run test functions matching the specified regex pattern.

"forge test -m testFunctionName" is deprecated. Please use 

forge test --match-test testFunctionName
```

or

```
forge test --fork-url $SEPOLIA_RPC_URL
```

### Test Coverage

```
forge coverage
```

# Deploying to local anvil chain

```
make anvil
make deploy
```

# Deployment to a testnet or mainnet

1. Setup environment variables

You'll want to set your `SEPOLIA_RPC_URL` and `PRIVATE_KEY` as environment variables. You can add them to a `.env` file, similar to what you see in `.env.example`.

- `PRIVATE_KEY`: The private key of your account (like from [metamask](https://metamask.io/)). **NOTE:** FOR DEVELOPMENT, PLEASE USE A KEY THAT DOESN'T HAVE ANY REAL FUNDS ASSOCIATED WITH IT.
  - You can [learn how to export it here](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-Export-an-Account-Private-Key).
- `SEPOLIA_RPC_URL`: This is url of the sepolia testnet node you're working with. You can get setup with one for free from [Alchemy](https://alchemy.com/?a=673c802981)

Optionally, add your `ETHERSCAN_API_KEY` if you want to verify your contract on [Etherscan](https://etherscan.io/).

2. Get testnet ETH

Head over to [faucets.chain.link](https://faucets.chain.link/) and get some testnet ETH. You should see the ETH show up in your metamask.

3. Deploy

```
forge script script/DeployFundMe.s.sol --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY --broadcast --verify --etherscan-api-key $ETHERSCAN_API_KEY
```

## Estimate gas

You can estimate how much gas things cost by running:

```
forge snapshot
```

And you'll see an output file called `.gas-snapshot`