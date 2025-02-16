---
icon: square
---

# Blocks

### Table function

The **eth\_blocks\_rpc** table provides detailed information about Ethereum blockchain blocks. A block comprises hashed transactions added to the blockchain. Each block contains a parent hash reference and a timestamp. The table includes details such as block number, block hash, block size, transaction count, and gas used.

### **Procedure**

To utilize the **eth\_blocks\_rpc** function, follow these steps:

1. **Setup**: Ensure you have access to an EVM node via a reliable RPC URL.&#x20;
2. **Input Parameters**: Define the range of blocks you wish to fetch by specifying `fromBlock` and `toBlock`, both of which should be `BigInt` values. Ensure that `fromBlock` is less than or equal to `toBlock`.
3. **Execution**: Call the function with the specified `fromBlock`, `toBlock`, and `rpc_url` to retrieve data about the blocks within the given range.
4. **Output Analysis**: Analyze the resulting data, which includes details like block hash, number, miner, and other block-specific metrics as outlined in the output table. Use this information to gain insights or perform further analysis on EVM blockchain blocks.

### **Inputs**

| Args      | Types   | Info                                 |
| --------- | ------- | ------------------------------------ |
| fromBlock | BIGINT  | Block number to start scanning from. |
| toBlock   | BIGINT  | Block number to stop scanning at.    |
| url       | VARCHAR | URL of the Ethereum node.            |

### **Outputs**

| Column names     | Types     | Info                                                                                               |
| ---------------- | --------- | -------------------------------------------------------------------------------------------------- |
| hash             | VARCHAR   | Hash of the block. null when its pending block.                                                    |
| number           | BIGINT    | The block number. null when its pending block.                                                     |
| nonce            | VARCHAR   | A block's nonce value, used in the consensus mechanism (may be deprecated in ethereum)             |
| baseFeePerGas    | BIGINT    | Minimum fee per gas unit required for transaction inclusion in this block in the ethereum unit wei |
| parentHash       | VARCHAR   | Hash of the parent block.                                                                          |
| miner            | VARCHAR   | Address of the miner.                                                                              |
| difficulty       | BIGINT    | Measure of how difficult it was to produce this block (deprecated in ethereum)                     |
| totalDifficulty  | VARCHAR   | Total chain difficulty up to this block (deprecated in ethereum)                                   |
| size             | BIGINT    | Integer the size of this block in bytes.                                                           |
| gasLimit         | BIGINT    | The maximum gas allowed in this block.                                                             |
| gasUsed          | BIGINT    | The total used gas by all transactions in this block.                                              |
| timestamp        | TIMESTAMP | The unix timestamp for when the block was collated.                                                |
| sha3Uncles       | VARCHAR   | SHA3 of the uncles data in the block.                                                              |
| logsBloom        | VARCHAR   | The bloom filter for the logs of the block.                                                        |
| transactionsRoot | VARCHAR   | The root of the transaction trie of the block.                                                     |
| stateRoot        | VARCHAR   | The root of the final state trie of the block.                                                     |
| receiptsRoot     | VARCHAR   | The root of the receipts trie of the block.                                                        |
| extraData        | VARCHAR   | Extra data field of this block.                                                                    |

### **Example**

The above example demonstrates how to query Ethereum block data using a specified range of block numbers and an RPC URL. The table output displays various attributes of the Ethereum blocks, such as the block hash, block number, nonce, base fee per gas, parent hash, miner address, difficulty, total difficulty, size, gas limit, gas used, and timestamp. These attributes provide valuable insights into the blockchain's state and activity for the queried range of blocks.

