
RainSaver
A Sensor-Controlled Plant Watering System Powered by Rainwater
Science fair project, 2026 · Website: https://yourusername.github.io/rain-bucket-waterer/

Why it matters
In Metro Vancouver, daily water use rises by about 50% in the hot, dry summer months, from about 1 billion to more than 1.5 billion litres a day, mostly because of lawn and garden watering (Metro Vancouver, n.d.). British Columbians also use more water at home than the Canadian average of 223 litres per person per day (Statistics Canada, 2023), and during the 2023 drought all lawn watering was banned (City of Vancouver, 2023).

Collected rainwater reduces demand on treated drinking water (City of Vancouver, n.d.), and soil moisture sensors can prevent watering when the soil is already wet, although their accuracy varies (Cardenas-Lailhacar & Dukes, 2010; Dukes, 2012). Low-cost sensors need to be calibrated for the soil they are used in (Placidi et al., 2020). RainSaver combines both ideas.

Question and hypothesis
Question: Can a sensor-controlled system keep a plant's soil moisture between 35% and 60% using only collected rainwater?

Hypothesis: If the plant is watered only when the soil drops below 35%, then the soil will stay in the target range while using less water than watering on a fixed schedule.

How it works
Water flows from a raised rain bucket to the plant by gravity, so no pump is needed.
An Arduino reads the soil moisture every 5 seconds. Below 35%, it opens a 12 V valve for up to 30 seconds, then waits 60 seconds for the water to soak in. It stops at 60%.
Every 15 minutes, the Arduino saves the average soil moisture in its own memory (about 10 days of data, kept when unplugged).
If watering doesn't raise the moisture, the bucket is probably empty, so the system stops.
Materials: Arduino Uno, soil moisture sensor, 5 V relay, 12 V solenoid valve, 12 V power supply, rain bucket, tubing.

Method
Calibrate the sensor in dry soil and in water, using the same soil as the experiment.
Test the valve with the bucket full, and measure its flow rate (mL per second).
Start the log and write the date and time in the logbook.
Run one automatic pot and one pot watered on a fixed schedule for at least 7 days.
Analyze the saved data with the log analyzer on the website and compare the water used.
Results
To be completed after testing.

Files
index.html: project website with an interactive simulation and a log analyzer
auto_waterer.ino: Arduino code
References
Cardenas-Lailhacar, B., & Dukes, M. D. (2010). Precision of soil moisture sensor irrigation controllers under field conditions. Agricultural Water Management, 97(5), 666–672. https://doi.org/10.1016/j.agwat.2009.12.009

City of Vancouver. (n.d.). Conserve water: Use a rain barrel. Retrieved November 18, 2026, from https://vancouver.ca/home-property-development/rain-barrels.aspx

City of Vancouver. (2023). Vancouver watering restrictions escalate to Stage 2 on August 4. https://vancouver.ca/news-calendar/vancouver-watering-restrictions-escalate-to-stage-2-on-august-4.aspx

Dukes, M. D. (2012). Water conservation potential of landscape irrigation smart controllers. Transactions of the ASABE, 55(2), 563–569.

Metro Vancouver. (n.d.). Water use changes with the seasons. Retrieved November 18, 2026, from https://www.metrovancouver.org/welovewater/why-conserve-water

Placidi, P., Gasperini, L., Grassi, A., Cecconi, M., & Scorzoni, A. (2020). Characterization of low-cost capacitive soil moisture sensors for IoT networks. Sensors, 20(12), Article 3585. https://doi.org/10.3390/s20123585

Statistics Canada. (2023). Potable water use by sector and average daily use (Table 38-10-0271-01) [Data table]. https://doi.org/10.25318/3810027101-eng

