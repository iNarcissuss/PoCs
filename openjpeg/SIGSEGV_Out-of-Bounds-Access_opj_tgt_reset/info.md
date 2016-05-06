# Title
OpenJPEG Out-of-Bounds Access in function opj_tgt_reset of tgt.c

# Testing Environment
Ubuntu + OpenJPEG (GitHub master, 2016/05/06)

# Exception Information
```
==1889== ERROR: AddressSanitizer: SEGV on unknown address 0x0000c03a (pc 0xb61731c3 sp 0xbf95c1c0 bp 0xbf95c1e8 T0)
AddressSanitizer can not provide additional info.
    #0 0xb61731c2 in opj_tgt_reset /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/tgt.c:241
    #1 0xb615db0a in opj_t2_read_packet_header /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/t2.c:874
    #2 0xb615b7e8 in opj_t2_decode_packet /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/t2.c:536
    #3 0xb615b128 in opj_t2_decode_packets /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/t2.c:422
    #4 0xb616d7ad in opj_tcd_t2_decode /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/tcd.c:1546
    #5 0xb616c2c5 in opj_tcd_decode_tile /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/tcd.c:1285
    #6 0xb6111853 in opj_j2k_decode_tile /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/j2k.c:8134
    #7 0xb611e61e in opj_j2k_decode_tiles /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/j2k.c:9757
    #8 0xb610ba44 in opj_j2k_exec /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/j2k.c:7350
    #9 0xb611f83c in opj_j2k_decode /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/j2k.c:9955
    #10 0xb613a367 in opj_decode /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/openjpeg.c:412
    #11 0x8051af8 in main /home/trylab/Desktop/repo/openjpeg/src/bin/jp2/opj_decompress.c:1332
    #12 0xb5ecba82 (/lib/i386-linux-gnu/libc.so.6+0x19a82)
    #13 0x804a150 in _start (/home/trylab/Desktop/repo/openjpeg/bin/opj_decompress+0x804a150)
SUMMARY: AddressSanitizer: SEGV /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/tgt.c:241 opj_tgt_reset
==1889== ABORTING
```

# PoC
https://raw.githubusercontent.com/trylab/PoCs/master/openjpeg/SIGSEGV_Out-of-Bounds-Access_opj_tgt_reset/poc.j2k

# Credit
Ke Liu of Tencent's Xuanwu LAB

