[README.md](https://github.com/user-attachments/files/35226245/README.md)
# RainSaver: A Sensor-Controlled Plant Watering System Powered by Rainwater

**Adam Hoang, Grade 9, David Thompson Secondary School (November 2026)**

![The finished RainSaver build](images/figure-2j-finished-build.jpg)

## Abstract

RainSaver is a watering system that opens a valve only when the soil is dry. It uses stored rainwater to reduce water waste in the dry months. An Arduino Uno reads a capacitive soil moisture sensor every 5 seconds. When the moisture drops below 35%, the Arduino opens a 12 V solenoid valve for up to 30 seconds and then waits 60 seconds for the water to soak in. The system stops at 60%. Water flows by gravity from a raised rain bucket.

The system was tested on dry, damp and wet soil (three trials of 400 seconds each per condition). The valve opened in all three dry soil trials, and the moisture rose from 21% to 31% to 71% to 78%. In the damp (40% to 48%) and wet (94% to 98%) trials, the valve stayed closed and the moisture changed by 2% or less. The watering stopped at around 60%, but the moisture rose to above 70% as the water settled, so the hypothesis was mostly supported and the stopping point needs further tuning.

**Website:** https://yourusername.github.io/rain-bucket-waterer/

## Question and hypothesis

**Question:** Will a sensor-controlled irrigation system powered by collected rainwater open the valve on dry soil and stay closed on damp and wet soil?

**Hypothesis:** If the soil moisture is below 35%, then the valve will open and close again at 60%. If the soil is damp (35% to 60%) or wet (above 60%), then the valve will stay closed.

## System design

| Part | Description |
|---|---|
| Controller | Arduino Uno R3 |
| Sensor | Capacitive soil moisture sensor V2.0.0 (calibrated: dry 562, wet 245) |
| Switch | 5 V one-channel relay module with optocoupler isolation |
| Valve | 12 V DC normally closed solenoid valve, with a 1N4007 flyback diode across the valve |
| Power | 12 V 2 A adapter (measured 11.7 V with the valve open) |
| Water source | 4-gallon rain bucket raised on a stool, gravity fed to the pot |

**Control rules**

1. Read the sensor every 5 seconds and convert the reading to a percent.
2. If the moisture is below 35%, switch the relay on and open the valve for up to 30 seconds.
3. Wait 60 seconds for the water to soak in before reading again.
4. Stop watering at 60%.
5. If the soil does not become wetter after several attempts, shut the system off (the bucket is probably empty or a tube is blocked).

| Pin | Connection |
|---|---|
| Pin 8 | Sensor power |
| A0 | Sensor signal |
| Pin 7 | Relay IN1 |
| GND | Sensor, relay |

## Photos of the build

| | |
|---|---|
| ![Barbs wrapped in Teflon tape](images/figure-2a-barbs-teflon.jpg) | ![Barb fitted through the bucket wall](images/figure-2b-barb-in-bucket.jpg) |
| *Figure 2. Brass hose barbs wrapped in Teflon tape.* | *Figure 3. Brass hose barb fitted through the bucket wall.* |
| ![Leak test, start](images/figure-2c-leak-test-start.jpg) | ![Leak test after 30 minutes](images/figure-2d-leak-test-30min.jpg) |
| *Figure 4. Leak test, start.* | *Figure 5. Leak test after 30 minutes. No leaks were seen.* |
| ![Tubing](images/figure-2e-tubing.jpg) | ![Breadboard wiring](images/figure-2f-breadboard.jpg) |
| *Figure 6. Tubing from the bucket barb to the valve.* | *Figure 7. Breadboard with the diode, relay and Arduino wiring.* |
| ![Bucket on stool](images/figure-2h-bucket-on-stool.jpg) | ![Pot](images/figure-2i-pot.jpg) |
| *Figure 8. Rain bucket raised on a stool.* | *Figure 9. Porcelain pot with soil, in the green basket.* |

## Results

| Trial | Soil condition | Starting moisture (%) | Valve opened? | Ending moisture (%) | Time (s) |
|---|---|---|---|---|---|
| 1 | Dry (below 35%) | 24 | Yes | 78 | 400 |
| 2 | Dry (below 35%) | 31 | Yes | 76 | 400 |
| 3 | Dry (below 35%) | 21 | Yes | 71 | 400 |
| 4 | Damp (35% to 60%) | 40 | No | 41 | 400 |
| 5 | Damp (35% to 60%) | 42 | No | 43 | 400 |
| 6 | Damp (35% to 60%) | 48 | No | 46 | 400 |
| 7 | Wet (above 60%) | 98 | No | 100 | 400 |
| 8 | Wet (above 60%) | 96 | No | 96 | 400 |
| 9 | Wet (above 60%) | 94 | No | 93 | 400 |

![Dry soil trials](images/figure-3a-dry-trials.png)

*Figure 10. Soil moisture (%) over time for the three dry soil trials.*

![Damp soil trials](images/figure-3b-damp-trials.png)

*Figure 11. Soil moisture (%) over time for the three damp soil trials.*

![Wet soil trials](images/figure-3c-wet-trials.png)

*Figure 12. Soil moisture (%) over time for the three wet soil trials.*

**Observations:** the solenoid valve clicked as it opened, the relay clicked at the same moment, and its lime green light turned on whenever the relay switched on the valve. The sensor readings were a little inconsistent unless the sensor was pushed fully down into the soil.

## Discussion

The data support the hypothesis. The valve opened in all three dry soil trials and stayed closed in all six damp and wet soil trials. In the dry soil trials, the watering stopped at around 60% moisture, as designed. However, as the water settled through the soil, the moisture reading kept rising and ended well above 70% (71% to 78%), because the water continued to spread to the sensor after the valve had closed.

**Sources of error:** sensor accuracy and soil packing, calibration, sensor position, hand-prepared soil conditions, short 400 second trials, power supply margin (about 1.7 A needed), and only three trials per condition.

**Next steps:** tune the stop point, add a water level sensor to the bucket, test more than one plant and soil type, use a data logger, and run the system outdoors for longer.

## References

- Cardenas-Lailhacar, B., & Dukes, M. D. (2010). Precision of soil moisture sensor irrigation controllers under field conditions. *Agricultural Water Management, 97*(5), 666-672. https://doi.org/10.1016/j.agwat.2009.12.009
- City of Vancouver. (n.d.). Conserve water: Use a rain barrel. https://vancouver.ca/home-property-development/rain-barrels.aspx
- City of Vancouver. (2023). Vancouver watering restrictions escalate to Stage 2 on August 4. https://vancouver.ca/news-calendar/vancouver-watering-restrictions-escalate-to-stage-2-on-august-4.aspx
- Dukes, M. D. (2012). Water conservation potential of landscape irrigation smart controllers. *Transactions of the ASABE, 55*(2), 563-569.
- Metro Vancouver. (n.d.). Water use changes with the seasons. https://metrovancouver.org/welovewater/why-conserve-water
- Placidi, P., Gasperini, L., Grassi, A., Cecconi, M., & Scorzoni, A. (2020). Characterization of low-cost capacitive soil moisture sensors for IoT networks. *Sensors, 20*(12), 3585. https://doi.org/10.3390/s20123585
- Statistics Canada. (2023). Table 38-10-0271-01: Potable water use by sector and average daily use [Data table]. https://doi.org/10.25318/3810027101-eng

## Files

- `index.html`: project website with the results, an interactive simulation of the control rules, and a log analyzer for the Arduino data log
- `auto_waterer.ino`: Arduino code
- `images/`: photos of the build and graphs of the results

## Data logging

Every 15 minutes, the Arduino saves the average soil moisture in its own memory (about 10 days of data, kept when unplugged). The log is printed with the `d` command in the Serial Monitor and can be analyzed with the log analyzer on the website. The 400 second trials reported above were recorded from the Serial Monitor every 50 seconds.
