---
icon: hive
---

# Supported Blockchains

### EVM-based blockchain

Currently BlockDuck support blockchain:

1. Ethereum.
2. All EVM-based blockchain which support Ethereum's JSON-RPC standard.

\
You will need a reliable RPC node provider, such as QuickNode, Alchemy, Infura, Chainstack, or Tatum. And the RPC node must support the following methods:

```
eth_getBlockByNumber
eth_getLogs
eth_call
eth_blockNumber
trace_block
```

### Bitcoin

Currently BlockDuck support Bitcoin mainnet and testnet. You will need a reliable RPC node provider, such as GetBlock, Chainstack and so on. And the RPC node must support the following methods:

```
getblockhash
getblock
```

### TODO

Todo in the future:

1. Solana.
2. Cosmos.
