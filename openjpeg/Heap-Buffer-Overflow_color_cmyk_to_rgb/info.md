# Title
OpenJPEG Heap Buffer Overflow in function color_cmyk_to_rgb of color.c

# Testing Environment
Ubuntu + OpenJPEG (GitHub master, 2016/05/06)

# Exception Information
```
==13576== ERROR: AddressSanitizer: heap-buffer-overflow on address 0xb4800a74 at pc 0x8071ec0 bp 0xbfaffb18 sp 0xbfaffb0c
READ of size 4 at 0xb4800a74 thread T0
    #0 0x8071ebf in color_cmyk_to_rgb /home/trylab/Desktop/repo/openjpeg/src/bin/common/color.c:872
    #1 0x805205f in main /home/trylab/Desktop/repo/openjpeg/src/bin/jp2/opj_decompress.c:1378
    #2 0xb5f16a82 (/lib/i386-linux-gnu/libc.so.6+0x19a82)
    #3 0x804a150 in _start (/home/trylab/Desktop/repo/openjpeg/bin/opj_decompress+0x804a150)
0xb4800a74 is located 0 bytes to the right of 4-byte region [0xb4800a70,0xb4800a74)
allocated by thread T0 here:
    #0 0xb61fb905 (/usr/lib/i386-linux-gnu/libasan.so.0+0x16905)
    #1 0xb61bf62d in opj_calloc /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/opj_malloc.c:203
    #2 0xb615cefb in opj_j2k_update_image_data /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/j2k.c:8221
    #3 0xb6169838 in opj_j2k_decode_tiles /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/j2k.c:9764
    #4 0xb6156a44 in opj_j2k_exec /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/j2k.c:7350
    #5 0xb616a83c in opj_j2k_decode /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/j2k.c:9955
    #6 0xb617749c in opj_jp2_decode /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/jp2.c:1492
    #7 0xb6185367 in opj_decode /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/openjpeg.c:412
    #8 0x8051af8 in main /home/trylab/Desktop/repo/openjpeg/src/bin/jp2/opj_decompress.c:1332
    #9 0xb5f16a82 (/lib/i386-linux-gnu/libc.so.6+0x19a82)
SUMMARY: AddressSanitizer: heap-buffer-overflow /home/trylab/Desktop/repo/openjpeg/src/bin/common/color.c:872 color_cmyk_to_rgb
Shadow bytes around the buggy address:
  0x369000f0: fa fa 00 04 fa fa 00 04 fa fa 00 04 fa fa 00 04
  0x36900100: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x36900110: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x36900120: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x36900130: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x36900140: fa fa fa fa fa fa fa fa fa fa fa fa fa fa[04]fa
  0x36900150: fa fa fd fd fa fa fd fd fa fa fd fa fa fa 00 00
  0x36900160: fa fa 00 00 fa fa 00 00 fa fa 00 00 fa fa 00 00
  0x36900170: fa fa 00 00 fa fa 00 00 fa fa 00 00 fa fa 00 00
  0x36900180: fa fa 00 00 fa fa 00 00 fa fa 00 00 fa fa 00 00
  0x36900190: fa fa 00 00 fa fa 00 00 fa fa 00 00 fa fa 00 00
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07 
  Heap left redzone:     fa
  Heap righ redzone:     fb
  Freed Heap region:     fd
  Stack left redzone:    f1
  Stack mid redzone:     f2
  Stack right redzone:   f3
  Stack partial redzone: f4
  Stack after return:    f5
  Stack use after scope: f8
  Global redzone:        f9
  Global init order:     f6
  Poisoned by user:      f7
  ASan internal:         fe
==13576== ABORTING
```

# PoC
https://raw.githubusercontent.com/trylab/PoCs/master/openjpeg/Heap-Buffer-Overflow_color_cmyk_to_rgb/poc.j2k

# Report Timeline
2016-05-06: Ke Liu of Tencent's Xuanwu LAB report issue to OpenJPEG ([#774](https://github.com/uclouvain/openjpeg/issues/774));

2016-05-08: OpenJPEG fixed this issue ([162f619](https://github.com/uclouvain/openjpeg/commit/162f6199c0cd3ec1c6c6dc65e41b2faab92b2d91));

# Credit
Ke Liu of Tencent's Xuanwu LAB


