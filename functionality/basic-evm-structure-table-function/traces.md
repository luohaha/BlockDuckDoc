---
icon: train-track
---

# Traces

### Table function

The **eth\_traces\_rpc** table logs EVM transaction traces, including both main and internal transactions. These traces help in debugging and understanding transaction execution. Also known as `internal transactions`, they provide insights into the transaction processes.

### **Procedure**

To utilize the **eth\_traces\_rpc** function, follow these steps:

1. **Establish a Connection**: Connect to your Ethereum node using the URL provided in the inputs.
2. **Set Block Range**: Determine the block range by specifying `fromBlock` and `toBlock`. These arguments represent the starting and ending block numbers for scanning.
3. **Execute RPC Call**: Invoke the eth\_traces\_rpc function, passing the required arguments (`fromBlock`, `toBlock`, and `url`).
4. **Retrieve and Analyze Data**: Collect the output data, which includes detailed transaction traces. Use this data to gain insights into transaction processes and perform any necessary debugging or analysis.

### **Inputs**

| Args      | Types   | Info                                 |
| --------- | ------- | ------------------------------------ |
| fromBlock | BigInt  | Block number to start scanning from. |
| toBlock   | BigInt  | Block number to stop scanning at.    |
| url       | VARCHAR | URL of the Ethereum node.            |

### **Outputs**

| Column names        | Types        | Info                                                                                       |
| ------------------- | ------------ | ------------------------------------------------------------------------------------------ |
| blockHash           | VARCHAR      | Hash of the block.                                                                         |
| blockNumber         | BIGINT       | The block number.                                                                          |
| callType            | VARCHAR      | callType: call type, "call", "delegatecall", "staticcall", "create".                       |
| from                | VARCHAR      | address of the sender                                                                      |
| to                  | VARCHAR      | address of the receiver                                                                    |
| value               | VARCHAR      | Amount of ETH sent from sender to recipient (if any), measured in wei (1 ETH = 10^18 wei)  |
| input               | VARCHAR      | call data provided to this trace, often containing function signatures and parameters      |
| gas                 | BIGINT       | gas provided by the caller                                                                 |
| error               | VARCHAR      | Error message or code if the trace execution failed                                        |
| output              | VARCHAR      | output data from the call.                                                                 |
| gasUsed             | BIGINT       | Actual amount of gas consumed by this trace's execution                                    |
| subtraces           | BIGINT       | Number of subtraces created by this trace                                                  |
| traceAddress        | LIST(BIGINT) | Array indicating the exact position of this trace within the trace tree of the transaction |
| type                | VARCHAR      | Type of trace (e.g., call, create, suicide) indicating the nature of the operation         |
| transactionHash     | VARCHAR      | hash of the parent transaction                                                             |
| transactionPosition | INTEGER      | Position of the parent transaction within its containing block                             |

### **Example**

