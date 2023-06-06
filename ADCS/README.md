# Attitude Determination and Control System #

## Directory Description

This directory contains the original design files for the Attitude Determination and Control System (ADCS) Printed Circuit Board (PCB). As with the rest of the Hardware for Quetzal-1, it was developed using [Altium Designer](https://www.altium.com/). It also contains schematics and PCB prints in PDF format so users can understand the overall design without necessary access to Altium's proprietary software.

The directory is organized as follows:

1. `src/`: contains the original original design files.
2. `output/`: contains project schematics and PCB prints in PDF format, as well as fabrication files (Gerber and NC Drill). It also contains the reference Bill of Materials (BOM) for the PCB.
3. `media/`: contains miscellaneous photos of the PCB that may be of use and serve as reference to the user.

## Conceptual Design Overview

### Passive Magnetic Attitude Control

The ADCS was developed in-house, and it included a passive control system based on a previous mission by a different team: [Colorado Student Space Weather Experiment (CSSWE)](https://lasp.colorado.edu/home/csswe/). Quetzal-1’s ADCS used a cylindrical magnet ([K&J Magnetics, Cat. No. D84](https://www.kjmagnetics.com/proddetail.asp?prod=D84)) (with a measured 0.74  $A \cdot m^2$ magnetic moment) to align the satellite to Earth’s magnetic field and two hysteresis rods, located on mutually orthogonal axes, to stabilize its rotation [[1]](#user-content-references).

### Attitude Determination

For attitude determination, Quetzal-1's ADCS included an [Adafruit Breakout Board](https://learn.adafruit.com/adafruit-bno055-absolute-orientation-sensor) for an Inertial Measurement Unit (IMU) ([Bosch, Cat. No. BNO055](https://cdn-learn.adafruit.com/assets/assets/000/036/832/original/BST_BNO055_DS000_14.pdf)), which includes a 3-axis accelerometer, gyroscope and magnetometer, as well as a temperature sensor. The accelerometer, however, was flown powered off as linear acceleration data while in free fall was deemed of little value on orbit [[1]](#user-content-references).

Additionally, 12 photodiodes ([Vishay, Cat. No. TEMD6010FX01](https://www.vishay.com/en/product/81308/)) were implemented as Sun sensors, two on each face of the satellite (for redundancy). The selected photodiodes were digitized via a voltage divider and an Analog-to-Digital Converter (ADC) ([Texas Instruments, Cat. No. ADC128D818](https://www.ti.com/product/ADC128D818)). All sensors were sampled and controlled by a microcontroller ([Microchip, Cat. No. ATMEGA328P](https://www.microchip.com/en-us/product/ATmega328P)) on the ADCS PCB [[1]](#user-content-references).

The following diagram gives on overview of the electrical interconnections between the aforementioned components.

![adcs-block-diagram](./src/PT-MIS-PCB-001_v1%20Block%20Diagram.jpg?raw=true "ADCS Block Diagram")

---
**NOTES**

:warning: The photodiodes were the only ADCS components not mounted on this PCB. They were mounted on each solar panel (`PT-MIS-PCB-003` through `-008`).

:information_source: The attitude determination algorithm was based on the SVD method proposed by [[2]](#user-content-references) and was performed on the ground ex post facto.

:information_source: Further information regarding a component selection rationale, in-orbit performance results and an in-depth analysis of this system's behaviour is provided in [[1]](#user-content-references).

---

## Electrical Design Specifics

### I2C Isolation

The ADCS module communicates via I2C with the On-Board Computer (OBC). However, the Electrical Power System (EPS) PCB contains load switches that turn the ADCS PCB (and other systems) on and off independently. Therefore, the I2C bus on the ADCS PCB was isolated with an I2C buffer ([Texas Instruments, Cat. No. TCA4311ADGKR](https://www.ti.com/product/TCA4311A/part-details/TCA4311ADGKR)). Without this, a power-off of the ADCS PCB would cause the unpowered slave to pull the whole satellite's I2C bus low.

### Deployment Switches

Although the satellite's deployment switches (used to control satellite power-on when deployed from the JEM Small Satellite Deployer [J-SSOD]) were controlled by the EPS PCB, these were physically mounted on the ADCS PCB. This is the reason for the cutouts on opposing corners of the PCB. The switches can be clearly seen in the upper-left and lower-right corners of the PCB in `media/adcs-engineering-model-test-1.jpg`.

### Additional Hardware for Testing and Software Development

The ADCS PCB contained additional hardware that was only used during the development of the module's software and for other testing purposes. Those components that were not to be mounted for the flight model of the PCB, were clearly designated in the design notes of the schematic.

These testing components include:

1. A battery charging circuit ([Microchip Cat. No. MCP73811](https://www.microchip.com/en-us/product/MCP73811)), since the PCB could be powered on by an external battery when not integrated to the rest of the satellite. A P-Channel MOSFET ([Diodes, Cat. No. DMG3415U](https://www.digikey.com/en/products/detail/diodes-incorporated/DMG3415U-7/2052768)) was used to select between the `5V` and `VBAT` power sources.
2. A 3.3 V voltage regulator ([Diodes, Cat. No. AP2112K](https://www.diodes.com/assets/Datasheets/AP2112.pdf)), which could be used to power all components on the board when not connected to the EPS power rails.
3. A USB to UART Serial Interface ([FTDI, Cat. No. FT232RL](https://ftdichip.com/products/ft232rl/)), used to easily program the microcontroller for software development purposes. Note that the [Arduino bootloader](https://docs.arduino.cc/hacking/software/Bootloader) was burned to the microcontroller to permit UART programming. For flight, the microcontroller was programmed via the included ICSP header and an external programmer.

    ---
    :information_source: For future revisions of this board, it may be more convenient to use an external USB to UART converter.

    ---

4. Miscellaneous LEDs and resistors (for I2C address selection and I2C bus pull-up, for example) that were not to be mounted for flight.

## References

[1] Alvarez, D. et al. (2023): Design and On-Orbit Performance of the Attitude Determination and Passive Control System for the Quetzal-1 CubeSat, Journal of Small Satellites (JOSS), vol. 12(2), p. 1231–1247.

[2] Markley, F.L. (1988): Attitude Determination Using Vector Observations and the Singular Value Decomposition, Journal of the Astronautical Sciences, vol. 36(3), pp. 245–258, http://www.malcolmdshuster.com/FC_Markley_1988_J_SVD_JAS_MDSscan.pdf, (accessed October 18, 2021).