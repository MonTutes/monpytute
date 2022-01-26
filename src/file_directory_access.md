# File and Directory Access

## pathlib — Object-oriented filesystem paths

Path

cwd
home
stat
chmod
exists
expanduser
glob
group
is_dir
is_file
is_mount
is_symlink
is_socket
is_fifo
is_block_device
is_char_device
iterdir
lchmod
lstat
mkdir
open
owner
read_bytes
read_text
rename
replace
resolve
rglob
rmdir
samefile
symlink_to
touch
unlink
link_to
write_bytes
write_text

## os.path — Common pathname manipulations

## fileinput — Iterate over lines from multiple input streams

## stat — Interpreting stat() results

## filecmp — File and Directory Comparisons

## tempfile — Generate temporary files and directories

## glob — Unix style pathname pattern expansion

## fnmatch — Unix filename pattern matching

The `re` module supports more advanced matching, but a lot of the time simpler wildcard matching of strings ("\*" for multiple characters or "?" for a single character) is adequate. 

Although this module is listed under "File and Directory Access", this can be used for many things.

```python
import re
import fnmatch

# Case-insensitive match: fnmatch
print(fnmatch.fnmatch("Dog", "do*")) # -> True
print(fnmatch.fnmatch("cat", "do*")) # -> False

# Case-sensitive match: fnmatchsensitive
print(fnmatch.fnmatchcase("Dog", "do*")) # -> False
print(fnmatch.fnmatchcase("dog", "do*")) # -> True

# Case-insensitive match in list: filter
print(fnmatch.filter(["Dog", "cat"], "do*")) # -> ["Dog"]

# Convert pattern to regular expression string: translate
pattern = fnmatch.translate("quick*")
print(pattern) # -> (?s:quick.*)\Z
re_inst = re.compile(pattern, re.IGNORECASE)
print(re_inst.match('quickly')) # -> <_sre.SRE_Match object; span=(0, 7), match='quickly'>
```

## linecache — Random access to text lines

## shutil — High-level file operations
