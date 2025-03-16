---
icon: square
---

# Blocks

The **bitcoin\_blocks\_rpc** table provides detailed information about Bitcoin blockchain blocks. A block is a collection of transactions, and is identified by a block hash. Each block contains a reference to the previous block, forming a chain of blocks.&#x20;

### **Inputs**

| Args      | Types   | Info                                 |
| --------- | ------- | ------------------------------------ |
| fromBlock | BIGINT  | Block number to start scanning from. |
| toBlock   | BIGINT  | Block number to stop scanning at.    |
| url       | VARCHAR | URL of the Bitcoin node.             |

### **Outputs**

| Column names      | Types         | Info                                                                            |
| ----------------- | ------------- | ------------------------------------------------------------------------------- |
| bits              | VARCHAR       | The value of the nBits field in the block header                                |
| chainwork         | VARCHAR       | Expected number of hashes required to produce the chain up to this block        |
| confirmations     | BIGINT        | The number of confirmations (blocks in the longest chain linking to this block) |
| difficulty        | DOUBLE        | Proof-of-work difficulty as a multiple of the minimum difficulty                |
| hash              | VARCHAR       | The block hash                                                                  |
| height            | BIGINT        | The block number                                                                |
| mediantime        | TIMESTAMP     | The median time of the block                                                    |
| merkleroot        | VARCHAR       | The Merkle root of the block                                                    |
| nTx               | BIGINT        | Number of transactions in the block                                             |
| nextblockhash     | VARCHAR       | Hash of the next block                                                          |
| nonce             | BIGINT        | The nonce value                                                                 |
| previousblockhash | VARCHAR       | Hash of the previous block                                                      |
| size              | BIGINT        | Total size of the block                                                         |
| strippedsize      | BIGINT        | Size of the block without witness data                                          |
| time              | TIMESTAMP     | Timestamp when the block was mined                                              |
| tx                | LIST(VARCHAR) | List of transaction IDs in the block                                            |
| version           | BIGINT        | The block version                                                               |
| weight            | BIGINT        | The block weight (SegWit metric)                                                |

