# Antenna Deployment Mechanism #

## Directory Description

This directory contains the original design files for the Antenna Deployment Mechanism (ADM) Printed Circuit Board (PCB). As with the rest of the Hardware for Quetzal-1, it was developed using [Altium Designer](https://www.altium.com/). It also contains schematics and PCB prints in PDF format so users can understand the overall design without necessary access to Altium's proprietary software.

The directory is organized as follows:

1. `src/`: contains the original design files.
2. `output/`: contains project schematics and PCB prints in PDF format, as well as fabrication files (Gerber and NC Drill). It also contains the reference Bill of Materials (BOM) for the PCB.
3. `media/`: contains miscellaneous photos of the PCB that may be of use and serve as reference to the user.

## Conceptual Design Overview

The following diagram gives an overview of the components mounted on this PCB (and their interconnections). Please note that this PCB houses both the Antenna Deployment Mechanism, as well as the solar panel corresponding to the satellite's `Z-` axis.

![adm-block-diagram](./src/PT-MIS-PCB-004_v1%20Block%20Diagram.jpg?raw=true "ADM Block Diagram")

### Antenna Deployment Mechanism

The mode of operation for this subsystem is, conceptually, quite simple: it is in charge of releasing the satellite's 4 antennas ([GOMspace, Cat. No. NanoCom ANT430](https://gomspace.com/shop/subsystems/communication-systems/nanocom-ant430.aspx)), 30 minutes after deployment from the International Space Station.

While in storage, each antenna is tied to this PCB using general-purpose, 0.3 mm, nylon fishing line (see `media/` for pictures). The line is knot in such a way that it is also tied around a 5.6 Ohm resistor ([Yageo, Cat. No. MFR50SFTE52-5R6](https://www.digikey.com/es/products/detail/yageo/MFR50SFTE52-5R6/9151636)) that is directly connected to the battery via a load switch ([Texas Instruments, Cat. No. TPS22965](https://www.ti.com/product/TPS22965)). The load switches are controlled via I2C by the Electrical Power System (EPS). When the On-Board Computer determines the 30-minute timer after deployment has expired, it commands the EPS to activate each load switch sequentially, dissipating approximately 3.15 W in the resistors (which are rated for 0.5 W) when the battery is fully-charged. This heats the resistors, thereby melting the fishing line which is wrapped around it. When it melts, the antenna (which is spring loaded) releases and an SPST switch ([Panasonic, Cat. No. ESE18L11C](https://na.industrial.panasonic.com/products/electromechanical/switches/lineup/detector-switches/series/28913/model/28919)), which is normally closed when the antenna is stowed, is used to detect the separation. Each of the switches is connected to the EPS via an I2C GPIO Expander ([Texas Instruments, Cat. No. TCA9539QPWRQ1](https://www.ti.com/product/TCA9539-Q1/part-details/TCA9539QPWRQ1)), to inform the system when each antenna has successfully deployed.

The fishing line knot was tested thoroughly on-ground to ensure the highest possible reliability. It was very important that when the fishing line melted, the antennas released completely and would not become stuck with the fishing line. The following diagram describes the knot that was used:

![knot-step-by-step-diagram](./media/knot_step_by_step_diagram.png?raw=true "Antenna Knot Diagram")

Additional pictures of the knot can be found in `media/`.

### Solar Panel

This PCB also houses one (1) [AZUR SPACE 3G30A](http://www.azurspace.com/images/products/0003401-01-01_DB_3G30A.pdf) solar cell and two (2) [Vishay TEMD6010FX01](https://www.vishay.com/en/product/81308/) photodiodes (for energy harvesting and attitude determination, respectively).

It only contains one solar cell, as opposed to two, because the satellite's camera points outwards from behind this PCB, and so half of it is reserved for a hole for the camera to see through (see `media/adm_bottom_view_1.jpg` in this directory).