# Title
division-by-zero in function opj_pi_next_pcrl of pi.c (line 447)

# Testing Environment
Ubuntu + OpenJPEG (GitHub master, 2016/05/06)

# Exception Information
```
Program received signal SIGFPE, Arithmetic exception.
0xb698af0c in opj_pi_next_pcrl (pi=0xb4603d80) at 
    /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/pi.c:447
447 if (!((pi->x % (OPJ_INT32)(comp->dx << rpx) == 0) || 
        ((pi->x == pi->tx0) && ((trx0 << levelno) % (1 << rpx))))){
```

# PoC
https://raw.githubusercontent.com/trylab/PoCs/master/openjpeg/SIGFPE_opj_pi_next_pcrl@447/poc.j2k

# Credit
Ke Liu of Tencent's Xuanwu LAB


