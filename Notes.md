# Corda Bootcamp:
### Resources
- [Corda Bootcamp - YouTube Playlist](https://www.youtube.com/playlist?list=PLi1PppB3-YrVq5Qy_RM9Qidq0eh-nL11N)
- [Corda Docs](docs.corda.net)
- [StackOverflow - Corda](stackoverflow.com/questions/tagged/corda)
- [Slack](slack.corda.net)

### What is Corda?
- Corda is a blockchain platform that allows private transactions between legally-identifiable counterparties in an easy-to-use way.
- Corda is for permissioned nodes to communicate on a need-to-know basis about updating shared facts.
- Each node needs to go through a KYC process, with there details posted to a network map service, used by nodes in the network.
- Notary Pools is a set of mutually distrusting nodes that will only sign a transaction if it doesn't represent a double spend attempt. These are used to provide consensus and avoid double-spend. Every transaction needs a signature from a notary node to be valid.
- Nodes provide user-defined flows to allow the user to perform some action in a click. The nodes abstract away messaging, storage, peer discover, data distribution, concurrency, disaster recovery, key management etc. Nodes also provide the functionality to read back data from the ledger.
- Flows describe a sequence of actions for the node. Flow's are essentially methods.

### CorDapp Structure
1. State Class: Represents the token on the ledger
2. Contract Class: Governs the evolution of tokens
3. Flow Class

#### Corda States
- Privacy is the most important part of a business blockchain.
- In corda we share data on a need to know basis
- Each node only sees subset of facts they need to see on the ledger
- In corda these shared facts are called states
- Parties on the network are represented by the Party class
- Shared facts are represented by the ContractState class

##### States API
###### Party Class
```kotlin
class Party(val name: CordaX500Name, owningKey: PublicKey) : AbstractParty(owningKey)
``` 
- `CordaX500Name`: Legal identity of the party
- `PublicKey`: Used to check signatures


###### ContractState Interface
```kotlin
interface ContractState{
    val participants: List<AbstractParty>
}
```
- Any state classes must implement this interface
- `participants`: List of parties on the network that should be notified when the state is changed