---
icon: arrows-rotate-reverse
---

# Try your first query

To explore the Ethereum blocks further, the query shown retrieves specific details for a range of block numbers, from 21104078 to 21104080. The retrieval includes attributes such as the block hash, block number, nonce, base fee per gas, parent hash, miner, total difficulty, size, gas limit, gas used, and timestamp.

When querying Ethereum data, consider checking the credibility of the source, ensuring that the `eth_url` you utilize is from a reliable provider like Alchemy, as shown in the example. This guarantees that the data is authentic and up-to-date.&#x20;

```
set variable eth_url = 'https://eth-mainnet.g.alchemy.com/v2/{API_KEY}';
D select * from eth_blocks_rpc(21104078, 21104080, getvariable('eth_url'));
┌──────────────────────┬──────────┬────────────────────┬───────────────┬──────────────────────┬──────────────────────┬───┬──────────────────────┬────────┬──────────┬──────────┬─────────────────────┐
│         hash         │  number  │       nonce        │ baseFeePerGas │      parentHash      │        miner         │ … │   totalDifficulty    │  size  │ gasLimit │ gasUsed  │      timestamp      │
│       varchar        │  int64   │      varchar       │    varchar    │       varchar        │       varchar        │   │       varchar        │ int64  │  int64   │  int64   │      timestamp      │
├──────────────────────┼──────────┼────────────────────┼───────────────┼──────────────────────┼──────────────────────┼───┼──────────────────────┼────────┼──────────┼──────────┼─────────────────────┤
│ 0x8e8d1d95a717a152…  │ 21104078 │ 0x0000000000000000 │ 0xc4896b99    │ 0x8ba7dba9eac3d806…  │ 0x95222290dd7278aa…  │ … │ 0xc70d815d562d3cfa…  │ 102446 │ 30000000 │ 24390088 │ 2024-11-03 02:18:23 │
│ 0x10fa22bea6d33914…  │ 21104079 │ 0x0000000000000000 │ 0xd3ea7b7a    │ 0x8e8d1d95a717a152…  │ 0x95222290dd7278aa…  │ … │ 0xc70d815d562d3cfa…  │  57087 │ 30000000 │ 17756256 │ 2024-11-03 02:18:35 │
│ 0xb50d27210ca2fffe…  │ 21104080 │ 0x0000000000000000 │ 0xd8c88d01    │ 0x10fa22bea6d33914…  │ 0x95222290dd7278aa…  │ … │ 0xc70d815d562d3cfa…  │  76943 │ 30000000 │ 13215058 │ 2024-11-03 02:18:47 │
├──────────────────────┴──────────┴────────────────────┴───────────────┴──────────────────────┴──────────────────────┴───┴──────────────────────┴────────┴──────────┴──────────┴─────────────────────┤
│ 3 rows                                                                                                                                                                       12 columns (11 shown) │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

