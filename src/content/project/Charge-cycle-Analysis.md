---
layout: ../../layouts/project.astro
title: "Analysis of Li-Ion Battery Charge Cycles"
description: Analysis of Li-ion battery charging cycles using NASA's PCoE dataset to identify voltage behavior patterns and anomalies
image: ""
dateFormatted: Oct 1st, 2024
---
<div style="text-align: justify;">


## Objective and Introduction

This study leverages a dataset from the NASA Prognostics Center of Excellence (PCoE) to analyze charging and discharging behaviors of Li-ion batteries under varying conditions. The dataset contains detailed records of experiments on Li-ion batteries, The dataset contains 616 cycles measured at an ambient temperature of 24°C. The cycles were processed by filtering them based on their type (charge, discharge, impedance). For charge cycles, time and voltage data were extracted and plotted to visualize voltage behavior over the full charging duration. The plotted data revealed several key observations about the typical charging pattern of a Li-ion battery.

In this analysis, we are now adding a comparison by analyzing charge cycles measured at a lower temperature of 4°C. This aims to explore how ambient temperature influences charging behavior and to determine whether there are significant differences in voltage behavior, stabilization points, or anomalies between the two temperature settings. This initial comparison provides insights into the role of temperature in battery performance, with the broader question of its impact on State of Health (SOH) reserved for future studies.



## Data Processed and Observation
The dataset was processed by filtering cycles based on their type (charge, discharge, impedance). For charge cycles, time and voltage data were extracted and plotted to visualize voltage behavior over the full charging duration. The plotted data revealed several key observations:

Initial Voltage Levels (0–10 Seconds):
The voltage starts between 3.3 and 3.7 V, drops slightly, and stabilizes. This behavior reflects the battery reaching equilibrium after the initial current application. The slight drop and stabilization are typical as the electrochemical reactions stabilize during the early stage of charging.

Voltage Plateau (1500–3200 Seconds):
During this period, the voltage stabilizes around 4.2 V, characteristic of the constant-current (CC) phase of charging. In this phase, the current remains constant while the voltage gradually rises to 4.2 V, the nominal maximum for most Li-ion cells.

Recurring Voltage Drop Before Full Charge (1000 Seconds Before End):
A recurring drop from 4.25 to 4.12 V is observed, followed by stabilization at 4.18 V. This behavior likely marks the transition to the constant-voltage (CV) phase of charging. During this phase, the current decreases as the voltage is held constant to avoid overcharging, causing minor voltage fluctuations.

End of Cycle Stabilization:
As the cycle concludes, the voltage stabilizes around 4.18 V. This marks the end of the CV phase, where the battery reaches its maximum state of charge with minimal current flow.

Anomalies in Two Cycles:

Cycle with 9 V: This anomaly is unusual and could indicate a measurement error, sensor malfunction, or a damaged battery cell. Further investigation is required to confirm the cause.
Cycle with 0 V: This behavior may result from a deep discharge scenario, where the battery was fully depleted before charging, or it might represent a fault in the battery or the recording equipment.

## Conclusion
Overall, the charging behavior aligns closely with expected Li-ion battery characteristics. This study provides a foundation for further exploration into how temperature influences battery performance, which will be addressed in subsequent research.


[Visit NASA's PCoE Dataset](https://www.nasa.gov/intelligent-systems-division/discovery-and-systems-health/pcoe/pcoe-data-set-repository/)

### Citation
B. Saha and K. Goebel (2007). “Battery Data Set”, NASA Prognostics Data Repository, NASA Ames Research Center, Moffett Field, CA.  
[Link to Dataset](https://www.nasa.gov/intelligent-systems-division/discovery-and-systems-health/pcoe/pcoe-data-set-repository/)

</div>