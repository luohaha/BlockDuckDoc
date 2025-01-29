---
icon: eye
---

# Contract view function

### What is contract view function

A contract view function is a type of function in a blockchain smart contract that allows users to view or read the state of the contract without making any modifications. These functions are non-mutating, meaning they do not change any state on the blockchain and do not require any gas fees for execution. They are typically used to retrieve information from a contract, such as balances or stored data.

The view functions in contracts allow you to read the state of the smart contract, and we can create table functions to analyze them.

### How to create

E.g. If we want to create table function for ERC20 **`balanceOf`** view function:

```
    /**
     * @notice Get the number of tokens held by the `account`
     * @param account The address of the account to get the balance of
     * @return The number of tokens held
     */
    function balanceOf(address account) external view returns (uint) {
        return balances[account];
    }
```

Its JSON ABI is:

```json
{
 "constant":true,
 "inputs":[
   {"internalType":"address","name":"account","type":"address"}
  ],
 "name":"balanceOf",
 "outputs":[
   {"internalType":"uint256","name":"","type":"uint256"}
  ],
  "payable":false,
  "stateMutability":"view",
  "type":"function"
}
```

Create a table function for `balanceOf`:

```
pragma blockduck_create_contract_view_rpc(balanceOf, '{"constant":true,"inputs":[{"internalType":"address","name":"account","type":"address"}],"name":"balanceOf","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"}');
```

#### **inputs**

| Args       | Types   | Info                                                |
| ---------- | ------- | --------------------------------------------------- |
| suffix     | VARCHAR | Table function suffix to identify the specific view |
| event\_abi | VARCHAR | JSON ABI of the view function to be monitored       |

#### **examples**

```
D pragma blockduck_create_contract_view_rpc(balanceOf, '{"constant":true,"inputs":[{"internalType":"address","name":"account","type":"address"}],"name":"balanceOf","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"}');
┌─────────┐
│ Success │
│ boolean │
├─────────┤
│ 0 rows  │
└─────────┘
```

### How to query

After that, table function named `eth_contract_view_rpc_balanceOf` already been created. Then you can try to query from it.

#### **Inputs**

| Args      | Types         | Info                                                |
| --------- | ------------- | --------------------------------------------------- |
| address   | LIST(VARCHAR) | Contract address emitting the event                 |
| fromBlock | BigInt        | Block number to start scanning from                 |
| toBlock   | BigInt        | Block number to stop scanning at                    |
| arg0      | ...           | ...                                                 |
| ...       | ...           | ...                                                 |
| argn      | ...           | inputs of the view function. Must be '0x' prefixed. |
| url       | VARCHAR       | URL of the Ethereum node                            |

#### **Examples**

```
set variable eth_url = 'https://eth-mainnet.g.alchemy.com/v2/_VAP1LMRwnhUbKarsWEtC_nYZk-yHPEm';
select * from eth_contract_view_rpc_balanceOf(['0x1f9840a85d5aF5bf1D1762F925BDADdC4201F984']::varchar[], 21104077, 21104078, '0xD66428f5754db6126059314275676B2820e09135', getvariable('eth_url'));
┌────────────────────────────────────────────┬──────────┬──────────────────────┐
│                  address                   │  block   │      balanceOf0      │
│                  varchar                   │  int64   │        varint        │
├────────────────────────────────────────────┼──────────┼──────────────────────┤
│ 0x1f9840a85d5aF5bf1D1762F925BDADdC4201F984 │ 21104077 │ 0                    │
│ 0x1f9840a85d5aF5bf1D1762F925BDADdC4201F984 │ 21104078 │ 20166875074384524618 │
└────────────────────────────────────────────┴──────────┴──────────────────────┘
```
