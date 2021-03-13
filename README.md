# pxem.posixism
Pxem implementation in POSIXism.

# Summary
This is an implementation of Pxem, an esoteric 
programming language designed by 「ぬこ」 
(or "nk.") with POSIX-compatible shell language 
with POSIX-compatible utilities.

**pxem.posixism** consists of two programs: 
**pxemc.posixism** --- Pxem-to-awk compiler 
--- and **pxemx.posixism** --- interpreter for 
compiled program.

This implementation tries to comply the original 
specification and as well as possible, including 
unspecified behaviours, such as:

- `.r` when popped value is non-positive
- zero-division

# Assumed usage
```sh
pxemc.posixism /path/to/pxem/program > a.awk \
  && pxemx.posixism a.awk
```

# License
CC0.
