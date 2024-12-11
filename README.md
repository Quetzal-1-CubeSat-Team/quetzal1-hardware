# Quetzal-1 Hardware

<p align="center">
<img width="300" src="./media/quetzal_1_badge.png">
</p>

### 📫 Contact Us!

If the information published here was helpful, we'd love to know! Contact us below and let us know how we can help 🙋‍♀️🙋‍♂️!

1. 💌 **Email us:** [satelite@uvg.edu.gt](mailto:satelite@uvg.edu.gt)
2. 🐦 **Reach out on X:** [@quetzal1_uvg](https://x.com/quetzal1_uvg)

For an overview of Quetzal-1, [read our profile!](https://github.com/Quetzal-1-CubeSat-Team)

## Directory Description

This repository serves as the central location for all hardware design files for the Quetzal-1 satellite. We are indebted to the open-source community, as a large part of the hardware and software was inspired and based on open-source platforms, such as [Arduino](https://www.arduino.cc/), and libraries written by its ever-expanding community.

The hardware files for the following subsystems are included in this repository:

1. [ADCS](./ADCS/): contains the hardware design files for the Attitude Determination and Control System (ADCS).
2. [EPS](./EPS/): contains the hardware design files for the Electrical Power System (EPS).
3. [ADM](./ADM/): contains the hardware design files for the Antenna Deployment Mechanism (ADM).
4. [media](./media/): contains miscellaneous photos relating to the satellite in general, that may be of use and serve as reference to the user.

### Internal Part Naming Scheme

Each Printed Circuit Board (PCB) in the design was tracked according to an internal part number (P/N), which is referenced throughout this repository and especially in the hardware source files. It is as follows:

| System  | P/N                                     | Description                                                                     |
|---------|-----------------------------------------|---------------------------------------------------------------------------------|
| ADCS    | `PT-MIS-PCB-001`                        | The ADCS PCB, in charge of passive attitude control and attitude determination. |
| EPS     | `PT-PWR-EPS-002`                        | The main EPS PCB, in charge of energy harvesting, storage and distribution. :information_source: Sometimes also referenced as `PT-MIS-PCB-002`.     |
| EPS     | `PT-MIS-PCB-003`, `-005` through `-008` | The solar panel PCBs for all axes except `Z-`.                                  |
| EPS/ADM | `PT-MIS-PCB-004`                        | PCB containing both the `Z-` solar panel and the ADM.                           |

## How should you cite this repository?

You may cite this repository as shown below. Further information is available in the [CITATION.cff](./CITATION.cff) file.

> Quetzal-1 CubeSat Team. (2022). Quetzal-1 Hardware. https://github.com/Quetzal-1-CubeSat-Team/quetzal1-hardware

## Available Repositories

| Repository               | Description                                                                                                             |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------|
| quetzal1-hardware        | This repository.                                                    |
| [quetzal1-flight-software](https://github.com/Quetzal-1-CubeSat-Team/quetzal1-flight-software) | Contains the software for Quetzal-1 and its subsystems.                                                                 |
| [quetzal1-telemetry](https://github.com/Quetzal-1-CubeSat-Team/quetzal1-telemetry)              | Contains the telemetry and photos transmitted by Quetzal-1 while in orbit. |
| [gr-quetzal1](https://github.com/danalvarez/gr-quetzal1)              | Contains the software used on the Ground Control Station for Quetzal-1, based on GNURadio. |
