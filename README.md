# Rain Bucket Waterer

An Arduino system that waters a plant automatically using rainwater collected in a bucket. Science fair project.

🌐 **Website + simulator:** https://yourusername.github.io/rain-bucket-waterer/

## What it does
A soil moisture sensor checks the soil every 5 seconds. When moisture drops below 35%, the Arduino opens a 12V valve and rainwater flows from a raised bucket to the plant by gravity. It stops when the soil reaches 60%.

## Why
It saves treated tap water by using rain, and the plant only gets water when it actually needs it.

## Parts
- Arduino Uno
- Soil moisture sensor
- 5V relay module
- 12V solenoid valve (U.S. Solid USS2-00069, normally closed)
- 12V 2A power adapter
- 1N4007 diode
- Bucket, bulkhead fitting, brass hose barbs, vinyl tubing, hose clamps

## Safety features
- Valve open 30 seconds max, then a 60-second soak
- Max 6 pulses per session, then a 10-minute rest
- Lockout if the bucket is empty
- Lockout if a sensor wire comes loose

## Files
- `index.html`: project website with an interactive simulator
- `auto_waterer.ino`: Arduino code
