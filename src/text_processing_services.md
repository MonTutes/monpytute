# Text Processing Services

## string — Common string operations

This module used to be used for more string operations in early versions of python (like `string.join(iterable)`) but is now mainly useful for the constants:

* `string.ascii_letters`: `'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'`
* `string.ascii_lowercase`: `'abcdefghijklmnopqrstuvwxyz'`
* `string.ascii_uppercase`: `'ABCDEFGHIJKLMNOPQRSTUVWXYZ'`
* `string.digits`: `'0123456789'`
* `string.hexdigits`: `'0123456789abcdefABCDEF'`
* `string.octdigits`: `'01234567'`
* `string.punctuation`: `'!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'`
* `string.printable`: `'0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ \t\n\r\x0b\x0c'`
* `string.whitespace`: `' \t\n\r\x0b\x0c'`

There is also a string `Template` class, but personally I prefer the templating functions inbuilt to the `str` type such as `'%s' % s` or `f'{s}'`.

## re — Regular expression operations

## difflib — Helpers for computing deltas

## textwrap — Text wrapping and filling

## unicodedata — Unicode Database

* `unicodedata.lookup(name)`
* `unicodedata.name(chr[, default])`
* `unicodedata.decimal(chr[, default])`
* `unicodedata.digit(chr[, default])`
* `unicodedata.numeric(chr[, default])`
* `unicodedata.category(chr)`
* `unicodedata.bidirectional(chr)`
* `unicodedata.combining(chr)`
* `unicodedata.east_asian_width(chr)`
* `unicodedata.mirrored(chr)`
* `unicodedata.decomposition(chr)`
* `unicodedata.normalize(form, unistr)`
* `unicodedata.is_normalized(form, unistr)`
* `unicodedata.unidata_version`

## stringprep — Internet String Preparation

## readline — GNU readline interface

## rlcompleter — Completion function for GNU readline
