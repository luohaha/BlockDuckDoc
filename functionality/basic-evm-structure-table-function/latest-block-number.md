---
icon: block
---

# Latest Block Number

### Table function

The **eth\_latest\_block\_rpc** table provides the latest block number of EVM chains.

### **Inputs**

| Args     | Types   | Info                     |
| -------- | ------- | ------------------------ |
| rpc\_url | VARCHAR | URL of the Ethereum node |

### **Ouputs**

| Column Name | Type   | Description              |
| ----------- | ------ | ------------------------ |
| number      | BIGINT | The latest block number. |

### **Examples**

```
D set variable eth_url = 'https://eth-mainnet.g.alchemy.com/v2/_VAP1LMRwnhUbKarsWEtC_nYZk-yHPEm';
D select * from eth_latest_block_rpc(getvariable('eth_url'));
┌──────────────┐
│ latest_block │
│    int64     │
├──────────────┤
│     21623511 │
└──────────────┘
```
