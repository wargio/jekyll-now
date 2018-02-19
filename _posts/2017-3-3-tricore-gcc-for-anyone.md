---
layout: post
title: Tricore GCC for everyone
---

To skip the registration check on the `2017.01` version (toolchain `v4.9.1.0`) you need to patch the following byte

```
[deroad@yuuki ~]$ radiff2 cc1.exe.original cc1.exe
0x00567919 74 => eb 0x00567919
```
