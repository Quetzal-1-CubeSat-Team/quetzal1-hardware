# Quetzal-1 Hardware

## An overview of Quetzal-1

Quetzal-1 was a 1U CubeSat developed by an engineering team from [Universidad del Valle de Guatemala](https://www.uvg.edu.gt/) (UVG). The satellite was deployed from the International Space Station's (ISS) KiboCUBE module, on April 28, 2020, and operated succesfully in space from the day of deployment to November of the same year. This amounted to 211 days of operation, which validated the performance of all systems on-board.

![fully-assembled-satellite-front](./media/fully_assembled_satellite_front.jpg?raw=true "Quetzal-1")

General information on the project is available on [the official site](https://www.uvg.edu.gt/cubesat/), including news and scientific publications that have been released throughout the project's lifetime. You can also check out [this live session on Arduino's EDUvision](https://youtu.be/YOHguG6epe4?t=378), where one of our team members speaks about the story behind Quetzal-1, from its inception to the time our satellite spent in space!

## Our purpose

This repository serves as the central location for all hardware design files for the Quetzal-1 satellite. We are indebted to the open-source community, as a large part of the hardware and software was inspired and based on open-source platforms, such as [Arduino](https://www.arduino.cc/), and libraries written by its ever-expanding community.

Our purpose is to provide a design reference for a satellite that was fully operational for 211 days in orbit, that it may serve as a stepping stone for future novice teams. Technology is being countinously democratized, and this is our little grain of sand in aim of doing just that: enabling access to space, and its wondrous possibilities, for everyone.

## Directory Description

The hardware files for the following subsystems are included in this repository:

1. `ADCS/`: contains the hardware design files for the Attitude Determination and Control System (ADCS).
2. `EPS/`: contains the hardware design files for the Electrical Power System (EPS).
3. `ADM/`: contains the hardware design files for the Antenna Deployment Mechanism (ADM).
4. `media/`: contains miscellaneous photos relating to the satellite in general, that may be of use and serve as reference to the user.

### Internal Part Naming Scheme

Each Printed Circuit Board (PCB) in the design was tracked according to an internal part number (P/N), which is referenced throughout this repository and especially in the hardware source files. It is as follows:

| System  | P/N                                     | Description                                                                     |
|---------|-----------------------------------------|---------------------------------------------------------------------------------|
| ADCS    | `PT-MIS-PCB-001`                        | The ADCS PCB, in charge of passive attitude control and attitude determination. |
| EPS     | `PT-PWR-EPS-002`                        | The main EPS PCB, in charge of energy harvesting, storage and distribution. :information_source: Sometimes also referenced as `PT-MIS-PCB-002`.     |
| EPS     | `PT-MIS-PCB-003`, `-005` through `-008` | The solar panel PCBs for all axes except `Z-`.                                  |
| EPS/ADM | `PT-MIS-PCB-004`                        | PCB containing both the `Z-` solar panel and the ADM.                           |