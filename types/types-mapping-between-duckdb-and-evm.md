# Types Mapping between DuckDB and EVM

## Types Mapping

| **Ethereum ABI Type**                       | **DuckDB Logical Type**                                              |
| ------------------------------------------- | -------------------------------------------------------------------- |
| `address`                                   | `VARCHAR`                                                            |
| `bool`                                      | `BOOLEAN`                                                            |
| `bytes`                                     | `VARCHAR`                                                            |
| `string`                                    | `VARCHAR`                                                            |
| `uint8`, `uint16`, `uint24`, ..., `uint256` | `UBIGINT` (<=64 bits), `UHUGEINT` (<=128 bits), `VARINT` (>128 bits) |
| `int8`, `int16`, `int24`, ..., `int256`     | `BIGINT` (<=64 bits), `HUGEINT` (<=128 bits), `VARINT` (>128 bits)   |
| `bytes1`, `bytes2`, ..., `bytes32`          | `VARCHAR`                                                            |

Currently, we don't support array or tuple type yet, will be supported in the future.
