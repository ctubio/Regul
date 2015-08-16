# cgminer-fan.sh
sh script to control fan PWM based on temperature levels. 
### Requirements
- Hardware: BITMAIN Antminer S5
- Software: Firmware* >= SD-S5-20150715-fan_ctrl.tar.gz

\* download page: https://bitmaintech.com/support.htm?pid=00720150101032800325X8cMcY2y068F)
### Configuration:
set your own desired values for the variables at the very top of the script if the current ones doesn't match your environment.

You may also want to remove the lovely beeper feature (it beeps when getting hot but does nothing while cooling), if so just delete the lines that writes to gpio20.
### Good Configuration:
the idea is to avoid useless fan revolutions/noise/angry_ugly_fat_neighbour, but also make the miner be restarted as less times as possible (for me it is 0 times during winter, but twiece a day in summer, when the temperature here changes between day and night [happens to be at arround 8am were the fan decides to start running at 42% and later again at 9pm when it goes back to 33%]).

I never saw the machine at 75ºC (out of tests in a normal run), but if in case, the script will run the fan at maximum speed. If the temperature even raises to 78ºC, it will stop the miner, and the miner will be started again by your system when the temperature is again below safe ranges.
### Usage:
this hardware restores the original filesystem on every reboot, so you can't store files. But whenever you feel hot, you can ssh into it, copy the file, and execute it:
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
