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

Though small, the in-process sqlite database has a large number of the features you'd expect from a full-blown client/server such as MySQL.
Note that the below code isn't threadsafe, and you must call "commit", otherwise changes won't be written to disk.

Just like the `shelve` module, the below code only supports string keys. I've used the `json` module to serialize data, which is more secure than `pickle` although doesn't support doing things like encoding a `dict` with non-string keys.

I'd often use something like the following:

```python
import json
import sqlite3
from os.path import exists

class ShelveReplacement:
    def __init__(self, path):
        # Note "path" can be ":memory" for a fast in-memory storage (which is lost on exit)
        already_exists = exists(path)
        self.con = sqlite3.connect(path)
        
        # Enable write-ahead logging
        # Please see https://www.sqlite.org/wal.html for more info before using this!
        self.con.execute('PRAGMA journal_mode=WAL;')
        
        if not already_exists:
            self.con.execute('CREATE TABLE my_data(key TEXT NOT NULL PRIMARY KEY, value TEXT NOT NULL);')
            self.con.commit()
    
    def commit(self):
        # Make sure changes are written to disk
        self.con.commit()
    
    def close():
        self.commit()
        self.con.close()
    
    def __iter__(self):
        # Allow "for key in my_shelve_replacement: ..."
        for key, in list(self.con.execute('SELECT key, value FROM my_data')):
            yield key, value
    
    def __setitem__(self, key, value):
        # Note the use of the "?" character to prevent SQL injection vulnerabilities!
        self.con.execute('REPLACE INTO my_data (key, value) VALUES (?, ?);', (key, json.dumps(value)))
        
    def __getitem__(self, key):
        for value, in self.con.execute('SELECT value FROM my_data WHERE key = ?;', (key,))
            return json.loads(value)
        raise KeyError(key) # Not found!
        

if __name__ == '__main__':
    db = ShelveReplacement('demo_db.sqlite')
    db['my_key'] = 'my_value'
    print(db['my_key'])
    for my_key in db:
        print(my_key, db['my_key'])
    db.close()
    
    db = ShelveReplacement('demo_db.sqlite')
    print(db['my_key'])
    db['my_key'] = 'my_new_value'
    print(db['my_key'])
    db.close()
    
