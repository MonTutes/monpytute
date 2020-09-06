# Binary Data Services

## struct — Interpret bytes as packed binary data

The `struct` module allows reading and writing binary data. Similar to the `re` module, it can be used with either encoder/decoder instances or directly with functions. I'll only show the former here to keep things brief (and because I think coding using instances is cleaner, as you can put the format at the top of the file). See also https://docs.python.org/3/library/struct.html#byte-order-size-and-alignment.

Note that binary data on different platforms and architectures isn't guaranteed to be the same size, and the byte order may be either big or little-endian. In the below case, we're using network order (big-endian) by using the "!" character.

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
