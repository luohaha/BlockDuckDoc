---
icon: file-signature
---

# Customized EVM contact table function

BlockDuck offer you customized contract table function, which are used to analyze events and states of specific EVM contracts, and needs to be created on-demand using the pragma directive.

It's essential to identify the key events and states you want to track. This might include:

* **Contract Events**: Specify events in your Solidity code that reflect important actions or changes in state within your contract.
* **Contract view functions**: Contract view functions are special functions in Solidity that allow you to retrieve information from the blockchain without making any changes to the state. These functions are marked with the `view` keyword and can safely be called without incurring any gas costs, as they do not modify the contract's storage or the blockchain state. View functions are ideal for reading data or calculating results based on the contract's current state.

