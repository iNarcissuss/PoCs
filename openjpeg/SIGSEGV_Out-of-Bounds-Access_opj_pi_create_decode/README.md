DESCRIPTION
==============
An integer overflow issue exists in function opj_pi_create_decode of pi.c. It can lead to Out-Of-Bounds Read and Out-Of-Bounds Write in function opj_pi_next_cprl of pi.c (function opj_pi_next_lrcp, opj_pi_next_rlcp, opj_pi_next_rpcl, opj_pi_next_pcrl may also be vulnerable). This vulnerability allows remote attackers to execute arbitrary code on vulnerable installations of OpenJPEG.


CREDIT
==============
This vulnerability was discovered by Ke Liu of Tencent's Xuanwu LAB.


CVE NUMBER
==============
CVE-2016-7163


TESTED VERSION
==============
Master version of OpenJPEG (2016/08/16)


EXCEPTION LOG
==============
```
==10074==ERROR: AddressSanitizer: heap-buffer-overflow on address 0xad9370a0 at pc 0xb767ba50 bp 0xbff1ad78 sp 0xbff1ad70
READ of size 2 at 0xad9370a0 thread T0
    #0 0xb767ba4f in opj_pi_next_cprl src/lib/openjp2/pi.c:541:12
    #1 0xb76644e7 in opj_pi_next src/lib/openjp2/pi.c:1872:11
    #2 0xb76cd0af in opj_t2_decode_packets src/lib/openjp2/t2.c:412:24
    #3 0xb771ee6e in opj_tcd_t2_decode src/lib/openjp2/tcd.c:1547:15
    #4 0xb771de16 in opj_tcd_decode_tile src/lib/openjp2/tcd.c:1286:15
    #5 0xb74d7a0e in opj_j2k_decode_tile src/lib/openjp2/j2k.c:8134:15
    #6 0xb7563354 in opj_j2k_decode_tiles src/lib/openjp2/j2k.c:9761:23
    #7 0xb74bce4c in opj_j2k_exec src/lib/openjp2/j2k.c:7350:43
    #8 0xb74f378b in opj_j2k_decode src/lib/openjp2/j2k.c:9959:15
    #9 0xb75b80de in opj_jp2_decode src/lib/openjp2/jp2.c:1492:8
    #10 0xb7622eb8 in opj_decode src/lib/openjp2/openjpeg.c:412:10
    #11 0x8140304 in main src/bin/jp2/opj_decompress.c:1332:10
    #12 0xb71b9af2 in __libc_start_main /build/eglibc-X4bnBz/eglibc-2.19/csu/libc-start.c:287
    #13 0x80781eb in _start (bin/opj_decompress+0x80781eb)

AddressSanitizer can not describe address in more detail (wild memory access suspected).
SUMMARY: AddressSanitizer: heap-buffer-overflow src/lib/openjp2/pi.c:541 opj_pi_next_cprl
Shadow bytes around the buggy address:
  0x35b26dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x35b26dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x35b26de0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x35b26df0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x35b26e00: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x35b26e10: fa fa fa fa[fa]fa fa fa fa fa fa fa fa fa fa fa
  0x35b26e20: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x35b26e30: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x35b26e40: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x35b26e50: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x35b26e60: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07 
  Heap left redzone:       fa
  Heap right redzone:      fb
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack partial redzone:   f4
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Container overflow:      fc
  Array cookie:            ac
  Intra object redzone:    bb
  ASan internal:           fe
  Left alloca redzone:     ca
  Right alloca redzone:    cb
==10074==ABORTING
```


SOURCE CODE
==============
1. OOB read and OOB write exist in function opj_pi_next_cprl, function opj_pi_next_lrcp, opj_pi_next_rlcp, opj_pi_next_rpcl, opj_pi_next_pcrl may also be vulnerable.
```
static OPJ_BOOL opj_pi_next_cprl(opj_pi_iterator_t * pi) {
    // ...
    for (pi->layno = pi->poc.layno0; pi->layno < pi->poc.layno1; pi->layno++) {
        index = pi->layno * pi->step_l + pi->resno * pi->step_r + pi->compno * pi->step_c + pi->precno * pi->step_p;
        if (!pi->include[index]) {      // ----> Out-Of-Bounds Read!!!
            pi->include[index] = 1;     // ----> Out-Of-Bounds Write!!!
            return OPJ_TRUE;
        }
    // ...
    return OPJ_FALSE;
}
```

2. Integer overflow exists in function opj_pi_create_decode.
```
opj_pi_iterator_t *opj_pi_create_decode(opj_image_t *p_image,
                                        opj_cp_t *p_cp,
                                        OPJ_UINT32 p_tile_no)
{
    // ...
    l_step_p = 1;
    l_step_c = l_max_prec * l_step_p;
    l_step_r = p_image->numcomps * l_step_c;
    l_step_l = l_max_res * l_step_r;

    /* set values for first packet iterator */
    l_current_pi = l_pi;

    /* memory allocation for include */
    l_current_pi->include = (OPJ_INT16*) opj_calloc(
        (l_tcp->numlayers +1) * l_step_l, sizeof(OPJ_INT16));   // ----> Integer Overflow!!!
    // ...
}
```