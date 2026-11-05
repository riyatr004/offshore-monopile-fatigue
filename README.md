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

Why this project
Offshore wind turbines stand on a steel foundation called a monopile. The monopile is often installed months before the turbine arrives. During that time it stands in the sea bare or only partly built, with nobody measuring it. It is lighter, softer and less damped than the finished turbine, and waves and wind keep shaking it. Small vibrations repeated millions of times can slowly damage the steel (fatigue), and nobody would notice.

Research question: how much vibration and fatigue damage can a bare monopile collect while it waits, and what should a small battery-powered logger record to capture it?

The answer in short
Question	Answer from this study
Do waves damage the bare monopile?	Hardly. Over 6 months it uses up about 0.03 % of its fatigue life (damage index 0.0003; 1.0 would mean the life is used up). Even in a pessimistic case (95th percentile) it is only about 0.3 %.
Which sea states cause the damage?	Storms. Waves above 4.5 m are only 4 % of the time but cause almost half (47 %) of the damage.
Which stage is the one to watch?	The tower without the rotor. Wind swirls (vortices) behind the tower can start to shake it when the wind speed is about 11.5 m/s, a very normal wind. This happens for roughly 30 % of the 6 months.
Is that dangerous?	Not shown, not ruled out. It depends on how large the shaking becomes, and a simple model cannot predict that. The study shows that the tower top would need to swing about 0.4 m to use up the allowable fatigue life, and a rough code-style estimate gives about 0.09 m. This amplitude is what should be measured.
What should the logger do?	Resolve very small accelerations and catch storms and "shaking events" instead of recording everything all the time (see Phase D).
Project plan and status
Phase	Content	Main outputs	Status
A	Structure and soil model	Beam model, natural frequencies and mode shapes for 4 installation stages	Complete
B	Loading	Wave spectra, wave forces, wind-vortex (VIV) check	Complete
C	Response and fatigue	Stress at the mudline weld, rainflow counting, Miner damage for a 6-month wait	Complete
D	Logger specification and uncertainty	Sensor range, noise limit, sampling rate, logging strategies, Monte Carlo study	Complete
Phase A: structure and soil model (complete)
Idea in simple words: before asking what pushes the structure, find out how fast it wobbles by itself (its natural frequency), like finding the rhythm of a swing.

A-1: cantilever column (validation). A self-written beam model of an upright tube fixed at the base, checked against the exact textbook solution. With 20 elements, the first three modes match to three decimals. Findings: longer is slower (frequency falls roughly with 1/L^2), wider is faster (rises roughly with D), and wall thickness hardly matters for a bare tube.

A-2: realistic monopile in four installation stages. Pile in the seabed (30 m embedded, 30 m water depth), transition piece, tapered tower, nacelle and rotor. Soil is modelled with springs that get stiffer with depth, and the water around the pile adds mass.

Stage	First natural frequency (medium soil)
Bare monopile	1.22 Hz
+ Transition piece	0.86 Hz
+ Tower	0.51 Hz
+ Nacelle and rotor	0.26 Hz
Every added part lowers the frequency. Soft soil and water also lower it, and they matter most for the bare pile. Waves push at about 0.08 to 0.17 Hz, so the heavier stages sit closer to the wave band.

Phase B: what pushes the structure (complete)
Idea in simple words: a push only builds up a big motion if its rhythm matches the structure's own rhythm, like pushing a swing. Two pushers matter before the turbine is connected: waves and wind swirls.

Six typical North Sea sea states (wave height 1 to 4 m, period 6 to 12 s).
Wave force from the Morison equation. The 8 m pile is so wide that waves mostly accelerate the water around it, so drag is below 0.5 % of the load. A diffraction correction (MacCamy-Fuchs) is applied because short waves are not much longer than the pile is wide.
Wind check: swirls shed at a rhythm f = St x U / D (St about 0.2). Trouble starts when this matches a natural frequency.
Result: the bare pile and the pile with transition piece follow the waves almost statically and are far from any realistic wind speed. The tower stages fall inside the normal wind range.
Phase C: response and fatigue (complete)
Idea in simple words: turn the pushes into stress in the steel, count how many stress cycles of each size occur, and add up the damage. Fatigue is like bending a paperclip: a few big bends or many small ones both wear it out.

Stress at the weld at the seabed level (mudline), from the exact wave moment plus a correction for the structure's own motion.
3-hour stress histories simulated for 40 sea states, rainflow counting, a DNV S-N curve (curve D) and Miner's rule (damage = sum of n / N).
A synthetic 6-month sea-state table (mean wave height about 1.7 m) turns the per-sea-state damage into a waiting-period total.
Cross-check: rainflow counting and two spectral formulas (Dirlik and narrow-band) agree within about 4 %.
Stage	6-month damage from waves	Pessimistic (95th percentile)
Bare monopile	0.0003	0.003
+ Transition piece	0.0004	0.003
+ Tower	0.0005	0.005
+ Nacelle and rotor (parked, qualitative only)	0.02	0.4
The allowable damage is about 0.33 (design fatigue factor 3). The parked-rotor value is a warning, not a result: it has no aerodynamic damping and depends on the tail of the wave spectrum.

Wind swirls (VIV) are treated as a scenario, not a prediction. The study counts how long the tower sits in the risky wind band (about 1330 hours for the tower without rotor) and plots the damage against an assumed shaking amplitude.

Phase D: logger specification and uncertainty (complete)
Idea in simple words: what must a cheap, battery-powered box measure so that nothing important is missed?

Requirement	Value	Why
Measured quantity	2 horizontal accelerations at the highest accessible point, plus inclination and temperature	The top moves most
Range	+/- 1 g	Covers storms and a strong shaking event
Noise floor	at most about 29 ug/sqrt(Hz)	The smallest sea state that still matters gives only about 0.4 mg of motion
Frequency band	0.03 to 7 Hz	Wave band up to the second mode of the bare pile
Sampling	25 Hz for raw bursts, 10 Hz for the always-on channel	At least 2.5 times the highest frequency of interest
Logging strategy (6 months)	Memory	Keeps
Raw continuous	about 2.4 GB	Everything
10-minute statistics + spectrum	about 3 MB	Spectra and exposure, not cycle order
On-board rainflow histogram	about 4 MB	Damage directly
Event-triggered raw bursts + statistics	about 300 to 700 MB	Full waveforms where they matter
Energy hardly differs between strategies (about 18 to 27 Wh), because the always-on sensor dominates. Recommendation: a hybrid of statistics, an hourly rainflow histogram and event-triggered raw bursts.

Monte Carlo (1500 samples) varies soil stiffness, damping, wave severity and VIV inputs. The spread of the damage is mostly driven by how severe the waves are, then by the VIV amplitude and damping. Soil stiffness hardly matters for the bare stages.

Honest limits
Soil is linear (real soil is nonlinear and degrades under cyclic loading); only the first bending mode is used; damping is fixed at 1 % with no aerodynamic damping.
Simplified waves: no breaking waves, slamming, current or marine growth. Sea states and wind statistics are generic, not from a site.
The VIV amplitude is an assumption, and the wind-vortex rule (Strouhal number 0.2, +/- 20 % band) is simplified.
Fatigue uses nominal stress at one weld section, without stress concentration factors.
S-N curve parameters, the thickness correction and the VIV amplitude constants were entered from memory and must be checked against the current standard (DNV-RP-C203 / C205, EN 1991-1-4) before any number is reused.
Logger hardware numbers are assumptions. Monte Carlo input distributions are judgement, not data.
