Fatigue Risk of Bare Offshore Monopiles During Installation: A Python-Based Study
Self-study portfolio project | Riya Thripakkal Rajesh, M.Sc. ACCESS, TU Dresden

All geometry, mass, soil, sea-state and logger values are illustrative, not site data. Results are for learning and demonstration, not for design use.

Summary
Before a wind turbine is connected, its steel foundation can stand bare in the sea for months with nobody measuring it. In this project, a computer model was built with AI assistance (Claude) to estimate how much wear (fatigue) the foundation picks up during that time, and what a monitoring box should record. Waves barely wear it out. Over 6 months (4380 hours) it uses up less than 1 % of its life, and almost half of that comes from a few big storms with wave heights above 4.5 m. The stage to watch is the tower before the rotor is added. A wind speed of about 11.5 m/s, which is normal, can make it shake. This could happen for roughly 30 % of the period. The study cannot say how much, because that is hard to predict without real measurements. The tower top would need to swing by about 0.4 m to use up the safe fatigue limit, while a rough estimate gives about 0.09 m.

The logger. A logger is a small battery-powered box with sensors that records measurements on its own. Based on the study, it should have these features:

What it measures: acceleration in two horizontal directions at the highest reachable point of the structure, plus tilt and temperature.
Measuring range: ±10 m/s² (this is ±1 g, where 1 g = 9.81 m/s²). The strongest shaking expected is about 4.3 m/s², so this range covers it without cutting off the peaks.
Sensitivity: quiet seas move the structure by only about 0.004 m/s² (RMS). The sensor noise must therefore stay below about 2.8 × 10⁻⁴ (m/s²)/√Hz, in the band from 0.03 to 2 Hz.
Frequency band: 0.03 to 7 Hz, which covers waves (0.08 to 0.17 Hz) and the structure's own vibration.
Sampling rate: 25 Hz for detailed recordings and 10 Hz for the always-on channel.
What it stores: summary values every 10 minutes (mean, maximum, main frequency and a 32-band spectrum), an hourly count of stress cycles, and detailed recordings only when a storm or strong shaking starts.
Why this mix: recording everything would need about 2.4 GB for 6 months. The smart mix needs about 3 MB to 700 MB, depending on how often events are triggered. Energy use is about the same either way, roughly 67 to 97 kJ for 6 months at an average power of 4 to 6 mW, because the sensor itself uses most of the power. One battery cell is enough in this model.
Limits. All numbers are examples, not real site data, and the fatigue constants must be checked against the official standards before anyone reuses them. The logger values also rest on assumed hardware data, so they should be checked against real sensor data sheets.

