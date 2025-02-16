---
icon: subtitles
---

# Transactions

### Table function

The **eth\_transaction\_rpc** table logs all transactions on the Ethereum blockchain. Each entry details a single transaction, providing information such as block number, hash, timestamp, sender, recipient, value, gas, gas price, and more. Transactions are the core operations on the Ethereum blockchain, initiated by users to transfer value, deploy smart contracts, or interact with.

### **Procedure**

To utilize the **eth\_transactions\_rpc** function, follow these steps:

1. Identify the range of blocks you want to scan by determining the `fromBlock` and `toBlock` parameters.
2. Obtain the RPC URL of your Ethereum node, which will be used to connect and interact with the blockchain.
3. Call the **eth\_transactions\_rpc** function in your application or script, providing the necessary inputs: `fromBlock`, `toBlock`, and `rpc_url`.
4. Review the output, which will include detailed transaction data from the specified block range.
5. Use this data to analyze transactions, monitor activity, or assist in any other blockchain-related operations as needed.

### **Inputs**

| Args      | Types   | Info                                 |
| --------- | ------- | ------------------------------------ |
| fromBlock | BIGINT  | Block number to start scanning from. |
| toBlock   | BIGINT  | Block number to stop scanning at.    |
| url       | VARCHAR | URL of the Ethereum node.            |

### **Outputs**

| Column Name          | Type    | Description                                                        |
| -------------------- | ------- | ------------------------------------------------------------------ |
| blockHash            | VARCHAR | Hash of the block containing the log                               |
| blockNumber          | BIGINT  | Number of the block containing the log                             |
| transactionIndex     | INTEGER | Transaction's position within the block                            |
| nonce                | INTEGER | The number of transactions made by the sender prior to this one.   |
| hash                 | VARCHAR | Hash of the transaction                                            |
| from                 | VARCHAR | Address of the sender                                              |
| to                   | VARCHAR | Address of the receiver (null for contract creation)               |
| value                | VARCHAR | Value transferred in Wei                                           |
| gasPrice             | BIGINT  | Gas price provided by sender in Wei                                |
| gas                  | BIGINT  | Gas provided by sender                                             |
| input                | VARCHAR | Data sent along with transaction                                   |
| maxFeePerGas         | BIGINT  | Total fee that covers both base and priority fees                  |
| maxPriorityFeePerGas | BIGINT  | Fee given to miners to incentivize them to include the transaction |
| type                 | VARCHAR | Type of the transaction                                            |

### **Example**

```
D set variable eth_url = 'https://eth-mainnet.g.alchemy.com/v2/{API_KEY}';
D select * from eth_transactions_rpc(21104078, 21104178, getvariable('eth_url')) limit 10;
┌──────────────────────┬─────────────┬──────────────────┬─────────┬──────────────────────┬──────────────────────┬───┬─────────┬──────────────────────┬──────────────┬──────────────────────┬─────────┐
│      blockHash       │ blockNumber │ transactionIndex │  nonce  │         hash         │         from         │ … │   gas   │        input         │ maxFeePerGas │ maxPriorityFeePerGas │  type   │
│       varchar        │    int64    │      int32       │  int32  │       varchar        │       varchar        │   │  int64  │       varchar        │    int64     │        int64         │ varchar │
├──────────────────────┼─────────────┼──────────────────┼─────────┼──────────────────────┼──────────────────────┼───┼─────────┼──────────────────────┼──────────────┼──────────────────────┼─────────┤
│ 0x8e8d1d95a717a152…  │    21104078 │                0 │ 3768645 │ 0x15b539fdf722615a…  │ 0xae2fc483527b8ef9…  │ … │  275391 │ 0x2b69abd055069a6b…  │   3297340313 │                    0 │ 0x2     │
│ 0x8e8d1d95a717a152…  │    21104078 │                1 │       5 │ 0x1bd4d5006a6b321c…  │ 0x08903a3be1e0c263…  │ … │  294993 │ 0x3593564c00000000…  │   4894983245 │           1000000000 │ 0x2     │
│ 0x8e8d1d95a717a152…  │    21104078 │                2 │ 3768646 │ 0xe391af23df899353…  │ 0xae2fc483527b8ef9…  │ … │  258151 │ 0x2b95abd055069a6b…  │ 214535973472 │         214535973472 │ 0x2     │
│ 0x8e8d1d95a717a152…  │    21104078 │                3 │   95152 │ 0x5e87d2b87799ada0…  │ 0xd1fa51f2db23a9fa…  │ … │  401168 │ 0x2b8e11b815efb8f5…  │   3297340313 │                    0 │ 0x2     │
│ 0x8e8d1d95a717a152…  │    21104078 │                4 │  125905 │ 0x72fcf6b7d6c3b2eb…  │ 0xfe0c760cbcb9da23…  │ … │ 1000000 │ 0x414bf38900000000…  │   4251752228 │           4251752228 │ 0x2     │
│ 0x8e8d1d95a717a152…  │    21104078 │                5 │   95153 │ 0x50acdb14a98d467e…  │ 0xd1fa51f2db23a9fa…  │ … │  712110 │ 0x2b7811b815efb8f5…  │   8355256463 │           8355256463 │ 0x2     │
│ 0x8e8d1d95a717a152…  │    21104078 │                6 │     666 │ 0xfc2a7846d11d9b18…  │ 0x428f1470b591aceb…  │ … │  293433 │ 0x209178e800000000…  │  20424716834 │          16000000000 │ 0x2     │
│ 0x8e8d1d95a717a152…  │    21104078 │                7 │    2138 │ 0x85da072290689a44…  │ 0xa8c9d1b57a6ac71a…  │ … │  350764 │ 0x791ac94700000000…  │ 100000000000 │          11000000000 │ 0x2     │
│ 0x8e8d1d95a717a152…  │    21104078 │                8 │    1991 │ 0x84ff7a3ec8a749ad…  │ 0xa172577031eafd8b…  │ … │  158678 │ 0x122067ed00000000…  │  16587093877 │          16587093877 │ 0x2     │
│ 0x8e8d1d95a717a152…  │    21104078 │                9 │     238 │ 0x584145a3a732e3aa…  │ 0xbe567e69885784a0…  │ … │   21000 │ 0x                   │         NULL │                 NULL │ 0x0     │
├──────────────────────┴─────────────┴──────────────────┴─────────┴──────────────────────┴──────────────────────┴───┴─────────┴──────────────────────┴──────────────┴──────────────────────┴─────────┤
│ 10 rows                                                                                                                                                                      14 columns (11 shown) │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### Dependent RPC Method

* eth\_getBlockByNumber
