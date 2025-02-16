---
icon: train-track
---

# Traces v2

### Table function

The **eth\_traces\_v2\_rpc** table contains EVM transaction traces, including both main and internal transactions. Basically the same as **eth\_traces\_rpc**, but it uses another RPC interface: **debug\_traceBlockByNumber**, which is a debugging API method provided by the Geth (Go-Ethereum) client.

### **Procedure**

1. **Establish a Connection**: Connect to your Ethereum node using the URL provided in the inputs.
2. **Set Block Range**: Determine the block range by specifying `fromBlock` and `toBlock`. These arguments represent the starting and ending block numbers for scanning.
3. **Execute RPC Call**: Invoke the **eth\_traces\_v2\_rpc** function, passing the required arguments (`fromBlock`, `toBlock`, and `url`).
4. **Retrieve and Analyze Data**: Collect the output data, which includes detailed transaction traces. Use this data to gain insights into transaction processes and perform any necessary debugging or analysis.

### **Inputs**

| Args      | Types   | Info                                 |
| --------- | ------- | ------------------------------------ |
| fromBlock | BigInt  | Block number to start scanning from. |
| toBlock   | BigInt  | Block number to stop scanning at.    |
| url       | VARCHAR | URL of the Ethereum node.            |

### **Outputs**

| Column names | Types        | Info                                                                                       |
| ------------ | ------------ | ------------------------------------------------------------------------------------------ |
| blockNumber  | BIGINT       | The block number.                                                                          |
| type         | VARCHAR      | trace type.(CALL, STATICCALL, DELEGATECALL...)                                             |
| from         | VARCHAR      | address of the sender                                                                      |
| to           | VARCHAR      | address of the receiver                                                                    |
| value        | VARCHAR      | Amount of ETH sent from sender to recipient (if any), measured in wei (1 ETH = 10^18 wei)  |
| input        | VARCHAR      | call data provided to this trace, often containing function signatures and parameters      |
| gas          | BIGINT       | gas provided by the caller                                                                 |
| error        | VARCHAR      | Error message or code if the trace execution failed                                        |
| output       | VARCHAR      | output data from the call.                                                                 |
| gasUsed      | BIGINT       | Actual amount of gas consumed by this trace's execution                                    |
| subtraces    | BIGINT       | Number of subtraces created by this trace                                                  |
| traceAddress | LIST(BIGINT) | Array indicating the exact position of this trace within the trace tree of the transaction |
| revertReason | VARCHAR      | Solidity revert reason, if any                                                             |

### **Example**

