---
icon: right-from-bracket
---

# Outputs

The **bitcoin\_outputs\_rpc** table contains information about the outputs of Bitcoin transactions. An output is a log detailing the amount of Bitcoin transferred to.

### **Inputs**

| Args      | Types   | Info                                 |
| --------- | ------- | ------------------------------------ |
| fromBlock | BIGINT  | Block number to start scanning from. |
| toBlock   | BIGINT  | Block number to stop scanning at.    |
| url       | VARCHAR | URL of the Bitcoin node.             |

### **Outputs**

| Column names      | Types         | Info                                                |
| ----------------- | ------------- | --------------------------------------------------- |
| time              | TIMESTAMP     | The block time                                      |
| block\_number     | BIGINT        | The block number                                    |
| block\_hash       | VARCHAR       | The block hash                                      |
| txid              | VARCHAR       | The transaction ID                                  |
| index             | UBIGINT       | The position of this output within the transaction  |
| value             | DOUBLE        | The value of the output                             |
| addresses         | LIST(VARCHAR) | The Bitcoin address(es) associated with this output |
| type              | VARCHAR       | The type of the address                             |
| script\_asm       | VARCHAR       | The script in assembly format                       |
| script\_hex       | VARCHAR       | The script in hexadecimal format                    |
| transaction\_hash | VARCHAR       | The hash of the transaction containing this input   |

### Examples

