# NFTEarth and NFTFi 

## Overview 

This repository aims to serve as the base level of building NFTFi tooling and integrations/applications for supporting all DeFi protocols - from small to large - to on-board into Layer2 ecosystems and into NFTFinance (NFTFi) use-cases. The market is new and there is currently not a single protocol serving these unmet needs. NFTEarth aims to be the first, or one of the leaders in NFTFi practical applications by using the Yearn V3 tokenized strategies as the foundational starting point - this will allow for using DeFi tokens to obtain loans and earn extra yield - composability enabled through NFT collateralization. Below is forked from Yearn's tokenized strategy repo. Checkout ERC-4626 details from [Ethereum](https://ethereum.org/en/developers/docs/standards/tokens/erc-4626/) to learn about the implications and possibilities here.

![image](https://user-images.githubusercontent.com/29180454/236651201-88e11a90-882b-49de-9edf-f40d19090300.png) - view the NFTEarth Whitepaper for more thorough background and use cases specific to NFTEarth and the NFT functionality.


# Yearn Tokenized Strategy

This repository contains the base code for the Yearn V3 tokenized strategy implementation. The V3 strategy implementation utilizes an immutable proxy pattern to allow anyome to easily create their own single strategy vaults that will all use the same logic held within the `TokenizedStrategy` for their redundant and high risk code. The implementation holds all ERC-20, ERC-4626, profit locking and reporting functionility to make any strategy that uses it a fully permisionless vault without holding any of this logic itself. 

NOTE: The implementation address that calls are delegated to is pre-set to a constant and can never be changed post deployment. The implementation contract itself is ownerless and can never be updated in any way.

A `Strategy` contract can become a fully ERC-4626 compliant vault by inheriting the `BaseTokenizedStrategy` contract that uses the fallback function to delegateCall a previously deployed version of `TokenizedStrategy`. A strategist then only needs to override three simple functions in their specific strategy.

[TokenizedStrategy](https://github.com/yearn/tokenized-strategy/blob/master/src/TokenizedStrategy.sol) - The implementation contract that holds all logic for every strategy.

[BaseTokenizedStrategy](https://github.com/yearn/tokenized-strategy/blob/master/src/BaseTokenizedStrategy.sol) - Abstract contract to inherit that communicates with the `TokenizedStrategy`.

Full tech spech can be found [here](https://hackmd.io/@D4Z1faeARKedWmEygMxDBA/H1WtpMTCs)

## Installation and Setup

1. First you will need to install [Foundry](https://book.getfoundry.sh/getting-started/installation).
NOTE: If you are on a windows machine it is recommended to use [WSL](https://learn.microsoft.com/en-us/windows/wsl/install)

2. Fork this repository (easier) or create a new repository using it as template. [Create from template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)

3. Clone your newly created repository recursively to include modules.

```sh
git clone --recursive https://github.com/myuser/tokenized-strategy

cd tokenized-strategy
```

NOTE: if you create from template you may need to run the following command to fetch the git submodules (.gitmodules for exact releases) `git submodule init && git submodule update`

4. Build the project.

```sh
make build
```
To print the size of each contract
```sh
make size
```

5. Run tests
```sh
make test
```

## Testing

Run all tests run on a local chain

```sh
make test
```
Run all tests with traces (very useful)

```sh
make trace
```
Run all tests with gas outputs

```sh
make gas
```
Run specific test contract with traces (e.g. `test/StrategyOperation.t.sol`)

```sh
make trace-contract contract=StrategyOperationsTest
```
Run specific test with traces (e.g. `test/StrategyOperation.t.sol::testStrategy`)

```sh
make trace-test test=testStrategy
```

See here for some tips on testing [`Testing Tips`](https://book.getfoundry.sh/forge/tests.html)

## Storage Layout

To print out the storage layout of any contract (e.g 'test/MockStrategy.sol')

```sh
make inspect contract=MockStrategy
```

# Resources

- [Getting help on Foundry](https://github.com/gakonst/foundry#getting-help)
- [Forge Standard Lib](https://github.com/brockelmore/forge-std)
- [Awesome Foundry](https://github.com/crisgarner/awesome-foundry)
- [Foundry Book](https://book.getfoundry.sh/)
- [Learn Foundry Tutorial](https://www.youtube.com/watch?v=Rp_V7bYiTCM)
