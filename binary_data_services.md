# Binary Data Services

## struct — Interpret bytes as packed binary data

The `struct` module allows reading and writing binary data. Similar to the `re` module, it can be used with either encoder/decoder instances or directly with functions. I'll only show the former here to keep things brief (and because I think coding using instances is cleaner, as you can put the format at the top of the file). See also https://docs.python.org/3/library/struct.html#byte-order-size-and-alignment for byte order characters and the C data type characters.

Note that binary data on different platforms and architectures isn't guaranteed to be the same size, and the byte order may be either big or little-endian. In the below case, we're using network order (big-endian) by using the "!" character with "i", or a `signed int`.

```python
import struct

enc_dec = struct.Struct("!i")
print(enc_dec.size) # -> 4 (indicating 4 bytes) on my PC, may not always be the same 
                    #    on others though I think it normally will be the same.

encoded = enc_dec.pack(5)
print(encoded) # -> b'\x00\x00\x00\x05'

decoded = enc_dec.unpack(encoded)
print(decoded) # -> (5,)
```

This can be useful for fast, efficient data retrieval (in many cases faster than using a DB for things like time-series data), and I often use it in combination with the `mmap` module for memory-backed disk retrieval.

## codecs — Codec registry and base classes

I think I have never used this module directly, but the "standard encodings" table is useful for decoding data which is in different encodings: https://docs.python.org/3/library/codecs.html#standard-encodings.

For example, I have some dictionary data which is in the "shift-jis" encoding, and I can see from that table there are 3 selections: `shift_jis`, `shift_jis_2004` and `shift_jisx0213`. From there, I can open the file by doing something like the following:

```python
with open(path, 'r', encoding='shift_jis') as f:
    data = f.read()
```
