# Scripts based on Layer Change
It is userfull if you need to execute some g-code periodically before or after layer change.

## TemperatureTower

*Insert it to "Before layer change G-code" field at Printer profile -> Custom G-code*

It will change temperature every **stepHeight** millimeters at a given **stepValue** degrees, right after printing Initail level (first **stepHeight** millimeters) at Initial temperature (will be taken from Filament -> Temperature -> Nozzle -> First layer at Filament Settings).
Raft layers does not count for Initial level and its height will be as **stepHeight** + Raft height.

> Please note that this example uses Firmware Retracts feature (G10/G11) and do the following before starting to print next "level" of tower:
>  * Retract
>  * Moves nozzle to bed side (X=10 mm)
>  * Waits unlit next target temperature reached
>  * Deretract and return to printing tower

## FanTower

*Insert it to "Before layer change G-code" field at Printer profile -> Custom G-code*

It will change Model(Part) Cooling Fan speed every **stepHeight** millimeters at a given **stepValuePercents** percents, right after printing Initail level (first **stepHeight** millimeters) at Initial fan speed (will be taken from Cooling -> Fan settings -> Fan speed -> Min at Filament Settings).
Raft layers does not count for Initial level and its height will be as **stepHeight** + Raft height.
