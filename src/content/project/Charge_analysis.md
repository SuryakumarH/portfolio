---
layout: ../../layouts/project.astro
title: "Comparison of Li-ion Battery Performance at 24°C and 4°C"
description: Analysis of Li-ion battery charging cycles using NASA's PCoE dataset to identify voltage behavior patterns and anomalies
image: ""
dateFormatted: Oct 1st, 2024
---
<div style="text-align: justify;">

## Introduction
Li-ion batteries are widely used in modern energy storage systems due to their high energy density, efficiency, and reliability. However, their performance can vary significantly with ambient temperature, which influences key parameters such as charging speed, stability, and long-term health. 

This study utilizes NASA's [Prognostics Center of Excellence (PCoE)](https://www.nasa.gov/intelligent-systems-division/discovery-and-systems-health/pcoe/pcoe-data-set-repository/) dataset to analyze charge cycle behavior at two temperatures: 24°C, representing typical operating conditions, and 4°C, simulating colder environments. By comparing the voltage-time profiles of the charge cycles, we aim to identify temperature-induced variations in charging behavior and assess their implications for battery performance and stability.

## Objective
The primary objective of this study is to evaluate the differences in charge cycle behavior between 24°C and 4°C, focusing on voltage stability, anomalies, and overall performance trends. This analysis provides insights into how ambient temperature impacts the charging characteristics of Li-ion batteries, serving as a foundation for future investigations into the effect of temperature on State of Health (SOH).

## Comparison of Charge Cycles at 24°C and 4°C

### Performance at 24°C
At 24°C, the charge cycles displayed typical Li-ion battery characteristics:
- **Initial Phase (0–10 seconds):** Voltage stabilized between 3.3 and 3.7 V as the battery reached equilibrium.
<div class="flex justify-center my-8">
  <img 
    src="/assets/images/projects/Battery_cycle/charge_cycle/24atfirst12s.png" 
    alt="Voltage shifts in the inital phase" 
    class="max-w-full h-auto rounded-lg"
  />
</div>

- **Constant-Current (CC) Phase (1500–3200 seconds):** Voltage plateaued at around 4.2 V, with constant current being applied.

<div class="flex justify-center my-8">
  <img 
    src="/assets/images/projects/Battery_cycle/charge_cycle/1500-3000.png" 
    alt="voltage plateaued at around 4.2V" 
    class="max-w-full h-auto rounded-lg"
  />
</div>

- **Constant-Voltage (CV) Phase (Last 1000 seconds):** Voltage dropped from 4.25 to 4.12 V due to current reduction to prevent overcharging.

<div class="flex justify-center my-8">
  <img 
    src="/assets/images/projects/Battery_cycle/charge_cycle/final.png" 
    alt="voltage drop around the final cycle" 
    class="max-w-full h-auto rounded-lg"
  />
</div>

The cycle length was approximately 11,000 seconds, stabilizing around 4.18 V at the end of the charge. However, two anomalies were observed:
1. One cycle exhibited an unusually high initial voltage of 9 V.
2. Another cycle started at 0 V with erratic fluctuations.  
These anomalies could result from sensor malfunctions, damaged cells, or measurement errors.

### Performance at 4°C
At 4°C, the charging behavior was more stable:
- **After Initial Stabilization (1000 seconds):** Voltage consistently stayed within 4.20–4.21 V, with minimal fluctuations.
<div class="flex justify-center my-8">
  <img 
    src="/assets/images/projects/Battery_cycle/charge_cycle/f10s.png" 
    alt="voltage raise in the intial 10 seconds" 
    class="max-w-full h-auto rounded-lg"
  />
</div>

- **Transient Voltage Drop (1800–3200 seconds):** A recurring millivolt-scale drop was observed, likely due to adjustments in the charging control system.

<div class="flex justify-center my-8">
  <img 
    src="/assets/images/projects/Battery_cycle/charge_cycle/1000-12000.png" 
    alt="voltage fluctuation after transient" 
    class="max-w-full h-auto rounded-lg"
  />
</div>

- **Voltage Increase (7000–8200 seconds):** Slight voltage increases were noted, likely caused by localized heat generation improving ion mobility.

Unlike at 24°C, no significant anomalies were observed at 4°C. The voltage profile remained stable and predictable throughout the cycle, indicating well-regulated charging under colder conditions.

### Key Differences
1. **Voltage Stability:**  
   - At 24°C, voltage fluctuations were more pronounced, especially during the CV phase.  
   - At 4°C, voltage was highly stable after the initial stabilization.

2. **Cycle Duration:**  
   Both temperatures yielded similar cycle lengths (~11,000 seconds), though charging at 4°C was less efficient due to increased resistance and slower reaction kinetics.

3. **Anomalies:**  
   - Significant anomalies were observed at 24°C (e.g., voltage spikes and erratic behavior).  
   - At 4°C, no anomalies were noted, reflecting better consistency at lower temperatures.

4. **Performance Implications:**  
   - At 24°C, charging is faster but more variable, potentially causing higher stress on the battery.  
   - At 4°C, charging is slower but highly stable, suggesting less wear and better long-term health.

## Conclusion
The comparison between 24°C and 4°C charge cycles highlights a trade-off between charging speed and stability. While 24°C supports faster charging with typical Li-ion behavior, it exhibits more voltage fluctuations and anomalies, potentially stressing the battery. In contrast, 4°C results in slower charging but offers greater stability, with minimal fluctuations and no significant anomalies.

These findings suggest that colder temperatures may enhance battery longevity by reducing stress, whereas moderate temperatures are more suitable for speed-critical applications. Future work will explore the effect of temperature on SOH to provide further insights into optimizing battery performance across varying environmental conditions.


[Visit NASA's PCoE Dataset](https://www.nasa.gov/intelligent-systems-division/discovery-and-systems-health/pcoe/pcoe-data-set-repository/)

### Citation
B. Saha and K. Goebel (2007). “Battery Data Set”, NASA Prognostics Data Repository, NASA Ames Research Center, Moffett Field, CA.  
[Link to Dataset](https://www.nasa.gov/intelligent-systems-division/discovery-and-systems-health/pcoe/pcoe-data-set-repository/)
