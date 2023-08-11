# Electrical Power Factor Correction Algorithm
Ideally, a purely resistive load produces the least amount of energy losses in a power network. Capacitors have negative reactances whereas inductors have positive reactances. An algebraic sum of the two would lead to all network reactances cancelling out leaving only the resistances.

This means that if an inductive load is detected, the capacitor banks are engaged. Also if a capactivie load is present, the reactor transformers (inductors) are called into action.

## Algorithm steps
Given the instantaneous voltages and instantaneous currents over a specified duration (2 power cycles or more), then the following procedure applies to the algorithm;
```
impedance_magnitude = effective_voltage / effective current
time_difference = time_of_voltage_maximum - time_of_current_maximum
if time_difference>0 ,current is lagging meaning the load has +ve reactance (inductor)
if time_difference<0 ,current is leading meaning the load has -ve reactance (capacitor)
angle_of_current_lagorlead_degrees = (360*supply_frequency*time_difference_seconds)
resistance = impedance_magnitude*cosine(angle_of_current_lagorlead_degrees)
reactance = impedance_magnitude*sine(angle_of_current_lagorlead_degrees)
power_factor = cosine(angle_of_current_lagorlead_degrees)
voltage_current_product = effective_voltage*effective_current
watt = voltage_current_product * power_factor
VAR = voltage_current_product * sine(angle_of_current_lagorlead_degrees)
if the load has inductance, corrective_capacitor_Farads = (1/reactance)*(j/(2*pi*frequency)) and disconnect reactor banks if any
if the load has capacitance, corrective_inductor_Farads = (-1*reactance)*(j*(2*pi*frequency)) and disconnect capacitor banks if any
```
