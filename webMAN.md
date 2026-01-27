# [Fan control](https://github.com/aldostools/webMAN-MOD/wiki/~-Fan-Settings)

> [!info] TL;DR
> Use **AUTO#2** to prevent overheating
> And use **SYSCON** for more quiet fan
> (no guarantee)

Fan Control Modes
webMAN MOD offers 5 different modes to control the temperature of your PS3 system in /setup.ps3:

DYNAMIC (AUTO)
AUTO #2
MANUAL
PS2 Manual
SYSCON
It is recommended that you try different values and stick to the settings that suits better to your environment and condition of your console. If the temperature keep increasing too much, consider to change the thermal paste.

It is generally accepted that the normal temperature for the PS3 is between 65°C and 75°C. Any temperature below that range is desirable. Above 75°C for long periods can damage the internal components in mid or long term.

DYNAMIC (AUTO)
This is the default mode selected when you install the webMAN MOD for the first time. In this mode you set a target (max) temperature, and the plugin will increase/decrease the fan speed dynamically until the target temperature is reached. The default is 68°C. This temperature is optimal if you only play movies or games with low demand of resources. If the temperature varies suddenly, the fan speed will change rapidly to keep the temperature.

On games with high demand of resources (TLoU, GT6, GTAV, etc.) the system temperature may increase up to 78°C (or higher) and the fans could sound like a jet engine. For these games, it is suggested to increase the target temperature to a value that is near to the real maximum temperature (e.g. 75°C).

The minimum and maximum fan speed setting prevents the fan speed go outside the limits defined by the user. The default maximum fan speed is 80%, but it can be changed to any value between 40% and 99%. The minimum can be any value between 20% and 95% (default is 25%).

The target temperature can be configured in-game pressing PS button then using the combos: SELECT+LEFT / SELECT+RIGHT

AUTO #2
This new algorithm is just an alternative method to cool your system in a less aggressive way than the original dynamic fan controller. It does its job but it may not be suitable for all users if the temperature have frequent variations. It's intended to avoid the "jet engine" effect.

In this mode, the fan speed is set proportionally to the current temperature with these 4 simple rules:

If temp < 60°C, the system will use SYSCON mode (ideal for cool environments)
Between 60°C and 69°C, the fan speed will be 31% + 2% per degree
Between 70°C and 78°C, the fan speed will be 50% + 3% per degree (**formerly 5%)
Above 78°C, then fan speed will be set to 80% (**formerly 98%)
**In webMAN MOD 1.47.28 and higher the curve was smoothed to a maximum fan speed of 80%

Auto #2 Fan Temps

It is the same algorithm implemented in the internal fan controller of MAMBA 8.3

For 60°C and above, the fan speed will be ruled by the minimum and maximum fan speed. e.g. If min fan speed = 40%, between 60°C and 64°C the fan speed will be set to 40%.

