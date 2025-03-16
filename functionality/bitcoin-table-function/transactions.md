---
icon: subtitles
---

# Transactions

The **bitcoin\_transactions\_rpc** table records Bitcoin blockchain transactions. Each transaction transfers Bitcoin value across the network, to be included in blocks.&#x20;

### **Inputs**

| Args      | Types   | Info                                 |
| --------- | ------- | ------------------------------------ |
| fromBlock | BIGINT  | Block number to start scanning from. |
| toBlock   | BIGINT  | Block number to stop scanning at.    |
| url       | VARCHAR | URL of the Bitcoin node.             |

### **Outputs**

| Column names  | Types      | Info                                                                         |
| ------------- | ---------- | ---------------------------------------------------------------------------- |
| height        | BIGINT     | The block number                                                             |
| txid          | VARCHAR    | The transaction ID                                                           |
| hash          | VARCHAR    | The transaction hash (differs from txid for witness transactions)            |
| size          | BIGINT     | The serialized transaction size                                              |
| vsize         | BIGINT     | The virtual transaction size (differs from size for witness transactions)    |
| weight        | BIGINT     | The transaction's weight (between vsiz&#x65;_&#x34;-3 and vsiz&#x65;_&#x34;) |
| version       | BIGINT     | The version of the transaction                                               |
| locktime      | BIGINT     | The transaction's locktime                                                   |
| vin           | LIST(JSON) | List of transaction inputs (structured as JSON objects)                      |
| vout          | LIST(JSON) | List of transaction outputs (structured as JSON objects)                     |
| blockhash     | VARCHAR    | Hash of the block containing this transaction                                |
| confirmations | BIGINT     | Number of confirmations the transaction has received                         |
| time          | TIMESTAMP  | Timestamp when the transaction was included in a block                       |
