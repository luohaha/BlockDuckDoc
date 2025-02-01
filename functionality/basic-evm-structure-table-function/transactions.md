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

| Column Name      | Type    | Description                                                      |
| ---------------- | ------- | ---------------------------------------------------------------- |
| blockHash        | VARCHAR | Hash of the block containing the log                             |
| blockNumber      | BIGINT  | Number of the block containing the log                           |
| transactionIndex | INTEGER | Transaction's position within the block                          |
| nonce            | INTEGER | The number of transactions made by the sender prior to this one. |
| hash             | VARCHAR | Hash of the transaction                                          |
| from             | VARCHAR | Address of the sender                                            |
| to               | VARCHAR | Address of the receiver (null for contract creation)             |
| value            | VARCHAR | Value transferred in Wei                                         |
| gasPrice         | BIGINT  | Gas price provided by sender in Wei                              |
| gas              | BIGINT  | Gas provided by sender                                           |
| input            | VARCHAR | Data sent along with transaction                                 |

### **Example**

```
D set variable eth_url = 'https://eth-mainnet.g.alchemy.com/v2/{API_KEY}';
D select * from eth_transactions_rpc(21104078, 21104178, getvariable('eth_url')) limit 10;
┌──────────────────────┬─────────────┬──────────────────┬─────────┬──────────────────────┬───┬──────────────────────┬──────────────────┬──────────────┬─────────┬──────────────────────┐
│      blockHash       │ blockNumber │ transactionIndex │  nonce  │         hash         │ … │          to          │      value       │   gasPrice   │   gas   │        input         │
│       varchar        │    int64    │      int32       │  int32  │       varchar        │   │       varchar        │     varchar      │    int64     │  int64  │       varchar        │
├──────────────────────┼─────────────┼──────────────────┼─────────┼──────────────────────┼───┼──────────────────────┼──────────────────┼──────────────┼─────────┼──────────────────────┤
│ 0x8e8d1d95a717a152…  │    21104078 │                0 │ 3768645 │ 0x15b539fdf722615a…  │ … │ 0x1f2f10d1c40777ae…  │ 0x6f             │   3297340313 │  275391 │ 0x2b69abd055069a6b…  │
│ 0x8e8d1d95a717a152…  │    21104078 │                1 │       5 │ 0x1bd4d5006a6b321c…  │ … │ 0x3fc91a3afd70395c…  │ 0x0              │   4297340313 │  294993 │ 0x3593564c00000000…  │
│ 0x8e8d1d95a717a152…  │    21104078 │                2 │ 3768646 │ 0xe391af23df899353…  │ … │ 0x1f2f10d1c40777ae…  │ 0x6f             │ 214535973472 │  258151 │ 0x2b95abd055069a6b…  │
│ 0x8e8d1d95a717a152…  │    21104078 │                3 │   95152 │ 0x5e87d2b87799ada0…  │ … │ 0xd4bc53434c5e12cb…  │ 0x6f             │   3297340313 │  401168 │ 0x2b8e11b815efb8f5…  │
│ 0x8e8d1d95a717a152…  │    21104078 │                4 │  125905 │ 0x72fcf6b7d6c3b2eb…  │ … │ 0xe592427a0aece92d…  │ 0x0              │   4251752228 │ 1000000 │ 0x414bf38900000000…  │
│ 0x8e8d1d95a717a152…  │    21104078 │                5 │   95153 │ 0x50acdb14a98d467e…  │ … │ 0xd4bc53434c5e12cb…  │ 0x6f             │   8355256463 │  712110 │ 0x2b7811b815efb8f5…  │
│ 0x8e8d1d95a717a152…  │    21104078 │                6 │     666 │ 0xfc2a7846d11d9b18…  │ … │ 0x055c48651015cf5b…  │ 0xb1a2bc2ec50000 │  19297340313 │  293433 │ 0x209178e800000000…  │
│ 0x8e8d1d95a717a152…  │    21104078 │                7 │    2138 │ 0x85da072290689a44…  │ … │ 0x7a250d5630b4cf53…  │ 0x0              │  14297340313 │  350764 │ 0x791ac94700000000…  │
│ 0x8e8d1d95a717a152…  │    21104078 │                8 │    1991 │ 0x84ff7a3ec8a749ad…  │ … │ 0x51c72848c68a965f…  │ 0x0              │  16587093877 │  158678 │ 0x122067ed00000000…  │
│ 0x8e8d1d95a717a152…  │    21104078 │                9 │     238 │ 0x584145a3a732e3aa…  │ … │ 0xbd44d27e1f6d8dbe…  │ 0x2c4e85d5b53688 │  80000000000 │   21000 │ 0x                   │
├──────────────────────┴─────────────┴──────────────────┴─────────┴──────────────────────┴───┴──────────────────────┴──────────────────┴──────────────┴─────────┴──────────────────────┤
│ 10 rows                                                                                                                                                        11 columns (10 shown) │
└──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### Dependent RPC Method

* eth\_getBlockByNumber
