# Beneath the Streets of Blockchain

By Christopher W. Johnson

## Terminology

* The term "Blockchain" is sometimes referred to as synonymous with a decentralized blockchain
* While blockchains are often decentralized, a chain of blocks is also useful in centralized solutions
  * Ironically, when blockchain developers create centralized solutions that interface with blockchain nodes, the centralized solutions are rarely implemented as blockchains

## Trust

* Blockchains are not trustless
* Everyone needs to trust in people and things to do most anything
  * Especially anything involving finance
* While any significant endeavor requires trust, often technical limitations require excessive trust
* Bitcoin liquifies trust, allowing trust to be more flexible
* Increased flexibility enables more optimal configurations of trust
* What people misidentify as "trustless" is actually minimized trust
* Trust can be more liquified than current blockchain technologies allow
  * Blockchain trust management would be more advanced at this point except so many blockchain developers are focused on eradicating trust instead of working with it
* Incomplete liquidity of trust is one of the primary causes of current blockchain scaling problems
* Blockchains need better protocols for managing trust before they can truly scale

## Scaling

### Background

* Like Atlas bearing the world on his shoulders, search engines such as Google bore the weight of the internet to place it in users' hands
* Bitcoin inverted that structure, requiring all Bitcoin nodes and apps to bear the world on their shoulders

### Of Banks and Blockchains

* In terms of scalability, the first three generations of blockchains are more centralized than traditional banks
* Banks only need to maintain ledgers for their customers
* When a bank transfers money to another bank, the first bank does not need to maintain a ledger of what happens to that money in the other bank
* Traditional blockchain nodes need to maintain a ledger for every user of that currency
* Cross-chain solutions mitigate the weight, but they still propogate the core problem

### Volume - A Cautionary Tale

* Bitcoin was the first generation of blockchain
* Ethereum was the second
* The third generation was largely a failure
* After Ethereum's rise, many promising technologies appeared to overcome Ethereum's limitations
* The core problem with Classic Ethereum is that every node needs to track the entire ledger for all of its accounts and currencies
* Most third gen blockchain technologies largely ignored the core problem and attempted to solve surface problems
* The most popular surface problem to tackle was transaction bandwidth
  * First and second gen blockchains have relatively narrow transaction bandwidth
* Third gen blockchains found ways to dramatically increase transaction volume
* But that wasn't the root problem, the root problem is that these blockchains expected all of their nodes and apps to be Google
* Most web apps are composed of roughly 90% reading and 10% writing
* A useful blockchain app can't just write data, it needs to read data and identify connections within that data
* Third gen blockchains did not solve the reading problem, but instead significantly increased the amount of data that needed to be stored and parsed
  * Instead of removing the burden of carrying the world from the shoulders of nodes and apps, they increased the size of the world
  * Part of this misdiagnosis was due to many third gen blockchains working in a world of theory and market bubble investors instead of solving immediate problems for ordinary people
* The focus on throughput instead of foundational scalability resulted in relatively little adoption of third gen blockchains
  * Instead, most blockchain projects fell back to the Ethereum stack
    * This fallback was assisted by the bandaid measure of putting more weight on multiple Ethereum networks

## Meeting Customer Needs

* Most of the world currently operates on relatively centralized solutions
* Blockchain projects have mostly focused on starting with decentralized solutions, and then attemping to bridge the gap to current centralized solutions
  * That is backwards from how most successful technologies are adopted
  * Normally a technology succeeds when it starts where its users are at and then gradually bridges the gap to more revolutionary technologies
  * It's a testament to the viability of blockchains that they have gained as much traction as they have while paddling up a waterfall
* Independent of a fully decentralized solution, Bitcoin and Ethereum are comprised of many useful paradigms and mechanisms that can be incorporated into centralized apps
* Most blockchain app developers write centralized code that incorporate few blockchain paradigms and mechanisms
  * Instead, blockchain apps tend to interface with decentralized nodes and put all of the decentralization weight on them
* There has been a tendency with the initial waves of blockchain pioneers to be excited about blockchains at a high level, without realizing that for a blockchain, the sum is not more valuable than its parts—it is valuable *because* of its parts
  * The invidivual parts of a blockchain each have intrinsic value and utility
* It would be practical for more blockchain projects to take a step back and examine how blockchain principles could be injected into traditional, centralized solutions
  * Currently there are relatively few software libraries to assist such efforts

## Useful Blockchain Technologies

* Here are some Blockchain technologies that are useful for centralized solutions:

### Blockchains in Traditional Databases

* Storing data within a chain of blocks where each block includes the hash of the block before it

### Merkle Trees

* Storing centralized data using [Merkle trees](https://en.wikipedia.org/wiki/Merkle_tree)

### Merkle Proofing

* Creating secondary systems that analyze and validate Merkle trees

### More Prevalent Use of Hashes as Primary Keys

* Some of the benefits of this include:
  * Integral unity between the ID of a record and its contents
  * Increased determinism
    * For example, a client can submit new records and know the primary key of that data without relying on a centralized server to assign arbitrary IDs to that data
    * This enables more idempotent processes

### Consensus

* Dividing a sensitive process across multiple authorities that must reach a minimum degree of agreement for a process to be authorized

### Signing

* Beyond blockchains, signing is used heavily in computer science, particularly network security, yet a surprising number of blockchain app developers are unfamiliar with signing outside of blockchains
  * In particular, [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security) is underutilized in the blockchain app industry
    * Note that TLS is normally associated with [CAs](https://en.wikipedia.org/wiki/Certificate_authority), but can also be useful without a CA