```
D set variable bitcoin_url = 'https://bitcoin-mainnet.core.chainstack.com/xxx';
D select * from bitcoin_outputs_rpc(886654, 886654, getvariable('bitcoin_url'));
┌─────────────────────┬──────────────┬──────────────────────┬──────────────────────┬────────┬───┬──────────────────────┬──────────────────────┬──────────────────────┬──────────────────────┬──────────────────────┐
│        time         │ block_number │      block_hash      │         txid         │ index  │ … │      addresses       │         type         │      script_asm      │      script_hex      │   transaction_hash   │
│      timestamp      │    int64     │       varchar        │       varchar        │ uint64 │   │      varchar[]       │       varchar        │       varchar        │       varchar        │       varchar        │
├─────────────────────┼──────────────┼──────────────────────┼──────────────────────┼────────┼───┼──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ f397dd542f4f1dd0e7…  │      0 │ … │ ["bc1pp7w6kxnj7lzg…  │ witness_v1_taproot   │ 1 0f9dab1a72f7c48d…  │ 51200f9dab1a72f7c4…  │ 4bc9f4fbd1f3aea067…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ f397dd542f4f1dd0e7…  │      1 │ … │ ["bc1qwzrryqr3ja8w…  │ witness_v0_scripth…  │ 0 7086320071974eef…  │ 00207086320071974e…  │ 4bc9f4fbd1f3aea067…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ f397dd542f4f1dd0e7…  │      2 │ … │ NULL                 │ nulldata             │ OP_RETURN aa21a9ed…  │ 6a24aa21a9ed250a93…  │ 4bc9f4fbd1f3aea067…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ f397dd542f4f1dd0e7…  │      3 │ … │ NULL                 │ nulldata             │ OP_RETURN 434f5245…  │ 6a2d434f5245012e50…  │ 4bc9f4fbd1f3aea067…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ f397dd542f4f1dd0e7…  │      4 │ … │ NULL                 │ nulldata             │ OP_RETURN 52534b42…  │ 6a2952534b424c4f43…  │ 4bc9f4fbd1f3aea067…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 29bb08bd18f253cf73…  │      0 │ … │ ["1J9uwBYepTm5737R…  │ pubkeyhash           │ OP_DUP OP_HASH160 …  │ 76a914bc29a73a98b6…  │ 29bb08bd18f253cf73…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 29bb08bd18f253cf73…  │      1 │ … │ NULL                 │ nulldata             │ OP_RETURN 6853a9c3…  │ 6a206853a9c38a4960…  │ 29bb08bd18f253cf73…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 87eaf7480075d6fb7a…  │      0 │ … │ ["1J9uwBYepTm5737R…  │ pubkeyhash           │ OP_DUP OP_HASH160 …  │ 76a914bc29a73a98b6…  │ 87eaf7480075d6fb7a…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 87eaf7480075d6fb7a…  │      1 │ … │ NULL                 │ nulldata             │ OP_RETURN 49e8109c…  │ 6a2049e8109c22d9c1…  │ 87eaf7480075d6fb7a…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ aac453c83e0c485a0d…  │      0 │ … │ ["1J9uwBYepTm5737R…  │ pubkeyhash           │ OP_DUP OP_HASH160 …  │ 76a914bc29a73a98b6…  │ aac453c83e0c485a0d…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ aac453c83e0c485a0d…  │      1 │ … │ NULL                 │ nulldata             │ OP_RETURN 05449551…  │ 6a2005449551fcd030…  │ aac453c83e0c485a0d…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 923abcf2a2b2ee60c7…  │      0 │ … │ ["1J9uwBYepTm5737R…  │ pubkeyhash           │ OP_DUP OP_HASH160 …  │ 76a914bc29a73a98b6…  │ 923abcf2a2b2ee60c7…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 923abcf2a2b2ee60c7…  │      1 │ … │ NULL                 │ nulldata             │ OP_RETURN 4f36da1e…  │ 6a204f36da1ec4beea…  │ 923abcf2a2b2ee60c7…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ b152cfefd7fed9ecbf…  │      0 │ … │ ["1Lva7CgxzEd2AP1J…  │ pubkeyhash           │ OP_DUP OP_HASH160 …  │ 76a914da8c127762f7…  │ 2926f5f088c432dac9…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ baa9484f319a40cd07…  │      0 │ … │ ["3CLDB8j92EWh3VTa…  │ scripthash           │ OP_HASH160 74ba0a6…  │ a91474ba0a6e9ddeb4…  │ baa9484f319a40cd07…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ baa9484f319a40cd07…  │      1 │ … │ ["19qJiMVJe17zWR1K…  │ pubkeyhash           │ OP_DUP OP_HASH160 …  │ 76a91460e3c22c9856…  │ baa9484f319a40cd07…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ a6eb96f9774e4a9e62…  │      0 │ … │ ["3DGxAYYUA61Wrrdb…  │ scripthash           │ OP_HASH160 7f14638…  │ a9147f1463882fd439…  │ f62c31d544886f2d12…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ a6eb96f9774e4a9e62…  │      1 │ … │ ["1EsqQmiPJ3uoy5BL…  │ pubkeyhash           │ OP_DUP OP_HASH160 …  │ 76a9149836d80205d4…  │ f62c31d544886f2d12…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 20601d8961129d37c1…  │      0 │ … │ ["bc1q866sv2stppgt…  │ witness_v0_scripth…  │ 0 3eb5062a0b0850b2…  │ 00203eb5062a0b0850…  │ 20601d8961129d37c1…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 20601d8961129d37c1…  │      1 │ … │ ["bc1qyy30guv6m5ez…  │ witness_v0_scripth…  │ 0 2122f4719add322f…  │ 00202122f4719add32…  │ 20601d8961129d37c1…  │
│          ·          │          ·   │          ·           │          ·           │      · │ · │  ·                   │    ·                 │          ·           │       ·              │          ·           │
│          ·          │          ·   │          ·           │          ·           │      · │ · │  ·                   │    ·                 │          ·           │       ·              │          ·           │
│          ·          │          ·   │          ·           │          ·           │      · │ · │  ·                   │    ·                 │          ·           │       ·              │          ·           │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 3843120da772b5b374…  │      1 │ … │ NULL                 │ nulldata             │ OP_RETURN 13 1310996 │ 6a5d0414011400       │ f5c597f9926e63b53c…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ a2db46a13900c28f92…  │      0 │ … │ ["bc1qktsvr7hqy66e…  │ witness_v0_keyhash   │ 0 b2e0c1fae026b598…  │ 0014b2e0c1fae026b5…  │ afb44d0c0c94786968…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ a2db46a13900c28f92…  │      1 │ … │ NULL                 │ nulldata             │ OP_RETURN 13 1310996 │ 6a5d0414011400       │ afb44d0c0c94786968…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 4f08966776a3dbc1c3…  │      0 │ … │ ["bc1qktsvr7hqy66e…  │ witness_v0_keyhash   │ 0 b2e0c1fae026b598…  │ 0014b2e0c1fae026b5…  │ dc7892cdefa9c3be57…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 4f08966776a3dbc1c3…  │      1 │ … │ NULL                 │ nulldata             │ OP_RETURN 13 1310996 │ 6a5d0414011400       │ dc7892cdefa9c3be57…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 2d5a70857b38a12a31…  │      0 │ … │ ["bc1qktsvr7hqy66e…  │ witness_v0_keyhash   │ 0 b2e0c1fae026b598…  │ 0014b2e0c1fae026b5…  │ 4017c539e6db0841bf…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 2d5a70857b38a12a31…  │      1 │ … │ NULL                 │ nulldata             │ OP_RETURN 13 1310996 │ 6a5d0414011400       │ 4017c539e6db0841bf…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 2dca20b7d1173d39af…  │      0 │ … │ ["3P4WqXDbSLRhzo2H…  │ scripthash           │ OP_HASH160 ea6b832…  │ a914ea6b832a05c6ca…  │ ecc1a824ff6c827880…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ eeffd5934a25188ff1…  │      0 │ … │ ["3P4WqXDbSLRhzo2H…  │ scripthash           │ OP_HASH160 ea6b832…  │ a914ea6b832a05c6ca…  │ ef585216d6080e2d6b…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 459f6d643f3c7b4c46…  │      0 │ … │ ["31qBiwtqFqM2DbwV…  │ scripthash           │ OP_HASH160 018b822…  │ a914018b8224b815b9…  │ 703787baeeb09d7e84…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 8e51d54491a32012f0…  │      0 │ … │ ["31qBiwtqFqM2DbwV…  │ scripthash           │ OP_HASH160 018b822…  │ a914018b8224b815b9…  │ 90ddaca07d49dc5b96…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 4db4487cc9598f501c…  │      0 │ … │ ["31qBiwtqFqM2DbwV…  │ scripthash           │ OP_HASH160 018b822…  │ a914018b8224b815b9…  │ 26a0eca2d7bde0c1c6…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 341cf61693681ac83f…  │      0 │ … │ ["31qBiwtqFqM2DbwV…  │ scripthash           │ OP_HASH160 018b822…  │ a914018b8224b815b9…  │ de9dd67f5996bd77f8…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ fb10df115adae318ed…  │      0 │ … │ ["31qBiwtqFqM2DbwV…  │ scripthash           │ OP_HASH160 018b822…  │ a914018b8224b815b9…  │ 5e8195e8807e9057f0…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ bf5fbedd06d0a48302…  │      0 │ … │ ["31qBiwtqFqM2DbwV…  │ scripthash           │ OP_HASH160 018b822…  │ a914018b8224b815b9…  │ 8dd0e035a0e2e3d041…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 32b67eb050ecf0e014…  │      0 │ … │ ["bc1pgula225sd82h…  │ witness_v1_taproot   │ 1 473fd52a9069d574…  │ 5120473fd52a9069d5…  │ d2163e7727b6cc9b58…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 716503e625103124a8…  │      0 │ … │ ["bc1qtr43gedgqgtr…  │ witness_v0_scripth…  │ 0 58eb1465a802163e…  │ 002058eb1465a80216…  │ 3248ce1b47c77aee56…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 716503e625103124a8…  │      1 │ … │ ["bc1pdcq4g205kmnp…  │ witness_v1_taproot   │ 1 6e015429f4b6e616…  │ 51206e015429f4b6e6…  │ 3248ce1b47c77aee56…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ 567dd63439444794bc…  │      0 │ … │ ["bc1quyqpa4pdcnm8…  │ witness_v0_keyhash   │ 0 e1001ed42dc4f677…  │ 0014e1001ed42dc4f6…  │ 2922305a6782b4d991…  │
│ 2025-03-07 00:02:24 │       886654 │ 000000000000000000…  │ d680da9da395543889…  │      0 │ … │ ["bc1qhv4he06j2hv7…  │ witness_v0_keyhash   │ 0 bb2b7cbf5255d9ec…  │ 0014bb2b7cbf5255d9…  │ b39c5d2e2d19fa0135…  │
├─────────────────────┴──────────────┴──────────────────────┴──────────────────────┴────────┴───┴──────────────────────┴──────────────────────┴──────────────────────┴──────────────────────┴──────────────────────┤
│ 6653 rows (40 shown)                                                                                                                                                                       11 columns (10 shown) │
└──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```
