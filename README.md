# PoCs
### What is PoCs?
This repository is used to store proof-of-concept files collected from fuzzers.

### Details on folders hierarchy
* [**openjpeg**](https://github.com/uclouvain/openjpeg): Official repository of the OpenJPEG project
    * [Issue #774](https://github.com/uclouvain/openjpeg/issues/774) [Heap-Buffer-Overflow_color_cmyk_to_rgb](https://github.com/trylab/PoCs/tree/master/openjpeg/Heap-Buffer-Overflow_color_cmyk_to_rgb) Fixed via [162f619](https://github.com/uclouvain/openjpeg/commit/162f6199c0cd3ec1c6c6dc65e41b2faab92b2d91)
    * [Issue #776](https://github.com/uclouvain/openjpeg/issues/776) [SIGSEGV_Null-Pointer-Access_imagetopnm](https://github.com/trylab/PoCs/tree/master/openjpeg/SIGSEGV_Null-Pointer-Access_imagetopnm) Reported
    * [Issue #784](https://github.com/uclouvain/openjpeg/issues/784) [SIGSEGV_Null-Pointer-Access_sycc444_to_rgb](https://github.com/trylab/PoCs/tree/master/openjpeg/SIGSEGV_Null-Pointer-Access_sycc444_to_rgb) Reported
    * [Issue #785](https://github.com/uclouvain/openjpeg/issues/785) [SIGSEGV_Null-Pointer-Access_color_esycc_to_rgb](https://github.com/trylab/PoCs/tree/master/openjpeg/SIGSEGV_Null-Pointer-Access_color_esycc_to_rgb) Reported
    * [Issue #792](https://github.com/uclouvain/openjpeg/issues/792) [SIGSEGV_Null-Pointer-Access_sycc422_to_rgb](https://github.com/trylab/PoCs/tree/master/openjpeg/SIGSEGV_Null-Pointer-Access_sycc422_to_rgb) Reported
    * [Issue #826](https://github.com/uclouvain/openjpeg/issues/826) [SIGSEGV_Out-of-Bounds-Access_opj_pi_create_decode](https://github.com/trylab/PoCs/tree/master/openjpeg/SIGSEGV_Out-of-Bounds-Access_opj_pi_create_decode) Fixed via [c16bc05](https://github.com/uclouvain/openjpeg/commit/c16bc057ba3f125051c9966cf1f5b68a05681de4) and [ef01f18](https://github.com/uclouvain/openjpeg/commit/ef01f18dfc6780b776d0674ed3e7415c6ef54d24)
    * [Issue #833](https://github.com/uclouvain/openjpeg/issues/833) [bmp24toimage-oob-read](https://github.com/trylab/PoCs/tree/master/openjpeg/bmp24toimage-oob-read) Reported
    * [Issue #833](https://github.com/uclouvain/openjpeg/issues/835) [opj_mqc_byteout-oob-write](https://github.com/trylab/PoCs/tree/master/openjpeg/opj_mqc_byteout-oob-write) Reported
