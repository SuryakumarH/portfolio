---
layout: ../../layouts/project.astro
title: "Optimizing Warehouse Management"
description: "A Model-Based Approach for Supervisory Control of Automated Guided Vehicles (AGVs)"
image: "/public/assets/images/projects/Warehouse/cover.png"
dateFormatted: Nov 23rd, 2024

<div style="text-align: justify;">
---
## Introduction

The primary objective of this project is to design and implement a supervisory controller for Automated Guided Vehicles (AGVs) in a warehouse setting. The project demonstrates a model-based engineering approach, focusing on synthesizing a supervisor that efficiently coordinates AGV operations. The supervisor ensures robust and safe operation while adhering to a set of requirements that encompass both safety and task optimization.

## System Layout

The AGV system comprises several onboard components, each designed to ensure smooth and reliable operations in the warehouse. These components are integrated into a hierarchy where low-level controllers manage hardware functions, while high-level controllers oversee tasks such as resource allocation and path planning.
</div>

<div class="flex justify-center my-8">
  <img 
    src="/assets/images/projects/Warehouse/Syslayout.png" 
    alt="System Layout" 
    class="max-w-full h-auto rounded-lg"
  />
</div>

<div style="text-align: justify;">

### Key Components
- **Motors:** Enable forward, backward, and rotational motion.
- **Safety Sensors:** Detect obstacles and potential collisions.
- **Barcode Cameras:** Identify the AGV's location and interaction points.
- **Lifting Mechanism:** Handles racks during loading and unloading operations.
- **Battery System:** Monitors power levels and manages charging cycles.
- **High-Level Controllers:**
  - **Resource Allocation Controller (RAC):** Allocates resources such as storage and picking locations.
  - **Path Planning Controller (PPC):** Calculates optimized navigation paths.
  - **Communicator:** Synchronizes operations between controllers and the AGV.

## Functional Components and Their Logic

### Motors
The AGV’s motion is controlled by motors that allow forward, backward, and rotational movement. To prevent abrupt transitions, the motor logic enforces that any directional change must pass through an idle state.

</div>

<div class="flex justify-center my-8">
  <img 
    src="/assets/images/projects/Warehouse/Motormodel.png" 
    alt="System Layout" 
    class="max-w-full h-auto rounded-lg"
  />
</div>


<div style="text-align: justify;">

#### Key Safety Features:
- Motors can only move when the AGV is in a valid operational state.
- Rotational motion is restricted to specific grid points identified by barcode cameras.
- Motors halt immediately when sensors detect obstacles.

### Product Stack Lifter Mechanism
Different aspects of the Product Stack Lifter Mechanism (PSLM) are modeled separately. These include lifter position, lifter motion, and sensors indicating whether the lifter has reached its highest or lowest positions.
</div>

<div class="flex justify-center my-8">
  <img 
    src="/assets/images/projects/Warehouse/PSLM.png" 
    alt="System Layout" 
    class="max-w-full h-auto rounded-lg "
  />
</div>

<div style="text-align: justify;">

## Informal Requirements and Corresponding Models

### Safe Movement
#### Requirement M1:
Special actions, like rotating, may only be performed when the vehicle is at a grid point as indicated by the location barcode.

```cif
requirement {v.motor.CW.c_motion, v.motor.CCW.c_motion} needs v.lbc.Driving;
````
In this report an uncontrolled system by means of a network of automata was modelled in CIF, representing a warehouse robot system. To ensure safe and optimal function, requirements were introduced. Thereafter, a controller was synthesized. Furthermore, the capabilities of CIF were used in order to validate this model, using synthesis on automata that represent desired or undesired behaviour. 

It can be concluded that the main improvement would be to make the uncontrollable model maximally permissive before introducing the requirements. The next step would be to simulate multiple vehicles and to introduce identities to the rack and storage facilities.

</div>