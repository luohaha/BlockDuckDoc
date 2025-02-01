---
icon: shapes
---

# How to build

### Clone repo

```
git clone --recurse-submodules git@github.com:luohaha/BlockDuck.git
```

> `--recurse-submodules` is need because BlockDuck has two submodules.

### Managing dependencies

Currently, BlockDuck have only one dependency which is `openssl`. And we use [VCPKG](https://vcpkg.io/en/getting-started) to manage this dependency. You can run the following cmds to install and enable `VCPKG`.

```shell
cd <your-working-dir-not-the-plugin-repo>
git clone https://github.com/Microsoft/vcpkg.git
sh ./vcpkg/scripts/bootstrap.sh -disableMetrics
export VCPKG_TOOLCHAIN_PATH=`pwd`/vcpkg/scripts/buildsystems/vcpkg.cmake
```

### Compile

Then we can use `make` to build the extension:

```
make
```

The BlockDuck extension binary will be:

```
./build/release/extension/blockduck/blockduck.duckdb_extension
```

### Tests

In BlockDuck, there are two types of test cases. One is inherited from DuckDB's `sqllogictest`, and the other is the internal `unittest` of BlockDuck.

**Sqllogictest**

run sqllogictest:

```
make test
```

**UnitTest**

build and run unittest:

```shell
cd unittest/
cmake .
make
./BlockDuckTests
```

