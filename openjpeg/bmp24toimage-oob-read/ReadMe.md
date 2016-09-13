DESCRIPTION
==============
An Out-of-Bounds Read issue was found in function bmp24toimage of convertbmp.c. The root cause of this issue was an Integer Overflow issue. The opj_compress process may crash in other functions.


CREDIT
==============
This vulnerability was discovered by **Ke Liu of Tencent's Xuanwu LAB**.


TESTED VERSION
==============
Master version of OpenJPEG (805972f, 2016/09/12)


EXCEPTION LOG
==============
```
==3498==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000eff5 
at pc 0x00000041ced5 bp 0x7ffddcd299b0 sp 0x7ffddcd299a0
READ of size 1 at 0x60200000eff5 thread T0
    #0 0x41ced4 in bmp24toimage openjpeg/src/bin/jp2/convertbmp.c:150
    #1 0x42273c in bmptoimage openjpeg/src/bin/jp2/convertbmp.c:747
    #2 0x40b8b2 in main openjpeg/src/bin/jp2/opj_compress.c:1730
    #3 0x7fdcbaa4782f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #4 0x4037e8 in _start (openjpeg/bin/opj_compress+0x4037e8)

0x60200000eff5 is located 1 bytes to the right of 4-byte region [0x60200000eff0,0x60200000eff4)
allocated by thread T0 here:
    #0 0x7fdcbbb5079a in __interceptor_calloc (/usr/lib/x86_64-linux-gnu/libasan.so.2+0x9879a)
    #1 0x421e06 in bmptoimage openjpeg/src/bin/jp2/convertbmp.c:682
    #2 0x40b8b2 in main openjpeg/src/bin/jp2/opj_compress.c:1730
    #3 0x7fdcbaa4782f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)

SUMMARY: AddressSanitizer: heap-buffer-overflow openjpeg/src/bin/jp2/convertbmp.c:150 bmp24toimage
Shadow bytes around the buggy address:
  0x0c047fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9de0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x0c047fff9df0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa[04]fa
  0x0c047fff9e00: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e10: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e20: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e30: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e40: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
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
==3498==ABORTING
```

ANALYSIS
==============
The integer overflow issue exists in function bmptoimage. Here Info_h.biWidth == 0x40000001 and Info_h.biBitCount == 0x18 and stride should equals (0x40000001 * 0x18 + 31) / 32 * 4 == 0xC0000004. But actually stride equals 0x04 when overflow happened.
```
opj_image_t* bmptoimage(const char *filename, opj_cparameters_t *parameters)
{
    // ......
	stride = ((Info_h.biWidth * Info_h.biBitCount + 31U) / 32U) * 4U;
	if (Info_h.biBitCount == 4 && Info_h.biCompression == 2) { 
		stride = ((Info_h.biWidth * 8U + 31U) / 32U) * 4U;
	}
	pData = (OPJ_UINT8 *) calloc(1, stride * Info_h.biHeight * sizeof(OPJ_UINT8));
	if (pData == NULL) {
		fclose(IN);
		return NULL;
	}
    // ......
}
```