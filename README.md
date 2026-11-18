
RainSaver
A Sensor-Controlled Plant Watering System Powered by Rainwater
Science fair project, 2026

Project website, simulation and log analyzer: https://yourusername.github.io/rain-bucket-waterer/

Abstract
In Metro Vancouver, daily water use rises by about 50% in the hot, dry summer months, mainly because of lawn and garden watering (Metro Vancouver, n.d.). RainSaver is a low-cost irrigation controller that waters a potted plant only when the soil needs it, using rainwater collected in a raised bucket instead of tap water. An Arduino Uno R3 reads a soil moisture sensor every 5 s and opens a 12 V normally closed solenoid valve when moisture falls below 35%. Water flows to the plant by gravity, so no pump is needed. Watering stops at 60%. The controller stores a 15-minute average of soil moisture in its non-volatile EEPROM, which lets it run as a stand-alone data logger for about 10 days.

Research question and hypothesis
Question: Can a sensor-controlled, gravity-fed system keep a potted plant's soil moisture between 35% and 60% using only collected rainwater?

Hypothesis: If the valve opens only when the soil drops below 35% and closes once it reaches 60%, then the soil will stay in that range while using less water than watering on a fixed schedule.

Variable	Description
Independent	Watering method: automatic (sensor-controlled) or fixed schedule
Dependent	Soil moisture (%) over time; total water used (L)
Controlled	Plant species, pot size, soil type, location, bucket height, tube length
Background
Soil moisture sensors can reduce unnecessary irrigation, but field tests of commercial sensor-based controllers found that many were not precise instruments (Cardenas-Lailhacar & Dukes, 2010). Low-cost capacitive sensors give a reliable relationship to soil water content only when they are characterized for a specific soil (Placidi et al., 2020). For this reason, RainSaver's sensor is calibrated in the same soil used in the experiment.

System design
WATER PATH (gravity)
  Rain bucket ──► bulkhead ──► ½" ID tubing ──► solenoid valve ──► tubing ──► plant pot

CONTROL PATH (electrical)
  Moisture sensor (A0) ──► Arduino Uno ──► relay (pin 7) ──► 12 V to valve coil
