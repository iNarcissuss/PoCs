# Title
Null Pointer Access in function sycc422_to_rgb of color.c

# Testing Environment
Ubuntu + OpenJPEG (GitHub master, 2016/06/28)

# Exception Information
```
==3793==ERROR: AddressSanitizer: SEGV on unknown address 0x00000000 (pc 0x08164302 bp 0xb4e00770 sp 0xbffd6da0 T0)
    #0 0x8164301 in sycc422_to_rgb ~/Desktop/repo/openjpeg-master/src/bin/common/color.c:169:29
    #1 0x8164301 in color_sycc_to_rgb ~/Desktop/repo/openjpeg-master/src/bin/common/color.c:336
    #2 0x8137a25 in main ~/Desktop/repo/openjpeg-master/src/bin/jp2/opj_decompress.c:1375:4
    #3 0xb7402a82 in __libc_start_main /build/eglibc-617sU_/eglibc-2.19/csu/libc-start.c:287
    #4 0x8077e6b in _start (~/Desktop/repo/openjpeg-master/bin/opj_decompress+0x8077e6b)

AddressSanitizer can not provide additional info.
SUMMARY: AddressSanitizer: SEGV ~/Desktop/repo/openjpeg-master/src/bin/common/color.c:169 sycc422_to_rgb
==3793==ABORTING
```

# PoC
https://raw.githubusercontent.com/trylab/PoCs/master/openjpeg/SIGSEGV_Null-Pointer-Access_sycc422_to_rgb/sycc422_to_rgb.j2k

# Credit
Ke Liu of Tencent's Xuanwu LAB