```
D set variable eth_url = 'https://eth-mainnet.g.alchemy.com/v2/{API_KEY}';
D select * from eth_blocks_rpc(21104078, 21104178, getvariable('eth_url')) limit 10;
┌──────────────────────┬──────────┬────────────────────┬───────────────┬──────────────────────┬───┬──────────────────────┬──────────────────────┬──────────────────────┬──────────────────────┐
│         hash         │  number  │       nonce        │ baseFeePerGas │      parentHash      │ … │   transactionsRoot   │      stateRoot       │     receiptsRoot     │      extraData       │
│       varchar        │  int64   │      varchar       │     int64     │       varchar        │   │       varchar        │       varchar        │       varchar        │       varchar        │
├──────────────────────┼──────────┼────────────────────┼───────────────┼──────────────────────┼───┼──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ 0x8e8d1d95a717a152…  │ 21104078 │ 0x0000000000000000 │    3297340313 │ 0x8ba7dba9eac3d806…  │ … │ 0x98ffe7fbb9e7da84…  │ 0x036ed2875c7ade4e…  │ 0x9224bd8c17e68b2e…  │ 0x6265617665726275…  │
│ 0x10fa22bea6d33914…  │ 21104079 │ 0x0000000000000000 │    3555359610 │ 0x8e8d1d95a717a152…  │ … │ 0x632e605059977bb3…  │ 0xd1832baabbb59933…  │ 0x60b0f46515162181…  │ 0x6265617665726275…  │
│ 0xb50d27210ca2fffe…  │ 21104080 │ 0x0000000000000000 │    3637021953 │ 0x10fa22bea6d33914…  │ … │ 0x6e720c4f3315c0eb…  │ 0x39ee1584e77812e5…  │ 0x86db2a09214508b0…  │ 0x6265617665726275…  │
│ 0x30bdeff3c89efcc3…  │ 21104081 │ 0x0000000000000000 │    3582923010 │ 0xb50d27210ca2fffe…  │ … │ 0xa5543ce25287e571…  │ 0x377d8cb2cec4ad81…  │ 0xa29bb89fd3745cbd…  │ 0x546974616e202874…  │
│ 0x14270e8fa4a20c33…  │ 21104082 │ 0x0000000000000000 │    3534801249 │ 0x30bdeff3c89efcc3…  │ … │ 0x74d926608af9b61b…  │ 0x047d1695332602f4…  │ 0x9d1eb7894cd2e2e4…  │ 0x6265617665726275…  │
│ 0xb752240613baa261…  │ 21104083 │ 0x0000000000000000 │    3976594583 │ 0x14270e8fa4a20c33…  │ … │ 0xc56e9743ff3c68c4…  │ 0xbe0ba88e7a0de9ab…  │ 0x386e7ef6805090b9…  │ 0x546974616e202874…  │
│ 0x6510d2b0ff0412eb…  │ 21104084 │ 0x0000000000000000 │    3839128613 │ 0xb752240613baa261…  │ … │ 0x97c11296f913ef30…  │ 0x573dc493cf73e58b…  │ 0x4d768330191ba9d1…  │ 0x6265617665726275…  │
│ 0x60a4777b3f98cd72…  │ 21104085 │ 0x0000000000000000 │    3807939725 │ 0x6510d2b0ff0412eb…  │ … │ 0x381cf492e64c31c6…  │ 0x10f42c75b708790f…  │ 0x58bf2f12a16b49a0…  │ 0x6265617665726275…  │
│ 0xe7d31b62f4e78a66…  │ 21104086 │ 0x0000000000000000 │    3714911250 │ 0x60a4777b3f98cd72…  │ … │ 0x784d408131cb9e82…  │ 0x871e70a6c60de779…  │ 0x0ad6bdd0df668db2…  │ 0x546974616e202874…  │
│ 0xb6c8faa1aef8a35f…  │ 21104087 │ 0x0000000000000000 │    4167739273 │ 0xe7d31b62f4e78a66…  │ … │ 0x58d8c6add121c153…  │ 0x428933a51393551b…  │ 0x0fd86f8489b58474…  │ 0xd883010d0f846765…  │
├──────────────────────┴──────────┴────────────────────┴───────────────┴──────────────────────┴───┴──────────────────────┴──────────────────────┴──────────────────────┴──────────────────────┤
│ 10 rows                                                                                                                                                                18 columns (9 shown) │
└─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```



### Dependent RPC Method

* eth\_getBlockByNumber
