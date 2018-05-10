Chapter 3 - Analysing Object File
=================================

## simple_section.o


* objdump -h

  -h, --[section-]headers  Display the contents of the section headers

* objdump -s -d

  -s, --full-contents      Display the full contents of all sections requested

  -d, --disassemble        Display assembler contents of executable sections

* objdump -t

  -t, --syms               Display the contents of the symbol table(s)

* size

size - list section sizes and total size.


```
$ make
gcc simple_section.c -c -m32 -o simple_section.o

$ objdump -h simple_section.o

simple_section.o:     file format elf32-i386

Sections:
Idx Name          Size      VMA       LMA       File off  Algn
  0 .group        00000008  00000000  00000000  00000034  2**2
                  CONTENTS, READONLY, GROUP, LINK_ONCE_DISCARD
  1 .text         0000007f  00000000  00000000  0000003c  2**0
                  CONTENTS, ALLOC, LOAD, RELOC, READONLY, CODE
  2 .data         00000008  00000000  00000000  000000bc  2**2
                  CONTENTS, ALLOC, LOAD, DATA
  3 .bss          00000004  00000000  00000000  000000c4  2**2
                  ALLOC
  4 .rodata       00000004  00000000  00000000  000000c4  2**0
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  5 .text.__x86.get_pc_thunk.ax 00000004  00000000  00000000  000000c8  2**0
                  CONTENTS, ALLOC, LOAD, READONLY, CODE
  6 .comment      0000001b  00000000  00000000  000000cc  2**0
                  CONTENTS, READONLY
  7 .note.GNU-stack 00000000  00000000  00000000  000000e7  2**0
                  CONTENTS, READONLY
  8 .eh_frame     0000007c  00000000  00000000  000000e8  2**2
                  CONTENTS, ALLOC, LOAD, RELOC, READONLY, DATA

$ size simple_section.o
   text    data     bss     dec     hex filename
    259       8       4     271     10f simple_section.o

$ objdump -s -d simple_section.o

simple_section.o:     file format elf32-i386

Contents of section .group:
 0000 01000000 07000000                    ........
Contents of section .text:
 0000 5589e553 83ec04e8 fcffffff 05010000  U..S............
 0010 0083ec08 ff75088d 90000000 005289c3  .....u.......R..
 0020 e8fcffff ff83c410 908b5dfc c9c38d4c  ..........]....L
 0030 240483e4 f0ff71fc 5589e551 83ec14e8  $.....q.U..Q....
 0040 fcffffff 05010000 00c745f0 01000000  ..........E.....
 0050 8b900400 00008b80 00000000 01c28b45  ...............E
 0060 f001c28b 45f401d0 83ec0c50 e8fcffff  ....E......P....
 0070 ff83c410 8b45f08b 4dfcc98d 61fcc3    .....E..M...a..
Contents of section .data:
 0000 78563412 12efcdab                    xV4.....
Contents of section .rodata:
 0000 25640a00                             %d..
Contents of section .text.__x86.get_pc_thunk.ax:
 0000 8b0424c3                             ..$.
Contents of section .comment:
 0000 00474343 3a202847 4e552920 372e332e  .GCC: (GNU) 7.3.
 0010 31203230 31383034 303600             1 20180406.
Contents of section .eh_frame:
 0000 14000000 00000000 017a5200 017c0801  .........zR..|..
 0010 1b0c0404 88010000 20000000 1c000000  ........ .......
 0020 00000000 2e000000 00410e08 8502420d  .........A....B.
 0030 05448303 66c5c30c 04040000 28000000  .D..f.......(...
 0040 40000000 2e000000 51000000 00440c01  @.......Q....D..
 0050 00471005 02750043 0f03757c 067e0c01  .G...u.C..u|.~..
 0060 0041c543 0c040400 10000000 6c000000  .A.C........l...
 0070 00000000 04000000 00000000           ............

Disassembly of section .text:

00000000 <func1>:
   0:   55                      push   %ebp
   1:   89 e5                   mov    %esp,%ebp
   3:   53                      push   %ebx
   4:   83 ec 04                sub    $0x4,%esp
   7:   e8 fc ff ff ff          call   8 <func1+0x8>
   c:   05 01 00 00 00          add    $0x1,%eax
  11:   83 ec 08                sub    $0x8,%esp
  14:   ff 75 08                pushl  0x8(%ebp)
  17:   8d 90 00 00 00 00       lea    0x0(%eax),%edx
  1d:   52                      push   %edx
  1e:   89 c3                   mov    %eax,%ebx
  20:   e8 fc ff ff ff          call   21 <func1+0x21>
  25:   83 c4 10                add    $0x10,%esp
  28:   90                      nop
  29:   8b 5d fc                mov    -0x4(%ebp),%ebx
  2c:   c9                      leave
  2d:   c3                      ret

0000002e <main>:
  2e:   8d 4c 24 04             lea    0x4(%esp),%ecx
  32:   83 e4 f0                and    $0xfffffff0,%esp
  35:   ff 71 fc                pushl  -0x4(%ecx)
  38:   55                      push   %ebp
  39:   89 e5                   mov    %esp,%ebp
  3b:   51                      push   %ecx
  3c:   83 ec 14                sub    $0x14,%esp
  3f:   e8 fc ff ff ff          call   40 <main+0x12>
  44:   05 01 00 00 00          add    $0x1,%eax
  49:   c7 45 f0 01 00 00 00    movl   $0x1,-0x10(%ebp)
  50:   8b 90 04 00 00 00       mov    0x4(%eax),%edx
  56:   8b 80 00 00 00 00       mov    0x0(%eax),%eax
  5c:   01 c2                   add    %eax,%edx
  5e:   8b 45 f0                mov    -0x10(%ebp),%eax
  61:   01 c2                   add    %eax,%edx
  63:   8b 45 f4                mov    -0xc(%ebp),%eax
  66:   01 d0                   add    %edx,%eax
  68:   83 ec 0c                sub    $0xc,%esp
  6b:   50                      push   %eax
  6c:   e8 fc ff ff ff          call   6d <main+0x3f>
  71:   83 c4 10                add    $0x10,%esp
  74:   8b 45 f0                mov    -0x10(%ebp),%eax
  77:   8b 4d fc                mov    -0x4(%ebp),%ecx
  7a:   c9                      leave
  7b:   8d 61 fc                lea    -0x4(%ecx),%esp
  7e:   c3                      ret

Disassembly of section .text.__x86.get_pc_thunk.ax:

00000000 <__x86.get_pc_thunk.ax>:
   0:   8b 04 24                mov    (%esp),%eax
   3:   c3                      ret

$ objdump -t simple_section.o

   simple_section.o:     file format elf32-i386

   SYMBOL TABLE:
   00000000 l    df *ABS*   00000000 simple_section.c
   00000000 l    d  .text   00000000 .text
   00000000 l    d  .data   00000000 .data
   00000000 l    d  .bss    00000000 .bss
   00000000 l    d  .rodata 00000000 .rodata
   00000004 l     O .data   00000004 static_var.1740
   00000000 l     O .bss    00000004 static_var2.1741
   00000000 l    d  .text.__x86.get_pc_thunk.ax 00000000 .text.__x86.get_pc_thunk.ax
   00000000 l    d  .note.GNU-stack 00000000 .note.GNU-stack
   00000000 l    d  .eh_frame   00000000 .eh_frame
   00000000 l    d  .comment    00000000 .comment
   00000000 l    d  .group  00000000 .group
   00000000 g     O .data   00000004 global_init_var
   00000004       O *COM*   00000004 global_uninit_var
   00000000 g     F .text   0000002e func1
   00000000 g     F .text.__x86.get_pc_thunk.ax 00000000 .hidden __x86.get_pc_thunk.ax
   00000000         *UND*   00000000 _GLOBAL_OFFSET_TABLE_
   00000000         *UND*   00000000 printf
   0000002e g     F .text   00000051 main
```

