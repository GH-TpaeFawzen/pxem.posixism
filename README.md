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
## On terminal
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

## On tio.run
[Try it here!](https://tio.run/##nRj7V9pI9/f9K4ZZHjNACCC2lmF0FW2XVqmrbrcVWE@EINGQAAkKAv3X@907SSC4fmcfx3PIzJ079/0ae4Y3@PEzqdUGvj/yqrp@Z/mD6W2h6w71D79qVyPDfG88PZuOPpqZw8LI9ayZ5Q31W9u91YeGFcCtQrkwtJz18f7@T57pE82ciunQ8B5IsVguC3M2cic@Oa3fHJ6eyrpg/nxkkjvT77pOP51WO@A7NJwe39d75qPuTG2blPfTpXQ6vHx@ePWrpEkW4hFtFBFQRzy5wE@uugoW2opGbH9vNr7eXF4dy3KxuBMBzz9fNr6efrupf764OKlfyZJoEc0hNLk4Orz89ebLycVl43OzCmRIJ51eEKWVS5SeAje5I7Fa37l@7Yo5nNqGbxJvgBfckQ@rJ3fS80a25QvDtgyPaHckk1yUcjT5C11lZAa/GdH8/fS0fnYsq4oFKI0Me8IbWH1fMe8RRAwBZnfgkuTPnBJJSsiaKYg3MMGGvusS1@7tp9ELlk9KXJiPhk1ogvQN2zPpcvkKOonjKwkUzmzpmT2S8fSZPteFBz/PekbxfSad5RJUVpQA5y9sQROwgP0o370T4MKRZZuMs74siq7hmcChRInlENbPctIHbwjTM7rC8DxzeGvP0fEu@PzQIdqjPy0t/QnR6h4plso7ld03b/fekUyr7WQ7meXdxByRwtJ4eiCZo5MPjebCBiY9WXkjwLpsNLEcv08yo3P3s9O0Gjfdunf5@KX/3jyZXDz9Mfs6//Z8bRz6V8Oz3nFOSyRTqczyP7BOFiWttyhJFgntyDalYBLbfTInzAtEYDTVpflkkXNC21RQAYbMqNBglOYv87RKuUDR@9KTlIq@O2ECIt62HJP094uCL6w@iwBeTRa5wgOgh5asp9N9KXt8ccK4UCxJveV1xMoErxPEUqdPA/REsD5lfY7sxEvCwQkSUs4sitVqzeavDBSH4Mop8zgAEGPVnzpd33Idcsq6SvZuAuTlnm90H1p2LteR3RgSXEEcmy9Cj1E7tIENutuaxiM4/IU0tFInFATssFpllCe0R@JC@Kjgo1FIBFqHOu6Dgk5O6q2n2fy5o2u6oaMFnFoxZE4LBjmqkEKAQJe0a0BEQ2zTdXArPPA1C6gYHf2Akl9ANCcH5KqgJ5J0lU56T0@nEw4PbRlA@GIqHa0kAsmc/WncvcoHoSiBEORJd0nBeFWWl7oEwlEDbYJ@c/4FrcCczQt1tjmBCIBwFaELUl67jWUwyla6ZC0SWJxotk/KWJTg/jJyiCGL@IF4TfYprgYAyHhZsN7Idbre48Tv6Flm1Eo8p7dykIRasC9zcJU588VKH@kLICM8qBUrr1YKwQNYDUB/X88mEoZYLTyZ0Ft9M3SKMNA21k1Hz@k2UGy@14AFMyAEgHkX7NVyHQ@YA3CAQH2oa3BcglUkh1iVIFdfqLizpWJmcd6ycsWOTIJ7czkxkrDXypAbo@8Qx@k0MF8EIDkKInh66/kTlizmd7jombYJfeO8pWlWRwSKwcU/bdL6k3RyeL@rL@AKowqQpHmaJmmaD0j@LYEkUvD0haXJ8gvc/3PTDm8onmTN9B9z3AgeWREyALydTOEKEBkpLkkxQONJyhcu2g6K6EjMZLL5XpC5TAbuEjEh4qKMOOK7mE@zmpzzxY2cweW5mMsbsdqyNkQt09s5/WCWm1fB6QczDb4J@Gbhm4Jval6FHve6XifN4wVWonsIv/uaJe5zuaAYAdp9BzMjapNQAQrZpK5nAoAO5gAb6jr2TpQ8q5@zNBf6HewJTGDiFtqkygHrBrKgb078YQfsrqehgOrCF1FeAygoFHDAF@rEQOBKLXu4xGaHnbu/HgtUc85g/rIizyyXwb4HpCemP5042IACLjkkYPR6EVcN996tH@0TuIfpJtq3kwjoWY8RIKUQ3IiApxey@h9X7xlNQyEEc7yQbN2Vg@p82XqQkDyQ3FE7HATtMAPDgh9VnQwaerm@uu4cJjviiwfIOiDTkfCDbQH9dQQUj2oIFUfgMljkj0IEWLwgjqIDA67afY9AgeMCUtvrTqyRL0NBsQmaZu87LUAfm8BUqrbxXnfOjjnqk//EeEceK5lAtO0@F5g/8WmrS35cHxA42C/Fjj5tjpQ2m5OrrRNkispvzr@yC764kICmJNG00PXkIoY0ZfWwQzCtVIM5ol4r777hB/UqttU12gekBRaYOt/1go5kp46YOjiDbIiGq3WnPUgWq1pcl9@RGdyqx2CH7CxqUYe3MKxXIWXPXutO6xsjFk0yCTAon7Kv8Bs7d4Np4vVDhzXy4/xx3t7gLMYSkGD8sk3nzh@wMVcR1IBm06hJWzQgfqaMHcuwbo/zjXyJ8@@0VdTedejBca6yV63s4uyzZmOBDOfswzbvG3aWr@ev89/44kzSwk2VNF0f65N5Z06oqEvAF9fAVo0@wcxXeRs4ZXeP305M4wErXh1qbaW1s9vB2nktKxWtHl4OULDvs73gXqkC3a0u5Q520wAJnlG@5UxNsULbB9j1WmUPEfd333KuwEqGDfeAAf8mvxFW1wBZoDPFObvOfovr2I0Z/5xdbRvAix1@3UqAR3DLff4LV7UWTF@EbL@XKqTBCfeCoROgdtzDLMgXXzCR842OCD5qdx/s7jvyS9wRkxhLXEzgUec69jydBtlw1DpktDCpElhSVAcTQSU3z2LkbDn1aZNwQA7KEWAkgERMjxn7LT8OOEJO8xC7JH5TIRYEWgj8rTaOXZz/i4v78YvPa6FYcDWSKxR/jejHLDHAarntgWFw/IBz/gBchyjx8x56KI4SdkvEEw9QXLY8p0pVA@tvDmqS8h7IdR98grrIeegvhYTe3DBT7Qh5fVRhBJLmXuQxNqjGGgVyDVgDioZoteKB1qg2tnynGtgWxewLitjRxmFd@BhGC1OGh3HRVl8ZxkuySq7NiZtYR8x43z4Y63bV1secx7lCV/yHNFOv0kwBzZSiiS3@x/vm4dmJ/Kn@uXl10rySP6JnUVIdULIk4XOb9OHHMYYmSad/WmOF9@J4WAxMmGZiaGvp@2Cx9SN6c/s/vpCbF2ocg0kPJiT8r4z2QErOJF@KBqg/VT3NkjYrZNs8CeNSu4QDBF9ReH5gs5VqzNG6RP3baIp56g5xpgDg5C/AjZi9CtGalS0EHCY8OHfJyOrlTd8amvlRdzTNP3rPomf4Jo@rWfl7NX3DsonmVMqROqAEK7QXe@0VKtMu6ZnNi0grlypvK3s7byp78H6AdwpYRY2awWhpBC@uf29nfGcFdsIPxWdaNMbQCGEs2xn8fr64lJlMNIZh9lowM1nY/vEdw7stqyPX/79ot1MuzVuQMM2L1G5RylIoq0fo@nE@hhfamNC2A6NDeNxtJYudQDccoMLZOUKCSBgQzfvxPw)

- Initialize two variables `FNAME` and `CONTENT` to pass program name.
- Both of they are passed to `printf` once.
- Size of each of them are shown on Debug section.
- Let me know if you found any bugs.

# License
CC0.
