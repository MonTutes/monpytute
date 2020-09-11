# Data Compression and Archiving

## zlib — Compression compatible with gzip


adler32(data) & 0xffffffff
compress(data, level=-1) 0 to 9

compressobj(level=-1, method=DEFLATED, wbits=MAX_WBITS, memLevel=DEF_MEM_LEVEL, strategy=Z_DEFAULT_STRATEGY[, zdict])

compress(data)
flush([mode])
copy()

crc32(data[, value])
decompress(data, wbits=MAX_WBITS, bufsize=DEF_BUF_SIZE)

decompressobj(wbits=MAX_WBITS[, zdict])
decompress
flush
copy


## gzip — Support for gzip files
## bz2 — Support for bzip2 compression
## lzma — Compression using the LZMA algorithm
## zipfile — Work with ZIP archives
## tarfile — Read and write tar archive files
