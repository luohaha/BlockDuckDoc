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

### Examples

```
D set variable bitcoin_url = 'https://bitcoin-mainnet.core.chainstack.com/xxx';
D select * from bitcoin_transactions_rpc(886654, 886654, getvariable('bitcoin_url')) where hash = '4bc9f4fbd1f3aea067c637daaa2f743e8bcdf7859688fc556964bdf67468c82a';
┌────────┬──────────────────────┬──────────────────────┬───────┬───────┬────────┬─────────┬──────────┬──────────────────────┬──────────────────────┬───────────────────────────┬───────────────┬─────────────────────┐
│ height │         txid         │         hash         │ size  │ vsize │ weight │ version │ locktime │         vin          │         vout         │         blockhash         │ confirmations │        time         │
│ int64  │       varchar        │       varchar        │ int64 │ int64 │ int64  │  int64  │  int64   │        json[]        │        json[]        │          varchar          │     int64     │      timestamp      │
├────────┼──────────────────────┼──────────────────────┼───────┼───────┼────────┼─────────┼──────────┼──────────────────────┼──────────────────────┼───────────────────────────┼───────────────┼─────────────────────┤
│ 886654 │ f397dd542f4f1dd0e7…  │ 4bc9f4fbd1f3aea067…  │  377  │  350  │  1400  │    2    │    0     │ [{"coinbase":"037e…  │ [{"n":0,"scriptPub…  │ 0000000000000000000132d…  │     1689      │ 2025-03-07 00:02:24 │
└────────┴──────────────────────┴──────────────────────┴───────┴───────┴────────┴─────────┴──────────┴──────────────────────┴──────────────────────┴───────────────────────────┴───────────────┴─────────────────────┘
```