```
D set variable eth_url = 'https://capable-winter-film.quiknode.pro/eeb424c4501392006b590ff1fa7f55e5ce8dc8ac';
D select * from eth_traces_rpc(21104078, 21104078, getvariable('eth_url'));
┌──────────────────────┬─────────────┬──────────────┬──────────────────────┬──────────────────────┬───┬───────────┬──────────────┬─────────┬──────────────────────┬─────────────────────┐
│      blockHash       │ blockNumber │   callType   │         from         │          to          │ … │ subtraces │ traceAddress │  type   │   transactionHash    │ transactionPosition │
│       varchar        │    int64    │   varchar    │       varchar        │       varchar        │   │   int64   │   int64[]    │ varchar │       varchar        │        int32        │
├──────────────────────┼─────────────┼──────────────┼──────────────────────┼──────────────────────┼───┼───────────┼──────────────┼─────────┼──────────────────────┼─────────────────────┤
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0xae2fc483527b8ef9…  │ 0x1f2f10d1c40777ae…  │ … │         2 │ []           │ call    │ 0x15b539fdf722615a…  │                   0 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x1f2f10d1c40777ae…  │ 0xabd055069a6b04db…  │ … │         4 │ [0]          │ call    │ 0x15b539fdf722615a…  │                   0 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0xabd055069a6b04db…  │ 0xabec00542d141bdd…  │ … │         0 │ [0, 0]       │ call    │ 0x15b539fdf722615a…  │                   0 │
│ 0x8e8d1d95a717a152…  │    21104078 │ staticcall   │ 0xabd055069a6b04db…  │ 0xc02aaa39b223fe8d…  │ … │         0 │ [0, 1]       │ call    │ 0x15b539fdf722615a…  │                   0 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0xabd055069a6b04db…  │ 0x1f2f10d1c40777ae…  │ … │         1 │ [0, 2]       │ call    │ 0x15b539fdf722615a…  │                   0 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x1f2f10d1c40777ae…  │ 0xc02aaa39b223fe8d…  │ … │         0 │ [0, 2, 0]    │ call    │ 0x15b539fdf722615a…  │                   0 │
│ 0x8e8d1d95a717a152…  │    21104078 │ staticcall   │ 0xabd055069a6b04db…  │ 0xc02aaa39b223fe8d…  │ … │         0 │ [0, 3]       │ call    │ 0x15b539fdf722615a…  │                   0 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x1f2f10d1c40777ae…  │ 0x60a8ea6005f7db58…  │ … │         3 │ [1]          │ call    │ 0x15b539fdf722615a…  │                   0 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x60a8ea6005f7db58…  │ 0xc02aaa39b223fe8d…  │ … │         0 │ [1, 0]       │ call    │ 0x15b539fdf722615a…  │                   0 │
│ 0x8e8d1d95a717a152…  │    21104078 │ staticcall   │ 0x60a8ea6005f7db58…  │ 0xabec00542d141bdd…  │ … │         0 │ [1, 1]       │ call    │ 0x15b539fdf722615a…  │                   0 │
│ 0x8e8d1d95a717a152…  │    21104078 │ staticcall   │ 0x60a8ea6005f7db58…  │ 0xc02aaa39b223fe8d…  │ … │         0 │ [1, 2]       │ call    │ 0x15b539fdf722615a…  │                   0 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x08903a3be1e0c263…  │ 0x3fc91a3afd70395c…  │ … │        12 │ []           │ call    │ 0x1bd4d5006a6b321c…  │                   1 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x3fc91a3afd70395c…  │ 0x000000000022d473…  │ … │         0 │ [0]          │ call    │ 0x1bd4d5006a6b321c…  │                   1 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x3fc91a3afd70395c…  │ 0x000000000022d473…  │ … │         1 │ [1]          │ call    │ 0x1bd4d5006a6b321c…  │                   1 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x000000000022d473…  │ 0xabec00542d141bdd…  │ … │         0 │ [1, 0]       │ call    │ 0x1bd4d5006a6b321c…  │                   1 │
│ 0x8e8d1d95a717a152…  │    21104078 │ staticcall   │ 0x3fc91a3afd70395c…  │ 0xc02aaa39b223fe8d…  │ … │         0 │ [2]          │ call    │ 0x1bd4d5006a6b321c…  │                   1 │
│ 0x8e8d1d95a717a152…  │    21104078 │ staticcall   │ 0x3fc91a3afd70395c…  │ 0x60a8ea6005f7db58…  │ … │         0 │ [3]          │ call    │ 0x1bd4d5006a6b321c…  │                   1 │
│ 0x8e8d1d95a717a152…  │    21104078 │ staticcall   │ 0x3fc91a3afd70395c…  │ 0xabec00542d141bdd…  │ … │         0 │ [4]          │ call    │ 0x1bd4d5006a6b321c…  │                   1 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x3fc91a3afd70395c…  │ 0x60a8ea6005f7db58…  │ … │         3 │ [5]          │ call    │ 0x1bd4d5006a6b321c…  │                   1 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x60a8ea6005f7db58…  │ 0xc02aaa39b223fe8d…  │ … │         0 │ [5, 0]       │ call    │ 0x1bd4d5006a6b321c…  │                   1 │
│          ·           │        ·    │  ·           │          ·           │          ·           │ · │         · │   ·          │  ·      │          ·           │                   · │
│          ·           │        ·    │  ·           │          ·           │          ·           │ · │         · │   ·          │  ·      │          ·           │                   · │
│          ·           │        ·    │  ·           │          ·           │          ·           │ · │         · │   ·          │  ·      │          ·           │                   · │
│ 0x8e8d1d95a717a152…  │    21104078 │ staticcall   │ 0xc1994a7efddd1a42…  │ 0xec53bf9167f50cde…  │ … │         1 │ [0, 0]       │ call    │ 0x3434012fef72cf68…  │                 220 │
│ 0x8e8d1d95a717a152…  │    21104078 │ delegatecall │ 0xec53bf9167f50cde…  │ 0x17f56e911c279bad…  │ … │         0 │ [0, 0, 0]    │ call    │ 0x3434012fef72cf68…  │                 220 │
│ 0x8e8d1d95a717a152…  │    21104078 │ staticcall   │ 0xc1994a7efddd1a42…  │ 0xc76b81d835a6ef88…  │ … │         0 │ [0, 1]       │ call    │ 0x3434012fef72cf68…  │                 220 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0xc1994a7efddd1a42…  │ 0xec53bf9167f50cde…  │ … │         1 │ [0, 2]       │ call    │ 0x3434012fef72cf68…  │                 220 │
│ 0x8e8d1d95a717a152…  │    21104078 │ delegatecall │ 0xec53bf9167f50cde…  │ 0x17f56e911c279bad…  │ … │         0 │ [0, 2, 0]    │ call    │ 0x3434012fef72cf68…  │                 220 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x1651a65f3f5e3141…  │ 0x6801763c790abe6c…  │ … │         0 │ []           │ call    │ 0x2191c99ee4e6deb4…  │                 221 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0xcbd6832ebc203e49…  │ 0x20c7e0f6822a0664…  │ … │         0 │ []           │ call    │ 0x563ead3eca191083…  │                 222 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0xa06ee26610f2a230…  │ 0x2bfbdc1d8985a1ae…  │ … │         0 │ []           │ call    │ 0x4933adb2f4d95b7e…  │                 223 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x38fc712418276b5d…  │ 0x018a220d9d6a3c25…  │ … │         0 │ []           │ call    │ 0xfda2256c3f3d7541…  │                 224 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x93793bd1f3e35a0e…  │ 0x68d3a973e7272eb3…  │ … │         1 │ []           │ call    │ 0xa514abcac47226ca…  │                 225 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x68d3a973e7272eb3…  │ 0x62e0d3fd804dfbf0…  │ … │         4 │ [0]          │ call    │ 0xa514abcac47226ca…  │                 225 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x62e0d3fd804dfbf0…  │ 0xb528edbef013aff8…  │ … │         0 │ [0, 0]       │ call    │ 0xa514abcac47226ca…  │                 225 │
│ 0x8e8d1d95a717a152…  │    21104078 │ staticcall   │ 0x62e0d3fd804dfbf0…  │ 0xa0b86991c6218b36…  │ … │         1 │ [0, 1]       │ call    │ 0xa514abcac47226ca…  │                 225 │
│ 0x8e8d1d95a717a152…  │    21104078 │ delegatecall │ 0xa0b86991c6218b36…  │ 0x43506849d7c04f91…  │ … │         0 │ [0, 1, 0]    │ call    │ 0xa514abcac47226ca…  │                 225 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x62e0d3fd804dfbf0…  │ 0x68d3a973e7272eb3…  │ … │         1 │ [0, 2]       │ call    │ 0xa514abcac47226ca…  │                 225 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x68d3a973e7272eb3…  │ 0xa0b86991c6218b36…  │ … │         1 │ [0, 2, 0]    │ call    │ 0xa514abcac47226ca…  │                 225 │
│ 0x8e8d1d95a717a152…  │    21104078 │ delegatecall │ 0xa0b86991c6218b36…  │ 0x43506849d7c04f91…  │ … │         0 │ [0, 2, 0, 0] │ call    │ 0xa514abcac47226ca…  │                 225 │
│ 0x8e8d1d95a717a152…  │    21104078 │ staticcall   │ 0x62e0d3fd804dfbf0…  │ 0xa0b86991c6218b36…  │ … │         1 │ [0, 3]       │ call    │ 0xa514abcac47226ca…  │                 225 │
│ 0x8e8d1d95a717a152…  │    21104078 │ delegatecall │ 0xa0b86991c6218b36…  │ 0x43506849d7c04f91…  │ … │         0 │ [0, 3, 0]    │ call    │ 0xa514abcac47226ca…  │                 225 │
│ 0x8e8d1d95a717a152…  │    21104078 │ call         │ 0x95222290dd7278aa…  │ 0x388c818ca8b9251b…  │ … │         0 │ []           │ call    │ 0xc2df1664c2a440b5…  │                 226 │
├──────────────────────┴─────────────┴──────────────┴──────────────────────┴──────────────────────┴───┴───────────┴──────────────┴─────────┴──────────────────────┴─────────────────────┤
│ 1370 rows (40 shown)                                                                                                                                            16 columns (10 shown) │
└───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

