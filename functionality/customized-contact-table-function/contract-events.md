---
icon: calendar-lines-pen
---

# Contract Events

### What is contract events

Contract events are a way for smart contracts, such as those on the Ethereum blockchain, to communicate action or changes to external entities or systems. They enable the logging of on-chain actions which can be captured and monitored off the blockchain by subscribers. These events are defined in the smart contract code, and they can be emitted during the execution of contract functions to provide information about transactions or changes in state, like token transfers or contract updates. This event-driven architecture facilitates efficient and scalable off-chain processing of blockchain interactions.

The event data in the contract is structured, and we can create a table function to analyze them.

### How to create

E.g. If you want to create a table function for ERC20 **`Transfer`** event. You can find its event ABI from [etherscan](https://etherscan.io/address/0x1f9840a85d5af5bf1d1762f925bdaddc4201f984#code)

```json
{"anonymous":false,
 "inputs":[
   {"indexed":true,"internalType":"address","name":"from","type":"address"},
   {"indexed":true,"internalType":"address","name":"to","type":"address"},
   {"indexed":false,"internalType":"uint256","name":"amount","type":"uint256"}
  ],
  "name":"Transfer",
  "type":"event"
}
```

Create a table function for `Transfer` event named `tranfer_erc20`:

```
pragma blockduck_create_contract_event_rpc('tranfer_erc20', '{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"from","type":"address"},{"indexed":true,"internalType":"address","name":"to","type":"address"},{"indexed":false,"internalType":"uint256","name":"amount","type":"uint256"}],"name":"Transfer","type":"event"}');
```

#### **inputs**

| Args       | Types   | Info                                                 |
| ---------- | ------- | ---------------------------------------------------- |
| suffix     | VARCHAR | Table function suffix to identify the specific event |
| event\_abi | VARCHAR | JSON ABI of the event to be monitored                |

#### **Example**

```
D pragma blockduck_create_contract_event_rpc('tranfer_erc20', '{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"from","type":"address"},{"indexed":true,"internalType":"address","name":"to","type":"address"},{"indexed":false,"internalType":"uint256","name":"amount","type":"uint256"}],"name":"Transfer","type":"event"}');
┌─────────┐
│ Success │
│ boolean │
├─────────┤
│ 0 rows  │
└─────────┘
```

### How to query

After that, table function named `eth_contract_event_rpc_tranfer_erc20` already been created. Then you can try to query from it.

#### **Inputs**

| Args      | Types         | Info                                |
| --------- | ------------- | ----------------------------------- |
| address   | LIST(VARCHAR) | Contract address emitting the event |
| fromBlock | BigInt        | Block number to start scanning from |
| toBlock   | BigInt        | Block number to stop scanning at    |
| url       | VARCHAR       | URL of the Ethereum node            |

#### **Examples**

```
D set variable eth_url = 'https://eth-mainnet.g.alchemy.com/v2/_VAP1LMRwnhUbKarsWEtC_nYZk-yHPEm';
D select * from eth_contract_event_rpc_tranfer_erc20([]::VARCHAR[], 21104078, 21104078, getvariable('eth_url')) limit 10;
┌──────────────────────┬─────────────┬──────────────────────┬─────────────────────────────────────────┬────────────────────────────────────────────────────────────────────┬──────────────────────────┐
│       address        │ blockNumber │   transactionHash    │                  from                   │                                 to                                 │          amount          │
│       varchar        │    int64    │       varchar        │                 varchar                 │                              varchar                               │          varint          │
├──────────────────────┼─────────────┼──────────────────────┼─────────────────────────────────────────┼────────────────────────────────────────────────────────────────────┼──────────────────────────┤
│ 0xabec00542d141bdd…  │    21104078 │ 0x15b539fdf722615a…  │ 0x000000000000000000000000abd055069a6…  │ 0x000000000000000000000000abec00542d141bddf58649bfe860c6449807237c │ 105836228163203292253    │
│ 0xabec00542d141bdd…  │    21104078 │ 0x15b539fdf722615a…  │ 0x000000000000000000000000abd055069a6…  │ 0x00000000000000000000000060a8ea6005f7db580bc0c9341e7e6275d114e874 │ 10477786588157125933126  │
│ 0xc02aaa39b223fe8d…  │    21104078 │ 0x15b539fdf722615a…  │ 0x0000000000000000000000001f2f10d1c40…  │ 0x000000000000000000000000abd055069a6b04db7d1547f88dd01cf14ff09cfd │ 886249995970281472       │
│ 0xc02aaa39b223fe8d…  │    21104078 │ 0x15b539fdf722615a…  │ 0x00000000000000000000000060a8ea6005f…  │ 0x0000000000000000000000001f2f10d1c40777ae1da742455c65828ff36df387 │ 188832235783192576       │
│ 0xabec00542d141bdd…  │    21104078 │ 0x1bd4d5006a6b321c…  │ 0x00000000000000000000000008903a3be1e…  │ 0x000000000000000000000000abec00542d141bddf58649bfe860c6449807237c │ 9748415873909063929026   │
│ 0xabec00542d141bdd…  │    21104078 │ 0x1bd4d5006a6b321c…  │ 0x00000000000000000000000008903a3be1e…  │ 0x00000000000000000000000060a8ea6005f7db580bc0c9341e7e6275d114e874 │ 965093171516997328973575 │
│ 0xc02aaa39b223fe8d…  │    21104078 │ 0x1bd4d5006a6b321c…  │ 0x00000000000000000000000060a8ea6005f…  │ 0x0000000000000000000000003fc91a3afd70395cd496c647d5a6cc9d4b2b7fad │ 14935959444018469899     │
│ 0xc02aaa39b223fe8d…  │    21104078 │ 0x1bd4d5006a6b321c…  │ 0x0000000000000000000000003fc91a3afd7…  │ 0x000000000000000000000000000000fee13a103a10d593b9ae06b3e05f2e7e1c │ 37339898610046174        │
│ 0xc02aaa39b223fe8d…  │    21104078 │ 0xe391af23df899353…  │ 0x000000000000000000000000abd055069a6…  │ 0x0000000000000000000000001f2f10d1c40777ae1da742455c65828ff36df387 │ 910473774728478721       │
│ 0xc02aaa39b223fe8d…  │    21104078 │ 0xe391af23df899353…  │ 0x0000000000000000000000001f2f10d1c40…  │ 0x00000000000000000000000060a8ea6005f7db580bc0c9341e7e6275d114e874 │ 173454427502411776       │
├──────────────────────┴─────────────┴──────────────────────┴─────────────────────────────────────────┴────────────────────────────────────────────────────────────────────┴──────────────────────────┤
│ 10 rows                                                                                                                                                                                   6 columns │
└─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```
