# Data Compression and Archiving

## zlib — Compression compatible with gzip

### Checksums

adler32(data) & 0xffffffff
crc32(data[, value])

### Compress

`zlib.compress(data[, level])` compresses and returns `bytes` data. The second parameter allows compression from level 0 (no compression) to 9 (maximum compression), trading CPU time for better compression.

`zlib.compressobj([level])` returns a streaming compress object which can allow compression of larger amounts which don't fit in memory. (Note there are more params but the defaults should be OK in most cases).

For example:

```python
co = zlib.compressobj(level=9)

with open('demo_out.zlib', 'wb') as f:
    for x in range(1000000):
        compressed_data = co.compress(b'lorem ipsum ')
        f.write(compressed_data)
    
    # Make sure the last bit is written!
    f.write(compressobj.flush())
```

### Decompress

`zlib.decompress(data)`

decompressobj(wbits=MAX_WBITS[, zdict])
decompress
flush
copy

## gzip — Support for gzip files
## bz2 — Support for bzip2 compression
## lzma — Compression using the LZMA algorithm
## zipfile — Work with ZIP archives
## tarfile — Read and write tar archive files
