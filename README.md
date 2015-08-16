# cgminer-fan.sh
sh script to control fan PWM based on temperature levels. 
### Requirements
- Hardware: BITMAIN Antminer S5
- Software: Firmware* >= SD-S5-20150715-fan_ctrl.tar.gz
- Config: must have defined somewhere in /config/cgminer.conf but not at the end of the file (because of the last comma):
```
{
...
"bitmain-fan-ctrl" : true,
"bitmain-fan-pwm" : "100",
...
}
```

\* download page: https://bitmaintech.com/support.htm?pid=00720150101032800325X8cMcY2y068F)
### Customization:
set your own desired values for the variables at the very top of the script if the current ones doesn't match your environment.

You may also want to remove the lovely beeper feature (it beeps when getting hot but does nothing while cooling), if so just delete the lines that writes to gpio20.
### Optimization:
the idea is to avoid useless fan revolutions/noise/angry_ugly_fat_neighbour, but also make the miner be restarted as less times as possible (for me it is 0 times during winter, but twiece a day in summer, when the temperature here changes between day and night [happens to be at arround 8am were the fan decides to start running at `$FAN_LOW` and later again at 9pm when it goes back to `$FAN_MIN`]).

You must never put the machine at `$CELSIUS_MAX` (out of tests in a normal run), but if in case, the script will run the fan at `$FAN_MAX` speed. If the temperature even raises to `$CELSIUS_DIE`, it will stop the miner, and the miner will be started again by your system when the temperature is again below safe ranges.

You may want to start with somewhat similar to:
```bash
FAN_MIN=50;
FAN_LOW=75;
FAN_MAX=100;
CELSIUS_LOW=60;
CELSIUS_MAX=70;
CELSIUS_DIE=78;
```
### Usage:
the machine restores the original filesystem on every reboot, so you can't store files. But whenever you feel hot, you can ssh into it, copy the file, and execute it:
```
root@antMiner:~# nohub ./cgminer-fan.sh &
```
this will start controlling the temperature and the fan speed every `$DELAY` seconds. It will edit the configuration file and restart your cgminer to apply the new fan speed every time that the temperature goes over or below a threshold.
### View Log:
you can run anytime:
```
root@antMiner:~# tail -f nohup.out
```
### Kill it:
when neighbour is out of home:
```
root@antMiner:~# killall cgminer-fan.sh
```
### Forced fan speed:
when neighbour is still out of home:
```
root@antMiner:~# ./cgminer-fan.sh 100
```
this will change the fan speed to the value of the first argument and exit (will not keep controling nothing, well only that the value passed is greater than `$FAN_MIN`, because we don't want to see fire today [to really avoid fire keep `$FAN_MIN` over a minimum of 30, always]).
#### Alternative controller:
see [this post](https://jomcflyatwork.wordpress.com/2015/07/13/shell-script-for-antminer-s5-temperature-regulation/) from  [kmitz/Regul](https://github.com/kmitz/Regul) if you preffer to control the temperature tweaking the Frequency rather than the Fan Speed.
#### Very special thanks to:
- https://github.com/kmitz/Regul
- https://github.com/ckolivas/cgminer


###### Donations
nope. but you can donate to your favorite developer today! (or tomorrow!)