Control logic
State	Valve	Leaves the state when
IDLE	closed	moisture < 35% → WATERING
WATERING	open	30 s elapsed → SOAKING; moisture ≥ 60% → RESTING
SOAKING	closed	after 60 s: moisture ≥ 60% → RESTING, otherwise → WATERING
RESTING	closed	10 min elapsed → IDLE
LOCKOUT	closed	manual reset only (4 pulses with < 2% rise, or sensor out of range)
Materials
Component	Model / specification	Function
Microcontroller	Arduino Uno R3 (ATmega328P, 16 MHz, 32 KB flash, 2 KB SRAM, 1 KB EEPROM)	Control logic, safety limits, data log
Moisture sensor	Analog soil moisture sensor, output to A0, powered from pin 8	Measures soil water content
Relay module	5 V single-channel relay module, pin 7	Switches the 12 V valve circuit
Solenoid valve	U.S. Solid USS2-00069, ½", 12 V DC, normally closed, 20 W (≈ 1.7 A)	Controls water flow; fails closed
Power supply	12 V DC, 2 A adapter with barrel-jack screw terminal	Powers the valve coil
Flyback diode	1N4007 (1 A, 1000 V)	Suppresses the coil's turn-off voltage spike
Reservoir	Bucket with ½" barbed bulkhead fitting and mesh cover	Collects rainwater
Plumbing	½" NPT brass hose barbs (2), ½" ID vinyl tubing, hose clamps (4), PTFE tape	Leak-free connections
On-board data logger
The sensor is read every 5 s. Every 15 min, the average of those readings (about 180 samples) is saved as one byte in EEPROM.
Byte value 0–100 = moisture %; bit 7 set (+128) = the valve opened during that period; 254 (0xFE) = RESTART marker (power was turned on).
Capacity: 1,024 bytes of EEPROM − 16-byte header = 1,008 records × 15 min ≈ 252 h (about 10.5 days). When full, the oldest records are overwritten.
Endurance: EEPROM is rated for at least 100,000 write/erase cycles (Microchip Technology, 2018). The header is written 96 times a day, giving an estimated life of about 1,040 days. EEPROM.update() skips unchanged bytes (Arduino, n.d.-b).
The Arduino has no real-time clock, so the start time of each power-on is recorded in the logbook. The log analyzer on the website converts records to real dates using these times.
Serial commands (9600 baud)
Command	Action
d	Print the saved log as comma-separated values
i	Records saved, hours covered, total pulses, total valve-open time
e e	Erase the log (typed twice within 15 s)
t	Valve test, 10 s
c / n	Calibration mode / normal mode
w / s / r	Water now / stop / reset after lockout
?	Show settings
Method
Calibrate the sensor in the experimental soil (c): record the raw value in dry soil and in water, and enter them as DRY_VALUE and WET_VALUE.
Run the valve test (t) with the bucket full and raised; measure the supply voltage while the valve is open (target ≥ 11 V).
Measure the valve flow rate (mL/s) with a measuring cup and a timer.
Check all connections for leaks.
Erase the log (e e) and record the start date and time.
Run the automatic pot and a fixed-schedule pot side by side for at least 7 days; record the water given to the fixed-schedule pot.
Retrieve the data (d, i), analyze it in the log analyzer, and compare time in range and water used.
Safety
Risk	Control
Valve coil overheating	30 s maximum per pulse, 60 s cool-down, maximum 6 pulses per session, 10 min rest
Empty bucket	Lockout after 4 pulses with < 2% moisture rise
Loose sensor wire	Raw readings < 50 or > 1000 trigger a lockout
Over-watering	Stops at 60%; valve is normally closed and fails closed
Water near electricity	Low-voltage DC only near water; electronics in a sealed box; adapter kept dry
Data loss	Non-volatile EEPROM; erase requires confirmation
Results
To be completed after testing.

Files
File	Description
index.html	Project website: design, interactive simulation, log analyzer, references
auto_waterer.ino	Arduino code (control logic, safety limits, EEPROM data logger)
References
Arduino. (n.d.-a). UNO R3 [Hardware documentation]. Retrieved November 18, 2026, from https://docs.arduino.cc/hardware/uno-rev3/

Arduino. (n.d.-b). EEPROM library. Retrieved November 18, 2026, from https://docs.arduino.cc/learn/built-in-libraries/eeprom/

Cardenas-Lailhacar, B., & Dukes, M. D. (2010). Precision of soil moisture sensor irrigation controllers under field conditions. Agricultural Water Management, 97(5), 666–672. https://doi.org/10.1016/j.agwat.2009.12.009

Metro Vancouver. (n.d.). Water use changes with the seasons. Retrieved November 18, 2026, from https://www.metrovancouver.org/welovewater/why-conserve-water

Microchip Technology. (2018). ATmega48A/PA/88A/PA/168A/PA/328/P megaAVR data sheet (DS40002061A). https://www.microchip.com/en-us/product/atmega328p

Placidi, P., Gasperini, L., Grassi, A., Cecconi, M., & Scorzoni, A. (2020). Characterization of low-cost capacitive soil moisture sensors for IoT networks. Sensors, 20(12), Article 3585. https://doi.org/10.3390/s20123585

U.S. Solid. (n.d.). 1/2" stainless steel electric solenoid valve, 12V DC, normally closed [Product page]. Retrieved November 18, 2026, from https://ussolid.com/1-2-stainless-steel-electric-solenoid-valve-12v-dc-normally-closed.html

Vishay General Semiconductor. (2020). 1N4001 thru 1N4007 general purpose plastic rectifier (Document No. 88503) [Data sheet]. https://www.vishay.com/en/product/88503/

