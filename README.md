# puce65c02
puce65c02, a WDC 65c02 cpu emulator focusing on accuracy and performance
runs at ~1Ghz on a modern computer  
powers reinette IIe : https://github.com/ArthurFerreira2/reinetteIIe

### tests
I left the test and timing routines I used during developpement  
you can use them to verify accuracy :

Theses tests require `6502_functional_test.bin` and `65C02_extended_opcodes_test.bin` which you can get from https://github.com/Klaus2m5/6502_65C02_functional_tests  
and `timingtest-1.bin` I got from BigEd at http://forum.6502.org/viewtopic.php?f=8&t=3340

### compile and run :
```bash
g++ -Wall -O3 -D __TESTS__ puce65c02.cpp -o puce65c02 && ./puce65c02
```
or, much slower but with detailled info :

```bash
g++ -Wall -O3 -D __TESTS__ -D VERBOSE puce65c02.cpp -o puce65c02 && ./puce65c02
```
or, if you just want to check the cycle accuracy :

```bash
g++ -Wall -O3 -D __TESTS__ -D TIMING puce65c02.cpp -o puce65c02 && ./puce65c02
```

### sample run :
```
360F 08        PHP              A=24  X=0E  Y=FF  S=FB  *S=0E  --UB----  Cycles: 3 Total: 3101022
3610 C5 0F     CMP $0F          A=24  X=0E  Y=FF  S=FB  *S=0E  --UB--ZC  Cycles: 3 Total: 3101025
3612 D0 FE     BNE $FE          A=24  X=0E  Y=FF  S=FB  *S=0E  --UB--ZC  Cycles: 2 Total: 3101027
3614 68        PLA              A=30  X=0E  Y=FF  S=FC  *S=30  --UB---C  Cycles: 4 Total: 3101031
3615 29 C3     AND #$C3         A=00  X=0E  Y=FF  S=FC  *S=30  --UB--ZC  Cycles: 2 Total: 3101033
3617 C5 11     CMP $11          A=00  X=0E  Y=FF  S=FC  *S=30  --UB--ZC  Cycles: 3 Total: 3101036
3619 D0 FE     BNE $FE          A=00  X=0E  Y=FF  S=FC  *S=30  --UB--ZC  Cycles: 2 Total: 3101038
361B 28        PLP              A=00  X=0E  Y=FF  S=FD  *S=72  -VUB--Z-  Cycles: 4 Total: 3101042
361C 08        PHP              A=00  X=0E  Y=FF  S=FC  *S=30  -VUB--Z-  Cycles: 3 Total: 3101045
361D A5 12     LDA $12          A=F6  X=0E  Y=FF  S=FC  *S=30  NVUB----  Cycles: 3 Total: 3101048
361F 8D 1502   STA $0215        A=F6  X=0E  Y=FF  S=FC  *S=30  NVUB----  Cycles: 4 Total: 3101052
3622 A5 0D     LDA $0D          A=1B  X=0E  Y=FF  S=FC  *S=30  -VUB----  Cycles: 3 Total: 3101055
3624 20 1402   JSR $0214        A=1B  X=0E  Y=FF  S=FA  *S=00  -VUB----  Cycles: 6 Total: 3101061
0214 E9 F6     SBC #$F6         A=24  X=0E  Y=FF  S=FA  *S=00  --UB----  Cycles: 2 Total: 3101063
0216 60        RTS              A=24  X=0E  Y=FF  S=FC  *S=36  --UB----  Cycles: 6 Total: 3101069
```

enjoy !
