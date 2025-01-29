---
icon: bullseye-arrow
---

# Quickstart

### Install DuckDB

First, you need to install DuckDB first, it is pretty easy, you can check this: [duckdb](https://duckdb.org/docs/installation/?version=stable\&environment=cli\&platform=macos\&download_method=package_manager).

DuckDB is an in-process database system and offers client APIs for several languages: [clients api overview](https://duckdb.org/docs/api/overview).



### Install BlockDuck

#### Download

| Arch               | Download link                                                                                  |
| ------------------ | ---------------------------------------------------------------------------------------------- |
| linux\_amd64       | [Download](https://github.com/luohaha/BlockDuck/actions/runs/12850432645/artifacts/2452167290) |
| linux\_amd64\_gcc4 | [Download](https://github.com/luohaha/BlockDuck/actions/runs/12850432645/artifacts/2452170472) |
| linux\_arm64       | [Download](https://github.com/luohaha/BlockDuck/actions/runs/12850432645/artifacts/2452145936) |
| osx\_amd64         | [Download](https://github.com/luohaha/BlockDuck/actions/runs/12850432645/artifacts/2452142020) |
| osx\_arm64         | [Download](https://github.com/luohaha/BlockDuck/actions/runs/12850432645/artifacts/2452138398) |



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

