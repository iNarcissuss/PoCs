# Title
Null Pointer Access in function sycc444_to_rgb of color.c

# Testing Environment
Ubuntu + OpenJPEG (GitHub master, 2016/05/25)

# Exception Information
```
==19455== ERROR: AddressSanitizer: SEGV on unknown address 0x00000000 
    (pc 0x0806ef10 sp 0xbff51d80 bp 0xbff51e08 T0)
AddressSanitizer can not provide additional info.
    #0 0x806ef0f in sycc444_to_rgb openjpeg/src/bin/common/color.c:115
    #1 0x8071a24 in color_sycc_to_rgb openjpeg/src/bin/common/color.c:346
    #2 0x8051fc3 in main openjpeg/src/bin/jp2/opj_decompress.c:1375
    #3 0xb5e7ea82 (/lib/i386-linux-gnu/libc.so.6+0x19a82)
    #4 0x804a150 in _start (openjpeg/bin/opj_decompress+0x804a150)
SUMMARY: AddressSanitizer: SEGV openjpeg/src/bin/common/color.c:115 sycc444_to_rgb
==19455== ABORTING
```

# PoC
https://raw.githubusercontent.com/trylab/PoCs/master/openjpeg/SIGSEGV_Null-Pointer-Access_sycc444_to_rgb/sycc444_to_rgb.j2k

# Credit
Ke Liu of Tencent's Xuanwu LAB
