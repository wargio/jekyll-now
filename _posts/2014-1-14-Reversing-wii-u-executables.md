---
layout: post
title: Reversing Wii U Executables
---

First thing to say, Wii U uses Executable and Linkable Format (ELF) with dynamic linking (since Wii U has a real OS), but they are different from the normal ones:

* Wii U libraries are called RPL
* Wii U executables are called RPX, but these are actually RPL.

The only difference between RPX and RPL is that the first one has the main entry point, but both are ELFs.

Ok, so this is what i understood about the header:

```c
/* Total size 0x500 -> elf + section table */
typedef struct __cafe_elf {
    uint8_t  e_ident[0x10]; // {0x7f,0x45,0x4c,0x46, <-- 'elf'
                            // 0x01,     <-- one
                            // 0x01,0x05,    <-- sdk version ?
                            // 0xca,0xfe,    <-- 0xcafe
                            // 0x00,0x00, ... ,0x00} 
    uint16_t e_type;        // 0xfe01 = rpl
    uint16_t e_machine;     // 0x0014 PPC
    uint32_t e_version;     // 0x00000001
    uint32_t e_entry;       // 0x02000000
    uint32_t e_phoff;       // 0x00000000
    uint32_t e_shoff;       // 0x00000040
    uint32_t e_flags;       // 0x00000000
    uint16_t e_ehsize;      // 0x0032 (54)
    uint16_t e_phentsize;   // 0x0000
    uint16_t e_phnum;       // 0x0000
    uint16_t e_shentsize;   // 0x0028 (40)
    uint16_t e_shnum;       // 0x0015 (19)
    uint16_t e_shstrndx;    // 0x0012 (16)
    uint8_t  _pad[0xC];     // zero filled
    uint8_t  zero[0x28];    // zero filled
    uint32_t one_0;         // 0x00000001
    uint32_t one_1;         // 0x00000001
} cafe_elf;
```

```c
typedef struct __cafe_elf_section_tbl {
    uint32_t flags;   // 0x08000006 <-- example
                      // 0x08000000 <-- z
                      // 0x00000001 <-- w
                      // 0x00000002 <-- a
                      // 0x00000004 <-- x
    uint32_t address; // 0x02000000 <-- memory addr (.text)
    uint32_t offset;  // 0x0019D740 <-- file offset
    uint32_t size;    // 0x00003EC8 <-- compressed size
    uint32_t data0;   // 0x00000000 <-- unknown
    uint32_t data1;   // 0x00000000 <-- unknown
    uint32_t align;   // 0x00000020 (32) <-- data align
    uint32_t data3;   // 0x00000000 <-- unknown
    uint32_t data4;   // 0x00000007 <-- unknown
    uint32_t data5;   // 0x80000001 <-- unknown
} cafe_elf_section_tbl;
```

Each section is compressed through ZLIB and has this structure:

```c
typedef struct __cafe_elf_section_data {
    uint32_t decompressed_size;
    uint16_t zlib_compression_hdr;
    uint8_t  data[];
} cafe_elf_section_tbl;
```
