# Quetzal-1 Hardware

<p align="center">
<img width="300" src="./media/quetzal_1_badge.png">
</p>

For an overview of Quetzal-1, [check this out!](https://github.com/Quetzal-1-CubeSat-Team)

## Directory Description

This repository serves as the central location for all hardware design files for the Quetzal-1 satellite. We are indebted to the open-source community, as a large part of the hardware and software was inspired and based on open-source platforms, such as [Arduino](https://www.arduino.cc/), and libraries written by its ever-expanding community.

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

## Available Repositories

| Repository               | Description                                                                                                             |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------|
| quetzal1-hardware        | This repository.                                                    |
| [quetzal1-flight-software](https://github.com/Quetzal-1-CubeSat-Team/quetzal1-flight-software) | Contains the software for Quetzal-1 and its subsystems.                                                                 |
| [gr-quetzal1](https://github.com/danalvarez/gr-quetzal1)              | Contains the software used on the Ground Control Station for Quetzal-1, based on GNURadio. |