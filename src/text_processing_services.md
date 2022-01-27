# Text Processing Services

## string — Common string operations

This module used to be used for more string operations in early versions of python (like `string.join(iterable)`) but is now mainly useful for the constants:

* `ascii_letters`: `'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'`
* `ascii_lowercase`: `'abcdefghijklmnopqrstuvwxyz'`
* `ascii_uppercase`: `'ABCDEFGHIJKLMNOPQRSTUVWXYZ'`
* `digits`: `'0123456789'`
* `hexdigits`: `'0123456789abcdefABCDEF'`
* `octdigits`: `'01234567'`
* `punctuation`: `'!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'`
* `printable`: `'0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ \t\n\r\x0b\x0c'`
* `whitespace`: `' \t\n\r\x0b\x0c'`

There is also a string `Template` class, but personally I prefer the templating functions inbuilt to the `str` type such as `'%s' % s` or `f'{s}'`.

## re — Regular expression operations

## difflib — Helpers for computing deltas

## textwrap — Text wrapping and filling

## unicodedata — Unicode Database

* `lookup(name)`
* `name(chr[, default])`
* `decimal(chr[, default])`
* `digit(chr[, default])`
* `numeric(chr[, default])`
* `category(chr)`
* `bidirectional(chr)`
* `combining(chr)`
* `east_asian_width(chr)`
* `mirrored(chr)`
* `decomposition(chr)`
* `normalize(form, unistr)`
* `is_normalized(form, unistr)`
* `unidata_version`

## stringprep — Internet String Preparation

## readline — GNU readline interface

## rlcompleter — Completion function for GNU readline
