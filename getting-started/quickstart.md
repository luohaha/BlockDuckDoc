---
icon: bullseye-arrow
---

# Quickstart

### Install DuckDB

First, you need to install DuckDB first, it is pretty easy, you can check this: [duckdb](https://duckdb.org/docs/installation/?version=stable\&environment=cli\&platform=macos\&download_method=package_manager).

DuckDB is an in-process database system and offers client APIs for several languages: [clients api overview](https://duckdb.org/docs/api/overview).

The compatibility between BlockDuck and BlockDB varies across versions. Refer to the list below to identify the correct BlockDB version compatible with your chosen BlockDuck.

| Version of BlockDuck | Version of DuckDB |
| -------------------- | ----------------- |
| v0.5.0               | v1.1.3            |
|                      |                   |

### Install BlockDuck

#### Download

* v0.5.0

| Arch               | Download link                                                                                  |
| ------------------ | ---------------------------------------------------------------------------------------------- |
| linux\_amd64       | [Download](https://github.com/luohaha/BlockDuck/actions/runs/13072373614/artifacts/2516580766) |
| linux\_amd64\_gcc4 | [Download](https://github.com/luohaha/BlockDuck/actions/runs/13072373614/artifacts/2516579944) |
| linux\_arm64       | [Download](https://github.com/luohaha/BlockDuck/actions/runs/13072373614/artifacts/2516584526) |
| osx\_amd64         | [Download](https://github.com/luohaha/BlockDuck/actions/runs/13072373614/artifacts/2516542999) |
| osx\_arm64         | [Download](https://github.com/luohaha/BlockDuck/actions/runs/13072373614/artifacts/2516544254) |



### Load BlockDuck

* CLI

For now, because BlockDuck isn't signed yet, we need to add `-unsigned` to enable load unsigned extension.

```
./build/release/duckdb -unsigned
```

And then load BlockDuck:

```
LOAD '/path/to/extension/blockduck.duckdb_extension';
```

* Python

To ensure that the BlockDuck extension is loaded correctly in your DuckDB environment, follow these steps. Make sure you specify the necessary configuration to allow unsigned extensions. This can be achieved by setting `allow_unsigned_extensions` to `true` when connecting to your database in Python. Then, use the `load_extension` method to load the BlockDuck extension from its specified path. Here's how you can do it:

1.  **Connect to the Database with Configuration:**

    When connecting to your DuckDB database, make sure to include the configuration option `{"allow_unsigned_extensions": "true"}` to permit loading unsigned extensions.
2.  **Load the Extension:**

    After establishing the connection, use the `load_extension` method to load the BlockDuck extension into the DuckDB environment.

```python
import duckdb

con = duckdb.connect(database = "file.db", config = {"allow_unsigned_extensions": "true"})
con.load_extension("./build/release/extension/blockduck/blockduck.duckdb_extension")
```

