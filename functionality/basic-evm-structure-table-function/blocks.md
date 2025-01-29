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

| Column names    | Types     | Info                                                                                               |
| --------------- | --------- | -------------------------------------------------------------------------------------------------- |
| hash            | VARCHAR   | Hash of the block. null when its pending block.                                                    |
| number          | BIGINT    | The block number. null when its pending block.                                                     |
| nonce           | VARCHAR   | A block's nonce value, used in the consensus mechanism (may be deprecated in ethereum)             |
| baseFeePerGas   | BIGINT    | Minimum fee per gas unit required for transaction inclusion in this block in the ethereum unit wei |
| parentHash      | VARCHAR   | Hash of the parent block.                                                                          |
| miner           | VARCHAR   | Address of the miner.                                                                              |
| difficulty      | BIGINT    | Measure of how difficult it was to produce this block (deprecated in ethereum)                     |
| totalDifficulty | VARCHAR   | Total chain difficulty up to this block (deprecated in ethereum)                                   |
| size            | BIGINT    | Integer the size of this block in bytes.                                                           |
| gasLimit        | BIGINT    | The maximum gas allowed in this block.                                                             |
| gasUsed         | BIGINT    | The total used gas by all transactions in this block.                                              |
| timestamp       | TIMESTAMP | The unix timestamp for when the block was collated.                                                |

### **Example**

The above example demonstrates how to query Ethereum block data using a specified range of block numbers and an RPC URL. The table output displays various attributes of the Ethereum blocks, such as the block hash, block number, nonce, base fee per gas, parent hash, miner address, difficulty, total difficulty, size, gas limit, gas used, and timestamp. These attributes provide valuable insights into the blockchain's state and activity for the queried range of blocks.

```
D set variable eth_url = 'https://eth-mainnet.g.alchemy.com/v2/_VAP1LMRwnhUbKarsWEtC_nYZk-yHPEm';
D select * from eth_blocks_rpc(21104078, 21104178, getvariable('eth_url')) limit 10;
┌──────────────────────┬──────────┬────────────────────┬───────────────┬──────────────────────┬──────────────────────┬───┬──────────────────────┬────────┬──────────┬──────────┬─────────────────────┐
│         hash         │  number  │       nonce        │ baseFeePerGas │      parentHash      │        miner         │ … │   totalDifficulty    │  size  │ gasLimit │ gasUsed  │      timestamp      │
│       varchar        │  int64   │      varchar       │    varchar    │       varchar        │       varchar        │   │       varchar        │ int64  │  int64   │  int64   │      timestamp      │
├──────────────────────┼──────────┼────────────────────┼───────────────┼──────────────────────┼──────────────────────┼───┼──────────────────────┼────────┼──────────┼──────────┼─────────────────────┤
│ 0x8e8d1d95a717a152…  │ 21104078 │ 0x0000000000000000 │ 0xc4896b99    │ 0x8ba7dba9eac3d806…  │ 0x95222290dd7278aa…  │ … │ 0xc70d815d562d3cfa…  │ 102446 │ 30000000 │ 24390088 │ 2024-11-03 02:18:23 │
│ 0x10fa22bea6d33914…  │ 21104079 │ 0x0000000000000000 │ 0xd3ea7b7a    │ 0x8e8d1d95a717a152…  │ 0x95222290dd7278aa…  │ … │ 0xc70d815d562d3cfa…  │  57087 │ 30000000 │ 17756256 │ 2024-11-03 02:18:35 │
│ 0xb50d27210ca2fffe…  │ 21104080 │ 0x0000000000000000 │ 0xd8c88d01    │ 0x10fa22bea6d33914…  │ 0x95222290dd7278aa…  │ … │ 0xc70d815d562d3cfa…  │  76943 │ 30000000 │ 13215058 │ 2024-11-03 02:18:47 │
│ 0x30bdeff3c89efcc3…  │ 21104081 │ 0x0000000000000000 │ 0xd58f1102    │ 0xb50d27210ca2fffe…  │ 0x4838b106fce9647b…  │ … │ 0xc70d815d562d3cfa…  │  67530 │ 30000000 │ 13388296 │ 2024-11-03 02:18:59 │
│ 0x14270e8fa4a20c33…  │ 21104082 │ 0x0000000000000000 │ 0xd2b0c961    │ 0x30bdeff3c89efcc3…  │ 0x95222290dd7278aa…  │ … │ 0xc70d815d562d3cfa…  │  85068 │ 30000000 │ 29998071 │ 2024-11-03 02:19:11 │
│ 0xb752240613baa261…  │ 21104083 │ 0x0000000000000000 │ 0xed060497    │ 0x14270e8fa4a20c33…  │ 0x62d4d3785f8117be…  │ … │ 0xc70d815d562d3cfa…  │  50019 │ 30000000 │ 10851748 │ 2024-11-03 02:19:23 │
│ 0x6510d2b0ff0412eb…  │ 21104084 │ 0x0000000000000000 │ 0xe4d47425    │ 0xb752240613baa261…  │ 0x95222290dd7278aa…  │ … │ 0xc70d815d562d3cfa…  │  44449 │ 30000000 │ 14025126 │ 2024-11-03 02:19:35 │
│ 0x60a4777b3f98cd72…  │ 21104085 │ 0x0000000000000000 │ 0xe2f88c8d    │ 0x6510d2b0ff0412eb…  │ 0x95222290dd7278aa…  │ … │ 0xc70d815d562d3cfa…  │  55485 │ 30000000 │ 12068384 │ 2024-11-03 02:19:47 │
│ 0xe7d31b62f4e78a66…  │ 21104086 │ 0x0000000000000000 │ 0xdd6d0c12    │ 0x60a4777b3f98cd72…  │ 0x4838b106fce9647b…  │ … │ 0xc70d815d562d3cfa…  │  66313 │ 30000000 │ 29627365 │ 2024-11-03 02:19:59 │
│ 0xb6c8faa1aef8a35f…  │ 21104087 │ 0x0000000000000000 │ 0xf86aa789    │ 0xe7d31b62f4e78a66…  │ 0x9f4cf329f4cf376b…  │ … │ 0xc70d815d562d3cfa…  │  10795 │ 30000000 │  2105443 │ 2024-11-03 02:20:11 │
├──────────────────────┴──────────┴────────────────────┴───────────────┴──────────────────────┴──────────────────────┴───┴──────────────────────┴────────┴──────────┴──────────┴─────────────────────┤
│ 10 rows                                                                                                                                                                      12 columns (11 shown) │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```
