# Title
Null Pointer Access in function color_esycc_to_rgb of color.c

# Testing Environment
Ubuntu + OpenJPEG (GitHub master, 2016/05/25)

# Exception Information
```
==31274== ERROR: AddressSanitizer: SEGV on unknown address 0x00000000 
    (pc 0x08072dd4 sp 0xbfca8780 bp 0xbfca87e8 T0)
AddressSanitizer can not provide additional info.
    #0 0x8072dd3 in color_esycc_to_rgb openjpeg/src/bin/common/color.c:937
    #1 0x80520b2 in main openjpeg/src/bin/jp2/opj_decompress.c:1381
    #2 0xb5e81a82 (/lib/i386-linux-gnu/libc.so.6+0x19a82)
    #3 0x804a150 in _start (openjpeg/bin/opj_decompress+0x804a150)
SUMMARY: AddressSanitizer: SEGV openjpeg/src/bin/common/color.c:937 color_esycc_to_rgb
==31274== ABORTING
```

# PoC
https://raw.githubusercontent.com/trylab/PoCs/master/openjpeg/SIGSEGV_Null-Pointer-Access_color_esycc_to_rgb/color_esycc_to_rgb.j2k

# Credit
Ke Liu of Tencent's Xuanwu LAB
