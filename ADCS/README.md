# Attitude Determination and Control System #

## Directory Description

This directory contains the original design files for the Attitude Determination and Control System (ADCS) Printed Circuit Board (PCB). As with the rest of the Hardware for Quetzal-1, it was developed using [Altium Designer](https://www.altium.com/). It also contains schematics and PCB prints in PDF format so users can understand the overall design without necessary access to Altium's proprietary software.

The directory is organized as follows:

1. `src/`: contains the original original design files.
2. `output/`: contains project schematics and PCB prints in PDF format, as well as fabrication files (Gerber and NC Drill). It also contains the reference Bill of Materials (BOM) for the PCB.
3. `media/`: contains miscellaneous photos of the PCB that may be of use and serve as reference to the user.

## Conceptual Design Overview

### Passive Magnetic Attitude Control

The ADCS was developed in-house, and it included a passive control system based on a previous mission by a different team: [Colorado Student Space Weather Experiment (CSSWE)](https://lasp.colorado.edu/home/csswe/). Quetzal-1’s ADCS used a [K&J Magnetics D84](https://www.kjmagnetics.com/proddetail.asp?prod=D84) cylindrical magnet (with 0.74  $A \cdot m^2$ magnetic moment) to align the satellite to Earth’s magnetic field and two hysteresis rods, located on mutually orthogonal axes, to stabilize its rotation.

### Attitude Determination

For attitude determination, Quetzal-1's ADCS included an [Adafruit Breakout Board for the BNO055 Inertial Measurement Unit](https://learn.adafruit.com/adafruit-bno055-absolute-orientation-sensor) (IMU), which includes 3-axis accelerometer, gyroscope and magnetometer, as well as a temperature sensor. The accelerometer, however, was flown powered off as linear acceleration data while in free fall was deemed of little value on orbit.

Additionally, 12 photodiodes [(Vishay TEMD6010FX01)](https://www.vishay.com/en/product/81308/) were implemented as Sun sensors, two on each face of the satellite (for redundancy). The selected photodiodes were digitized via a voltage divider and an Analog-to-Digital Converter (ADC) [(Texas Instruments ADC128D818)](https://www.ti.com/product/ADC128D818). All sensors were sampled and controlled by a [Microchip ATMEGA328P](https://www.microchip.com/en-us/product/ATmega328P) microcontroller on the ADCS PCB.

The attitude determination algorithm was based on the SVD method proposed by [(Markley, 1987)](https://www.researchgate.net/publication/243753921_Attitude_Determination_Using_Vector_Observations_and_the_Singular_Value_Decomposition) and was performed on the ground ex post facto.

## Elecrical Design Specifics

### PCB Stackup

The ADCS PCB is a 4-layer PCB in 1 oz copper. The layer stackup is as shown below.

|      Name      |    Material   | Thickness | Constant |
|:--------------:|:-------------:|:---------:|:--------:|
| Top Paste      |               |           |          |
| Top Overlay    |               |           |          |
| Top Solder     | Solder Resist |   0.40mil | 3.5      |
| Top Layer      | Copper        |   1.40mil |          |
| Dielectric 1   | FR-4          |  18.85mil | 4.8      |
| Ground Plane   | Copper        |   1.42mil |          |
| Dielectric 3   |               |  18.85mil | 4.2      |
| Power Plane    | Copper        |   1.42mil |          |
| Dielectric 4   |               |  18.85mil | 4.2      |
| Bottom Layer   | Copper        |   1.40mil |          |
| Bottom Solder  | Solder Resist |   0.40mil | 3.5      |
| Bottom Overlay |               |           |          |
| Bottom Paste   |               |           |          |

### I2C Isolation

The ADCS module communicates via I2C with the On-Board Computer (OBC). However, the Electrical Power System (EPS) PCB contains load switches that turn the ADCS PCB (and other systems) on and off independently. Therefore, the I2C bus on the ADCS PCB was isolated with a [Texas Instruments TCA4311ADGKR](https://www.ti.com/product/TCA4311A/part-details/TCA4311ADGKR) I2C buffer. Without this, a power-off of the ADCS PCB would cause the unpowered slave to pull the whole satellite's I2C bus low.

### Deployment Switches

Although the satellite's deployment switches (used to control satellite power-on when deployed from the JEM Small Satellite Deployer [J-SSOD]) were controlled by the EPS PCB, these were physically mounted on the ADCS PCB. This is the reason for the cutouts on opposing corners of the PCB. The switches can be clearly seen in the upper-left and lower-right corners of the PCB in `media/adcs-engineering-model-test-1.jpg`.

### Additional Hardware for Testing and Software Development

The ADCS PCB contained additional hardware that was only used during the development of the module's software and for other testing purposes. Those components that were not to be mounted for the flight model of the PCB, were clearly designated in the design notes of the schematic.

These testing components include:

1. A battery charging circuit, since the PCB could be powered on by an external battery when not integrated to the rest of the satellite.
2. A 3.3 V voltage regulator, which could be used to power all components on the board when not connected to the EPS power rails.
3. A USB to UART Serial Interface, used to easily program the microcontroller for software development purposes. Note that the [Arduino bootloader](https://docs.arduino.cc/hacking/software/Bootloader) was burned to the microcontrollers to enable UART programming. For flight, the microcontroller was programmed via the included ICSP header and an external programmer.
4. Miscellaneous LEDs and resistors (for I2C address selection and I2C bus pull-up, for example) that were not to be mounted for flight.