## Lena

To use binary file with symbol in code.


* objdump -ht

  -h, --[section-]headers  Display the contents of the section headers

  -t, --syms               Display the contents of the symbol table(s)

```
$ make lena
objcopy -I binary -O elf32-i386 -B i386 l_hires.jpg l_hires.o

$ objdump -ht l_hires.o

l_hires.o:     file format elf32-i386

Sections:
Idx Name          Size      VMA       LMA       File off  Algn
  0 .data         0008b64e  00000000  00000000  00000034  2**0
                  CONTENTS, ALLOC, LOAD, DATA
SYMBOL TABLE:
00000000 l    d  .data  00000000 .data
00000000 g       .data  00000000 _binary_l_hires_jpg_start
0008b64e g       .data  00000000 _binary_l_hires_jpg_end
0008b64e g       *ABS*  00000000 _binary_l_hires_jpg_size
```

## Custom Sections

```c
__attribute__((section("FOO"))) int global = 0x12345678;

__attribute__((section("BAR"))) void foo() { }
```


Real usage

```c
#ifndef __weak
#define __weak __attribute__((weak))
#endif

...

__weak int global = 0x12345789;
```

```
#define HOOK_BUILTIN_CMD(_name, _func)                               \
    static struct shell_cmd shell_##_name                            \
        __attribute__((section(".shell_cmd"), aligned(sizeof(long)), \
```

## ELF File Structure

* readelf

```
$ readelf -h simple_section.o
ELF Header:
  Magic:   7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00 00
  Class:                             ELF32
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              REL (Relocatable file)
  Machine:                           Intel 80386
  Version:                           0x1
  Entry point address:               0x0
  Start of program headers:          0 (bytes into file)
  Start of section headers:          1052 (bytes into file)
  Flags:                             0x0
  Size of this header:               52 (bytes)
  Size of program headers:           0 (bytes)
  Number of program headers:         0
  Size of section headers:           40 (bytes)
  Number of section headers:         15
  Section header string table index: 14
```

