# Lisa 2 CPU Card

This project seeks to reproduce the Lisa 2 CPU card as faithfully to the original layout as possible. All ICs, traces, and silkscreening are located as close as possible to their original positions on an OEM card and the most absolute minimum of changes have been applied. These changes can be found in the section below titled "Modifications".

NOTE: This card has been confirmed to boot successfully into LOS and MacWorks.

The Lisa 2's CPU hardware is contained on a single dedicated PCB in the card stack. This card contains sub-sections responsible for the following aspects of the Lisa 2:

- The Motorola 68000 CPU itself;
- Error detection logic;
- Memory management;
- Video signal generation, timing, and VRAM management;
- Clock circuitry; and
- Minor I/O functionality.

The CPU card interfaces with the system bus via a 120-pin card edge connector whose pins are 1.4mm wide across a 2.54mm pitch, using a readily available and currently produced female connector on the motherboard (backplane). There are three factory bodge wires and one undocumented ceramic disc capacitor which have now been integrated directly into the design of this card. The original traces which were cut in order to produce the bodges have been removed and are replaced by the connections the bodges were added to create. The capacitor has been added with its own component designation (C43) and silkscreen in order to prevent users from having to solder the capacitor directly to the IC's legs on which it was originally soldered. Additionally, some passive components listed in the schematics are not present on the original hardware and, thus, are also not present on this card. These and other corrections/errata may be found below.

## Resources Found In This Project

In this project, you will find miltuple directories containing different project components. These include:

1. KiCAD project files (as well as an archived ZIP version).

2. Gerber files for the current board revision; these may be uploaded to the PCB manufacturer of your choice for production.

3. Gerber files for the v1.1 board revision; these represent the final Gerber output from the original EasyEDA project and are retained for archival purposes. These can be found in the legacy directory.

4. Schematics exported from KiCAD which detail the PCB design.

5. Preview images of the final Gerber output.

# Errata, Corrections, and Modifications

## Factory Bodges

The following bodges have been corrected in this card's design to be included as physical traces which remove the original incorrect traces altogether and replace them with the correct required traces.

1. Original Connection: U1D_12 > U2D_4
   Corrected Connection: U1D_11 > U2D_4

2. Original Connection: U3C_2 > U5D_14
   Corrected Connection: U1D_2 > U5D_14

3. Original Connection: U4A_4 > U2B_3
   Corrected Connection: U1B_8 > U2B_3

## Components Not Featured On PCB

1. R18 (1K) which, in the schematics pulls up the line between U3C_1, U3B_13, U3B_5, U3C_15, U3B_3, U4B_5, U4B_3, U2B_5, U4B_11, U4B_3, U2B_1, U4B_15, U2B_11, and U2B_13, is not present on the CPU card revision this design was based off of (620-0119 Rev. H). RP1_5 is also connected to this network and seems to fulfill a similar purpose.

2. R19 (3.3K) which, in the schematics pulls up the VMA line between U13A_19 (CPU pin 19) and U8C_8 (74LS244 pin 8), is not present on the CPU card revision this design was based off of (620-0119 Rev. H).

3. DS1 which, in the schematics is an LED tying U11C_2 to GND, is not present on the CPU card revision this design was based off of (620-0119-H). It is present on some other revisions, however.

## Schematic Errata

1. Some versions of the schematics indicate connector pins 1 and 2 are /SH0 and /SL0 respectively. These are backwards (pin 1 should be /SL0 and pin 2 should be /SH0) and corrected in later printings of the schematics.

2. Four pins on RP1 are connected incorrectly in the schematic to a family of signal lines:
   - RP1_1 shows to be tied to the /RO line in the schematics; it is actually tied to the /IO line
   - RP1_14 shows to be tied to the /IO line in the schematics; it is actually tied to the /RO line
   - RP1_9 shows to be tied to the /MEM line in the schematics; it is actually tied to the /STK line
   - RP1_25 shows to be tied to the /STK line in the schematics; it is actually tied to the /MEM line

3. U11C_3 shows to be tied to the UD7 line in some versions of the schematics. It is instead tied to U11C_4/GND on the CPU card revision this design was based off of (620-0119 Rev. H).

## Modifications

1. The ceramic disc capacitor bridging U5C_11 (/HDMSK) to U5C_8 (GND) was originally soldered straight to the pins of the IC. This has been removed and added as a distinct component with a designated number and mask - C43 - and is located adjacent and in parallel to C21.

2. The three unpopulated pins to the right of U14D_23 (EPROM) are shown in the schematics as an undesignated jumper between the UA12 line and +5V. The default configuration is a connection between U13A_40 and U13D_23/U14D_23. A numerical designator and mask have been added - J2 - and the pads resized to accept standard 2.54mm pitch male header pins.

3. The array of pins below the clock circuit have been reduced to only the ones with signals connected (GND and INVID) and documented in the KiCAD schematic. A numerical designator and mask have been added - J3 - and the pads resized to accept standard 2.54mm pitch male header pins.

4. The two pins to the right of pin 63 on the 68000 CPU (GND and /RSTSW) have been documented in the KiCAD schematic. A numerical designator and mask have been added - J4 - and the pads resized to accept standard 2.54mm pitch male header pins.

5. The four pins in a rectangular arrangement above U1E were originally an undocumented pad for a DIP14 oscillator can. A numerical designator and mask have been added - OSC - for this component if you wish to use a standard 20.000 MHz oscillator or a programmable oscillator with the more accurate 20.37504MHz value.

6. The diode symbol (triangle and bar) near CR1 has been removed due to lack of space; the original component symbol (rectangle with polarity indicator bar) is retained, however.

## Board Revisions

1. Version 1.0 of this PCB failed to connect the power and ground pins of U5A to their corresponding rails. This is corrected in version 1.1.

2. Version 1.1 of this PCB corrects power and ground rail assignments for U5A.

3. Version 2.0 of this PCB has been compiled using KiCAD and has minor layout/silkscreening changes due to differences between EDA programs. The board is electrically identical in all other respects, however.
