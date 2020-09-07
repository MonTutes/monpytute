# Data Persistence

## copyreg — Register pickle support functions



## shelve — Python object persistence

Some python tutorials use this module. I don't ever use it myself, as it uses the `dbm` module for storage. The `dbm` module used to use the Berkeley DB as its backend, however due to licensing changes it was removed from python 3, and which backend you get depends on what your system provides. 

I recommend using something like [plyvel](https://plyvel.readthedocs.io/en/latest/) for Google's LevelDB or [python-rocksdb](https://python-rocksdb.readthedocs.io/en/latest/) for Facebook's RocksDB for fast, space-efficient key/value storage. Simply using `sqlite3` below is also a good choice, as it is small, fast (even if not as fast as LevelDB/RocksDB) and comes default with most python installations.

```python
import shelve

db = shelve.open("test.shelve")
db["test key"] = "test data"
db.close()

db = shelve.open("test.shelve")
data = db["test key"]
print(data) # -> "test data"
db.close()
```

## marshal — Internal Python object serialization

This module allows for very fast encoding/decoding of basic python types to binary data. It may be slightly faster than `pickle`, however the format isn't guaranteed to stay the same across python releases, and it doesn't support encoding some kinds of python objects. 

This module might be slightly less insecure than `pickle`, but <b>should still be considered insecure</b>, especially for untrusted input.

I normally would prefer the `json` or similar modules unless I need something like `tuple`s as `dict` keys (as the `json` module only supports strings as keys in objects), as it's fast enough for a vast majority of uses (and much more secure).

```python
from marshal import loads, dumps

print(loads(dumps({"my object": "out", (1, 2, 3): 4})))
# -> {'my object': 'out', (1, 2, 3): 4}
```

## dbm — Interfaces to Unix “databases”

I never use this, for the reasons I detail under the `shelve` heading above.

## sqlite3 — DB-API 2.0 interface for SQLite databases
