# Title
division-by-zero in function opj_pi_next_rpcl of pi.c (line 366)

# Testing Environment
Ubuntu + OpenJPEG (GitHub master, 2016/05/06)

# Exception Information
```
Program received signal SIGFPE, Arithmetic exception.
0xb69892b1 in opj_pi_next_rpcl (pi=0xb3a03ec0) at 
    /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/pi.c:366
366 if (!((pi->x % (OPJ_INT32)(comp->dx << rpx) == 0) || 
        ((pi->x == pi->tx0) && ((trx0 << levelno) % (1 << rpx))))){
```

# PoC
https://raw.githubusercontent.com/trylab/PoCs/master/openjpeg/SIGFPE_opj_pi_next_rpcl@366/poc.j2k

# Credit
Ke Liu of Tencent's Xuanwu LAB


