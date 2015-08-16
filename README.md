# cgminer-fan.sh
sh script to control fan PWM based on temperature levels. 
### Requirements
- Hardware: BITMAIN Antminer S5
- Software: Firmware >= SD-S5-20150715-fan_ctrl.tar.gz

(get it at https://bitmaintech.com/support.htm?pid=00720150101032800325X8cMcY2y068F)
### Configs:
set your own desired values for the variables at the very top of the script if the current ones doesn't match your environment.

The idea is to make the miner be restarted as less times as possible (for me it is twiece a day, when the temperature here changes between day and night [happens to be at arround 8am and later again at 9pm]).
### Usage:
The hardware replaces on every boot the filesystem, so you can't store files. But whenever you feel hot, you can ssh into it, copy the file, and execute it:
```
root@antMiner:~# nohub ./cgminer-fan.sh &
```
### View Log:
you can run anytime:
```
root@antMiner:~# tail -f nohup.out
```
#### Very special thanks to:
- https://github.com/kmitz/Regul
- https://github.com/ckolivas/cgminer
