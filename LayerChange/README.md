# Scripts based on Layer Change
It is userfull if you need to execute some g-code periodically before or after layer change.

*Insert it to "Before layer change G-code" field at Printer profile -> Custom G-code*

## TemperatureTower

It will change temperature every **stepHeight** millimeters at a given **stepValue** degrees, right after printing Initail level (first **stepHeight** millimeters) at Initial temperature (will be taken from Filament -> Temperature -> Nozzle -> First layer at Filament Settings).
Raft layers does not count for Initial level and its height will be as **stepHeight** + Raft height.

> Please note that this example uses Firmware Retracts feature (G10/G11) and do the following before starting to print next "level" of tower:
>  * Retract
>  * Moves nozzle to bed side (X=10 mm)
>  * Waits unlit next target temperature reached
>  * Deretract and return to printing tower

## FanTower

It will change Model(Part) Cooling Fan speed every **stepHeight** millimeters at a given **stepValuePercents** percents, right after printing Initail level (first **stepHeight** millimeters) at Initial fan speed (will be taken from Cooling -> Fan settings -> Fan speed -> Min at Filament Settings).
Raft layers does not count for Initial level and its height will be as **stepHeight** + Raft height.

## RetractTower

> This script could looks a little bit complicated, but it could be useful in some cases to change something two-dimensionally.
> Since retracts have two dimensions (length and speed), sometimes it is more comfortable to calibrate both for one run. 

At each **stepHeight** mm above raft it calculates and changes:
  * retract length from **lengthInit** mm decrementallly by **lengthStep** mm for maximum **lengthStepsPerPeriod** levels
  * retract speed from **speedInit** mm/s incrementally by **speedStep** mm/s every **lengthStepsPerPeriod** levels of retract length changes.

*Changes it performs for retract could be illustrated this way:
Lets assume we would like to fine-tune retracts from **lengthInit**=0.7 mm to 0.5 mm by **lengthStep**=0.1 mm at each level (so **lengthStepsPerPeriod**=3), and speed from **speedInit**=20 mm/s to 30 mm/s by **speedStep**=5 mm/s increments. If each level will be **stepHeight**=5 mm tall, then we need model height to be 45 mm and retracts will change according to this table:*

| Model level | Retract Length | Retract Speed |
|---|---|---|
| 1 | 0.7 | 20 |
| 2 | 0.6 | 20 |
| 3 | 0.5 | 20 |
| 4 | 0.7 | 25 |
| 5 | 0.6 | 25 |
| 6 | 0.5 | 25 |
| 7 | 0.7 | 30 |
| 8 | 0.6 | 30 |
| 9 | 0.5 | 30 |

> If you need to calibrate just length, you can set **speedInit** to desired value and adjust model height to be not more than (**lengthStepsPerPeriod** x **stepHeight**)
