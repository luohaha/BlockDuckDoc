---
icon: power-off
---

# Quickstart

### Install DuckDB

First, you need to install DuckDB first, it is pretty easy, you can check this: [duckdb](https://duckdb.org/docs/installation/?version=stable\&environment=cli\&platform=macos\&download_method=package_manager).

DuckDB is an in-process database system and offers client APIs for several languages: [clients api overview](https://duckdb.org/docs/api/overview).

The compatibility between BlockDuck and BlockDB varies across versions. Refer to the list below to identify the correct BlockDB version compatible with your chosen BlockDuck.

| Version of BlockDuck | Version of DuckDB |
| -------------------- | ----------------- |
| v0.5.0               | v1.1.3            |
| v0.6.0               | v1.2.0            |

### Install BlockDuck

BlockDuck is one of available DuckDB community [extensions](https://duckdb.org/community_extensions/list_of_extensions) , so we can use `INSTALL`and `LOAD`  to install it easily.

```
INSTALL blockduck FROM community;
LOAD blockduck;
```

Next, we can verify whether the installation was successful by querying the version.

```
D select * from blockduck_version();
┌─────────┐
│ version │
│ varchar │
├─────────┤
│ v0.6.0  │
└─────────┘
```

###

