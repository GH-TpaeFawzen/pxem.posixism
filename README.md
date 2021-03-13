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
specification and as exactl yas possible, 
including unspecified behaviours such as:

- `.r` when popped value is non-positive
- zero-division

# Assumed usage
```sh
pxemc.posixism /path/to/pxem/program > a.awk \
  && pxemx.posixism a.awk
```

The Pxem program file has to be a regular file 
with readable permission. The program is assumed 
to be written in ASCII-compatible encoding.

The compiled program assumes that you are using 
POSIX-compatible locale: the `._` command, which 
stands for `scanf("%d",&value)` ignores leading 
blank characters (which are 0x09-0x0d and 0x20). 

# License
CC0.
