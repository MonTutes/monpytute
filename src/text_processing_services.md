# Text Processing Services

## string — Common string operations

This module used to be used for more string operations in early versions of python (like `string.join(iterable)`) but is now mainly useful for the constants:

* `ascii_letters`: `'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'`
* `ascii_lowercase`: `'abcdefghijklmnopqrstuvwxyz'`
* `ascii_uppercase`: `'ABCDEFGHIJKLMNOPQRSTUVWXYZ'`
* `digits`: `'0123456789'`
* `hexdigits`: `'0123456789abcdefABCDEF'`
* `octdigits`: `'01234567'`
* `punctuation`: ``'!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'``
* `printable`: ``'0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ \t\n\r\x0b\x0c'`` 
* `whitespace`: `' \t\n\r\x0b\x0c'`

There is also a string `Template` class, but personally I prefer the templating functions inbuilt to the `str` type such as `'%s' % s` or `f'{s}'`.

## re — Regular expression operations

## difflib — Helpers for computing deltas

## textwrap — Text wrapping and filling

## unicodedata — Unicode Database

* `lookup(name)`: Find a character by its unicode name. For example `lookup('RED APPLE')` will give the character `🍎` and `lookup('LATIN CAPITAL LETTER A')` will give `'A'`.
* `name(chr[, default])`: Find the name of a given character. For example `unicodedata.name('ç')` will give `'LATIN SMALL LETTER C WITH CEDILLA'`.
* `decimal(chr[, default])`, `digit(chr[, default])` or `numeric(chr[, default])`: Find the decimal/digit/numeric value of a given character. For some characters, e.g. `'9'` this will give the value as an int of `9` for both `decimal('9')` and `digit('9')`. `numeric('9')` and `numeric('¼')` will give floating point values of `9.0` and `0.25` respectively.  
* `category(chr)`, `bidirectional(chr)`, `combining(chr)`, `east_asian_width(chr)`, `mirrored(chr)`: return the relevant value from the unicode character database. See also tables `General_Category`, `Bidi_Class`, `Canonical_Combining_Class`, `East_Asian_Width`, `Bidi_Mirrored` properties at http://www.unicode.org/reports/tr44/.
* `decomposition(chr)`
* `normalize(form, unistr)`
* `is_normalized(form, unistr)`
* `unidata_version`

## stringprep — Internet String Preparation

## readline — GNU readline interface

## rlcompleter — Completion function for GNU readline
