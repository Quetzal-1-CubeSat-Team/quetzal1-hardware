# Electrical Power System #

## Directory Description

This directory contains the original design files for the Electrical Power System (EPS) Printed Circuit Board (PCB). As with the rest of the Hardware for Quetzal-1, it was developed using [Altium Designer](https://www.altium.com/). It also contains schematics and PCB prints in PDF format so users can understand the overall design without necessary access to Altium's proprietary software.

The directory is organized as follows:

1. `src/`: contains the original original design files.
2. `output/`: contains project schematics and PCB prints in PDF format, as well as fabrication files (Gerber and NC Drill). It also contains the reference Bill of Materials (BOM).
3. `media/`: contains miscellaneous photos of the PCB that may be of use and serve as reference to the user.

---
:information_source: **NOTE**

The `src/` and `output/` directories are further split into two subdirectories each: `eps/` and `solar_panels/`. The former contains the files relating to the main EPS PCB (that is, the PCB that was in charge of energy harvesting, voltage regulation, etc.), while the latter contains the files for the satellite's solar panels. These panels were connected to the main EPS PCB to form the complete Electrical Power System.

---

### Solar Panel Directories

The `solar_panel/` directories contain folders under then following naming scheme: `PT-MIS-PCB-NNN`, where `NNN` corresponds to an internal part number (P/N).

| Internal P/N   | Satellite Axis |
|----------------|----------------|
| PT-MIS-PCB-003 | Z+             |
| PT-MIS-PCB-005 | X+             |
| PT-MIS-PCB-006 | Y-             |
| PT-MIS-PCB-007 | Y+             |
| PT-MIS-PCB-008 | X-             |

---
:warning: **NOTE**

The PCB corresponding to the `Z-` axis (`PT-MIS-PCB-004`) is purposely not listed here (nor is it contained in this directory). This is because, this PCB also houses the satellite's Antenna Deployment Mechanism (ADM). See the `ADM/` directory for the files pertaining to this subsystem.

---

All solar panels contain two (2) [AZUR SPACE 3G30A](http://www.azurspace.com/images/products/0003401-01-01_DB_3G30A.pdf) solar cells and two (2) [Vishay TEMD6010FX01](https://www.vishay.com/en/product/81308/) photodiodes, with the following additions:

1. `PT-MIS-PCB-005` contains, additionally, the Remove Before Flight (RBF) switch: [Cinch 133-3701-401](https://www.belfuse.com/resources/productinformations/cinchconnectivitysolutions/johnson/pi-ccs-john-133-3701-401.pdf).
2. `PT-MIS-PCB-006` contains, additionally, the Flight Preparation Panel (FPP) connector, which is used to interface with the satellite when fully assembled.
3. `PT-MIS-PCB-008` contains, on the internal silk screen, the names of all the students, professors, engineers and volunteers that, at the time of fabrication of this PCB, had participated in this project, contributing to its eventual (and resounding) success. We owe a debt of gratitude to them all.