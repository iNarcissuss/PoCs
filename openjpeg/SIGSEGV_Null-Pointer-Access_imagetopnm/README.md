# Title
OpenJPEG Null Pointer Access in function imagetopnm of convert.c

# Testing Environment
Ubuntu + OpenJPEG (GitHub master, 2016/05/06)

# Exception Information
```
==22059== ERROR: AddressSanitizer: SEGV on unknown address 0x00000000 
    (pc 0x0805f813 sp 0xbfd3b8a0 bp 0xbfd3b958 T0)
AddressSanitizer can not provide additional info.
    #0 0x805f812 in imagetopnm /home/trylab/Desktop/repo/openjpeg/src/bin/jp2/convert.c:1974
    #1 0x805279a in main /home/trylab/Desktop/repo/openjpeg/src/bin/jp2/opj_decompress.c:1467
    #2 0xb5e96a82 (/lib/i386-linux-gnu/libc.so.6+0x19a82)
    #3 0x804a150 in _start (/home/trylab/Desktop/repo/openjpeg/bin/opj_decompress+0x804a150)
SUMMARY: AddressSanitizer: SEGV /home/trylab/Desktop/repo/openjpeg/src/bin/jp2/convert.c:1974 imagetopnm
==22059== ABORTING
```

# PoC
https://raw.githubusercontent.com/trylab/PoCs/master/openjpeg/SIGSEGV_Null-Pointer-Access_imagetopnm/poc.j2k

# Report Timeline
+ 2016-05-06: Ke Liu of Tencent's Xuanwu LAB report issue to OpenJPEG ([#776](https://github.com/uclouvain/openjpeg/issues/776));

# Credit
Ke Liu of Tencent's Xuanwu LAB

