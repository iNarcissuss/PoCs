# Title
division-by-zero in function opj_pi_next_pcrl of pi.c (line 444)

# Testing Environment
Ubuntu + OpenJPEG (GitHub master, 2016/05/06)

# Exception Information
```
Program received signal SIGFPE, Arithmetic exception.
0xb698ae01 in opj_pi_next_pcrl (pi=0xb4603d80) at
    /home/trylab/Desktop/repo/openjpeg/src/lib/openjp2/pi.c:444
444 if (!((pi->y % (OPJ_INT32)(comp->dy << rpy) == 0) || 
        ((pi->y == pi->ty0) && ((try0 << levelno) % (1 << rpy))))){
```

# PoC
https://raw.githubusercontent.com/trylab/PoCs/master/openjpeg/SIGFPE_opj_pi_next_pcrl@444/poc.j2k

# Credit
Ke Liu of Tencent's Xuanwu LAB