```
D set variable eth_url = 'https://capable-winter-film.quiknode.pro/{API_KEY}';
D select * from eth_traces_v2_rpc(21104078, 21104078, getvariable('eth_url'));
┌─────────────┬──────────────┬──────────────────────┬──────────────────────┬──────────────────┬───┬─────────┬──────────────────────┬─────────┬───────────┬──────────────┬──────────────┐
│ blockNumber │     type     │         from         │          to          │      value       │ … │  error  │        output        │ gasUsed │ subtraces │ traceAddress │ revertReason │
│    int64    │   varchar    │       varchar        │       varchar        │     varchar      │   │ varchar │       varchar        │  int64  │   int64   │   int64[]    │   varchar    │
├─────────────┼──────────────┼──────────────────────┼──────────────────────┼──────────────────┼───┼─────────┼──────────────────────┼─────────┼───────────┼──────────────┼──────────────┤
│    21104078 │ CALL         │ 0xae2fc483527b8ef9…  │ 0x1f2f10d1c40777ae…  │ 0x6f             │ … │ NULL    │ NULL                 │  192774 │         2 │ NULL         │ NULL         │
│    21104078 │ CALL         │ 0x1f2f10d1c40777ae…  │ 0xabd055069a6b04db…  │ 0x0              │ … │ NULL    │ 0xffffffffffffffff…  │   69204 │         4 │ [0]          │ NULL         │
│    21104078 │ CALL         │ 0xabd055069a6b04db…  │ 0xabec00542d141bdd…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │   25380 │         0 │ [0, 0]       │ NULL         │
│    21104078 │ STATICCALL   │ 0xabd055069a6b04db…  │ 0xc02aaa39b223fe8d…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │     534 │         0 │ [0, 1]       │ NULL         │
│    21104078 │ CALL         │ 0xabd055069a6b04db…  │ 0x1f2f10d1c40777ae…  │ 0x0              │ … │ NULL    │ NULL                 │    9274 │         1 │ [0, 2]       │ NULL         │
│    21104078 │ CALL         │ 0x1f2f10d1c40777ae…  │ 0xc02aaa39b223fe8d…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │    8862 │         0 │ [0, 2, 0]    │ NULL         │
│    21104078 │ STATICCALL   │ 0xabd055069a6b04db…  │ 0xc02aaa39b223fe8d…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │     534 │         0 │ [0, 3]       │ NULL         │
│    21104078 │ CALL         │ 0x1f2f10d1c40777ae…  │ 0x60a8ea6005f7db58…  │ 0x0              │ … │ NULL    │ NULL                 │   28828 │         3 │ [1]          │ NULL         │
│    21104078 │ CALL         │ 0x60a8ea6005f7db58…  │ 0xc02aaa39b223fe8d…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │    6062 │         0 │ [1, 0]       │ NULL         │
│    21104078 │ STATICCALL   │ 0x60a8ea6005f7db58…  │ 0xabec00542d141bdd…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │     909 │         0 │ [1, 1]       │ NULL         │
│    21104078 │ STATICCALL   │ 0x60a8ea6005f7db58…  │ 0xc02aaa39b223fe8d…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │     534 │         0 │ [1, 2]       │ NULL         │
│    21104078 │ CALL         │ 0x08903a3be1e0c263…  │ 0x3fc91a3afd70395c…  │ 0x0              │ … │ NULL    │ NULL                 │  211764 │        12 │ NULL         │ NULL         │
│    21104078 │ CALL         │ 0x3fc91a3afd70395c…  │ 0x000000000022d473…  │ 0x0              │ … │ NULL    │ NULL                 │   30786 │         1 │ [0]          │ NULL         │
│    21104078 │ STATICCALL   │ 0x000000000022d473…  │ 0x0000000000000000…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │    3000 │         0 │ [0, 0]       │ NULL         │
│    21104078 │ CALL         │ 0x3fc91a3afd70395c…  │ 0x000000000022d473…  │ 0x0              │ … │ NULL    │ NULL                 │   74806 │         1 │ [1]          │ NULL         │
│    21104078 │ CALL         │ 0x000000000022d473…  │ 0xabec00542d141bdd…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │   71099 │         0 │ [1, 0]       │ NULL         │
│    21104078 │ STATICCALL   │ 0x3fc91a3afd70395c…  │ 0xc02aaa39b223fe8d…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │    2534 │         0 │ [2]          │ NULL         │
│    21104078 │ STATICCALL   │ 0x3fc91a3afd70395c…  │ 0x60a8ea6005f7db58…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │    2504 │         0 │ [3]          │ NULL         │
│    21104078 │ STATICCALL   │ 0x3fc91a3afd70395c…  │ 0xabec00542d141bdd…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │     909 │         0 │ [4]          │ NULL         │
│    21104078 │ CALL         │ 0x3fc91a3afd70395c…  │ 0x60a8ea6005f7db58…  │ 0x0              │ … │ NULL    │ NULL                 │   50312 │         3 │ [5]          │ NULL         │
│        ·    │  ·           │          ·           │          ·           │  ·               │ · │  ·      │  ·                   │      ·  │         · │  ·           │  ·           │
│        ·    │  ·           │          ·           │          ·           │  ·               │ · │  ·      │  ·                   │      ·  │         · │  ·           │  ·           │
│        ·    │  ·           │          ·           │          ·           │  ·               │ · │  ·      │  ·                   │      ·  │         · │  ·           │  ·           │
│    21104078 │ STATICCALL   │ 0xc1994a7efddd1a42…  │ 0xec53bf9167f50cde…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │    9765 │         1 │ [0, 0]       │ NULL         │
│    21104078 │ DELEGATECALL │ 0xec53bf9167f50cde…  │ 0x17f56e911c279bad…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │    2626 │         0 │ [0, 0, 0]    │ NULL         │
│    21104078 │ STATICCALL   │ 0xc1994a7efddd1a42…  │ 0xc76b81d835a6ef88…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │     836 │         0 │ [0, 1]       │ NULL         │
│    21104078 │ CALL         │ 0xc1994a7efddd1a42…  │ 0xec53bf9167f50cde…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │   18011 │         1 │ [0, 2]       │ NULL         │
│    21104078 │ DELEGATECALL │ 0xec53bf9167f50cde…  │ 0x17f56e911c279bad…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │   17369 │         0 │ [0, 2, 0]    │ NULL         │
│    21104078 │ CALL         │ 0x1651a65f3f5e3141…  │ 0x6801763c790abe6c…  │ 0xa37f19a1d960   │ … │ NULL    │ NULL                 │   21000 │         0 │ NULL         │ NULL         │
│    21104078 │ CALL         │ 0xcbd6832ebc203e49…  │ 0x20c7e0f6822a0664…  │ 0x55c390debc6000 │ … │ NULL    │ NULL                 │   21000 │         0 │ NULL         │ NULL         │
│    21104078 │ CALL         │ 0xa06ee26610f2a230…  │ 0x2bfbdc1d8985a1ae…  │ 0x5cc4b9c46000   │ … │ NULL    │ NULL                 │   21000 │         0 │ NULL         │ NULL         │
│    21104078 │ CALL         │ 0x38fc712418276b5d…  │ 0x018a220d9d6a3c25…  │ 0x13b983bbcb000  │ … │ NULL    │ NULL                 │   21000 │         0 │ NULL         │ NULL         │
│    21104078 │ CALL         │ 0x93793bd1f3e35a0e…  │ 0x68d3a973e7272eb3…  │ 0x14205ce        │ … │ NULL    │ NULL                 │  121451 │         1 │ NULL         │ NULL         │
│    21104078 │ CALL         │ 0x68d3a973e7272eb3…  │ 0x62e0d3fd804dfbf0…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │   85580 │         4 │ [0]          │ NULL         │
│    21104078 │ CALL         │ 0x62e0d3fd804dfbf0…  │ 0xb528edbef013aff8…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │   12540 │         0 │ [0, 0]       │ NULL         │
│    21104078 │ STATICCALL   │ 0x62e0d3fd804dfbf0…  │ 0xa0b86991c6218b36…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │    9839 │         1 │ [0, 1]       │ NULL         │
│    21104078 │ DELEGATECALL │ 0xa0b86991c6218b36…  │ 0x43506849d7c04f91…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │    2553 │         0 │ [0, 1, 0]    │ NULL         │
│    21104078 │ CALL         │ 0x62e0d3fd804dfbf0…  │ 0x68d3a973e7272eb3…  │ 0x0              │ … │ NULL    │ NULL                 │   16943 │         1 │ [0, 2]       │ NULL         │
│    21104078 │ CALL         │ 0x68d3a973e7272eb3…  │ 0xa0b86991c6218b36…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │   15052 │         1 │ [0, 2, 0]    │ NULL         │
│    21104078 │ DELEGATECALL │ 0xa0b86991c6218b36…  │ 0x43506849d7c04f91…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │   14263 │         0 │ [0, 2, 0, 0] │ NULL         │
│    21104078 │ STATICCALL   │ 0x62e0d3fd804dfbf0…  │ 0xa0b86991c6218b36…  │ NULL             │ … │ NULL    │ 0x0000000000000000…  │    1339 │         1 │ [0, 3]       │ NULL         │
│    21104078 │ DELEGATECALL │ 0xa0b86991c6218b36…  │ 0x43506849d7c04f91…  │ 0x0              │ … │ NULL    │ 0x0000000000000000…  │     553 │         0 │ [0, 3, 0]    │ NULL         │
│    21104078 │ CALL         │ 0x95222290dd7278aa…  │ 0x388c818ca8b9251b…  │ 0xe9c0c9428e82ef │ … │ NULL    │ NULL                 │   22111 │         0 │ NULL         │ NULL         │
├─────────────┴──────────────┴──────────────────────┴──────────────────────┴──────────────────┴───┴─────────┴──────────────────────┴─────────┴───────────┴──────────────┴──────────────┤
│ 1406 rows (40 shown)                                                                                                                                           13 columns (11 shown) │
└──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### Dependent RPC Method

* debug\_traceBlockByNumber
