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
specification and as exactly as possible, 
including unspecified behaviours such as:

- `.r` when popped value is non-positive
- zero-division

This implementation aborts when it tries to do 
unspecified behaviour.

# Assumed usage
```sh
pxemc.posixism /path/to/pxem/program > a.awk \
  && pxemx.posixism a.awk
```

The Pxem program file has to be a regular file 
with readable permission (if and only if your
file name contains one of these commands: `.f`, 
`.e`; otherwise the existence of file is not 
checked). The program is assumed to be written 
in ASCII-compatible encoding. Additionally, the 
command substrings are case-insensitive; two 
programs such as `hi.p` and `hi.P` are 
semantically same.

The compiled program assumes that you are using 
POSIX-compatible locale: the `._` command, which 
stands for `scanf("%d",&value)` ignores leading 
blank characters (which are 0x09-0x0d and 0x20). 

# License
CC0.
