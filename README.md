# cgminer-fan.sh
sh script to control fan PWM based on temperature levels. 
### Requirements
- Hardware: BITMAIN Antminer S5
- Software: Firmware >= SD-S5-20150715-fan_ctrl.tar.gz

(get it at https://bitmaintech.com/support.htm?pid=00720150101032800325X8cMcY2y068F)
### Usage:
set your own desired values for the variables at the very top of the script if the current ones doesn't match your environment; the idea is to make the miner be restarted as less times as possible; then:
```
root@antMiner:/etc/init.d# ./cgminer-fan.sh
```
#### Very special thanks to:
- https://github.com/ckolivas/cgminer
- https://github.com/kmitz/Regul
