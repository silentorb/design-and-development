# A Technical Analysis of Uniswap

## Decentralized Trading

* It is beneficial for Cryptocurrency owners to trade assets
* The natural first candidate for a decentralized exchange was the order book

## EVM Order Book Challenges

* Mainnet Ethereum smart contracts cannot practically support order books
* The challenges with order books have little to do with the amount of data an order book needs to store
  * Smart contract storage is relatively inexpensive (in some ways too inexpensive)
    * Contracts are only charged for the initial writing of data, not the persistence of that data
    * ERC-20 and similar token contracts can store massive amounts of data, but most of that data is deep storage and rarely read or modified
* Smart contract hash map lookups are relatively inexpensive
  * This is the primary read operation of most token contracts, and generally only one or two lookups are performed per contract execution
* A traditional order book doesn't rely on lookups but needs to iterate over many if not all of the orders in the list
  * This volume of read operations gets expensive fast
* Potentially a highly optimized system of indexing ranges of limit orders could be implemented to streamline the processing
  * However such a system would be extremely complex and would still leave the next problem:
* Changes in limit order book state can cause recursive chain reactions where the resolution of one order results in the resolution of other orders
  * This results in undeterministic behavior, something EVM smart contracts do not handle well

## Centralized Exchanges

* Contrary to popular belief, centralization was not the first choice for crypto exhanges
* A decentralized order book was simply not practical
* Due to technical limitations, all initial exchanges were centralized

## The Introduction of AMMs

* AMMs introduced a lighter-weight model of EVM trading
* Instead of directly matching non-fungible trading orders, orders could be integrated through fungible liquidity
* However, while early AMM implementations made decentralized exchanges possible, they were still expensive for mainnet Ethereum and not very practical

## Down to the Metal

* At the time of the first AMMs, mainnet Ethereum was like an impoverished country where gasoline is so expensive that hardly anyone can afford a car
* Uniswap stripped its cars down to go karts that ran on drops of gasoline
* Suddenly, everyone in the country was bopping around in go karts

## Uniswap V1

* Uniswap V1 only needs to track a hash map of asset types to liquidity amounts
  * Which is the same core data structure of an ERC-20 contract, which is what Uniswap V1 uses
* The trading math can be complex but ultimately results in liquidity amounts getting decremented and incremented
* In terms of internal IO, a single Uniswap V1 trade only requires a few lookups and a few writes
* On top of this simplified approach, Uniswap V1 heavily utilizes optimizations that rely on obscure and sometimes accidental EVM performance behavior
  * In other words, optimization hacks

### Gas Benchmarks

| Exchange       | Uniswap | EtherDelta                                                   | Bancor                                                       | Radar Relay (0x)                                             | IDEX                                                         | Airswap                                                      |
| -------------- | ------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ETH to ERC20   | 46,000  | [108,000](https://etherscan.io/tx/0xb0d4330872132a808381bc709069e233c6f69f0bd4c4a4b87e2d40142866a0c7) | [440,000](https://etherscan.io/tx/0x462a3ad9dd05ce18cb33412fde02ee8cfa782d69a9df85be97ac8216a5c8b422) | [113,000](https://etherscan.io/tx/0xe2ca9f47926e2b262cf9b060f735c5ebfda1a4edd55af236d95b274c75be5449)* | [143,000](https://etherscan.io/tx/0xe2ca9f47926e2b262cf9b060f735c5ebfda1a4edd55af236d95b274c75be5449) | [90,000](https://etherscan.io/tx/0xccc10f160bde7779a35cda22f5d67532d0a4beaf76c9296f3d645ff1edf424ec) |
| ERC20 to ETH   | 60,000  | [93,000](https://etherscan.io/tx/0xc06aeb2b6794271c978b2d41b16ba0e75f80f55ab9160b21212d0d4eb918f6e1) | [403,000](https://etherscan.io/tx/0x550961cbe81995c2300550b75654c75fb112fa5ba4a20ab7af1c02ed218af8e1) | [113,000](https://etherscan.io/tx/0xe2ca9f47926e2b262cf9b060f735c5ebfda1a4edd55af236d95b274c75be5449)* | [143,000](https://etherscan.io/tx/0xe2ca9f47926e2b262cf9b060f735c5ebfda1a4edd55af236d95b274c75be5449) | [120,000](https://etherscan.io/tx/0xf4576e9cd6a598b50e8dec2c248049fa5cdc40d5994d185da70447d671094734)* |
| ERC20 to ERC20 | 88,000  | no                                                           | [538,000](https://etherscan.io/tx/0x4f0595d122a2202022960d8c89773de206f4e4ab4da26336b68f1993691334b2) | [113,000](https://etherscan.io/tx/0xe2ca9f47926e2b262cf9b060f735c5ebfda1a4edd55af236d95b274c75be5449) | no                                                           | no                                                           |
| *wrapped ETH   |         |                                                              |                                                              |                                                              |                                                              |                                                              |

* https://hackmd.io/@HaydenAdams/HJ9jLsfTz?type=view#Gas-Benchmarks

## Uniswap V2

* Uniswap V2 added many improvements while staying within the core performance constraints of V1

## Uniswap V1 and V2 Limitations

* The downside to Uniswap V1 and V2 is they strip away so much information that they can only ever support broad-stroke financial operations
* Advanced business logic requires management of more granular information, a thing order books support but Uniswap V1 and V2 can't
* Along with its simplified model, Uniswap V1/V2's reliance on optimization hacks further restricts what business logic they can support

## Uniswap V3

* Uniswap V3 introduced a hybrid model of fungible and non-fungible data
* Liquidity positions are now stored as non-fungible records instead of fungible ERC-20 data
* Trading is still applied through fungible operations
* To integrate trades, Uniswap V3 translates non-fungible positions to fungible pools, then performs certain fungible operations, then converts the results back to non-fungible records
* The process is similar to linear algebra where some 3D math problems are solved by translating to a 2D space, performing 2D operations, and then converting back to 3D space
* The application of such a process extends far beyond AMMs and could become the cornerstone of most blockchain platforms

## Layer 2 Uniswap

* Since Uniswap V3 uses non-fungible records and has additional heavy features, it can not maintain the light-weight profile of Uniswap V1 and V2
* Uniswap V3 is not a mainnet Ethereum solution and instead relies on Layer 2 processing
* Layer 2 solutions were around years before Uniswap V3, but they had only recently matured to the point of being practical
* Even though Uniswap V3 is too heavy to practically run on mainnet Ethereum, due to fungible integration it is still more deterministic and efficient than an order book