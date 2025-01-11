# BMS 12

## Introduction
The battery management system (BMS) is a core component of the solar car. It has numerous objectives:

* Monitor individual cell voltages
* Monitor battery module temperatures
* Balance the voltage across cells
* Protect the cells from over- or under-charge
* Protect the cells from over- or under-temperature
* Monitor pack current
* Protect the pack from over-current
* Open and close contactors to connect the pack to other loads
* Manage vehicle startup and shutdown
* Provide low-voltage (LV) terminals for other modules
* Provide high-voltage HV terminals for two motor controllers and the array
* Connect to the car network via Ethernet and produce telemetry
* Control fans for battery pack cooling

## Background on BMS 12
This is a spring 2024 project to tidy-up BMS and make it ASC-compliant. There was no time to do multiple revisions prior to ASC 2024, so the race version lacks substantial refinement. The team raced with 12.0, with the changes for 12.1 inspired by the bring-up of the design as well as the race experience.

BMS 11.x was never raced, having been designed and brought up during the COVID pandemic from 2020-2022. It technically did work, but was somewhat complicated. The biggest problem with the design was that it had several relays that could potentially apply high voltage to the microcontroller if they were prematurely closed before the low side contactor had finished closing. Naive software, switching several of these relays simultaneously, was prone to burning up the low voltage electronics.

## Changes 12.0.0 --> 12.1.0
* Architectural changes	
	- Replaced low-side relay drivers with current regulators.
	- Changed temperature sensing to PT1000 and moved to stack monitors.
	- Split LV and HV GND across isolation barrier.
	- Switched to isolated RQB150W 12V 150 watt brick from HV buck.
	- Added 7-port Ethernet switch.
	- Replaced several Micro-Fit connectors with Ampseal 35-position.
	- Added additional Ampseal 35-position intended to go to top shell.
* Cell stack monitoring
	- Reduced termination to 2 x 499 ohms to reduce requisite drive strength.
	- Switch from magnetic to capacitive isolation between LTC6811 instances.
	- Annotated LTC6820 strapping options.
	- Changed C0 cell tap RC connection to look like Figure 38.
	- Replaced LDO with buck converter to power LTC6811.
	- Replaced 2-pin headers with DIP switches for cell-skipping.
	- Enlarged bleed resistors to 20 ohm 2512 (1-watt).
	- Changed WDT LED from red to green to make goodness more obvious.
	- Reduced WDT LED drive current by increasing series resistor to 4k7 ohms.
	- Removed GPIO3 LED to make room for PT1000 multiplexing.
	- Added PT1000 multiplexer and buffer amplifier.
	- Replaced cell tap connectors with 14-position RA Micro-Fit.
* Bug fixes
	- Moved R73 from VIN to EN1 to avoid unwanted quiescent red LED.
	- Fixed incorrect USB polarity at STM32.
	- Changed R128 to 4k7 ohms because datasheet requires <=5k.
	- Added amber LED for DC/DC enable.
* CAN interface
	- Switched from SN65HVD256 to TCAN1462V-Q1 to avoid CANTX pull-up to 5P0.
	- Added CAN termination switches.
	- Plumbed silent pin to MCU.
* Misc
	- Added chassis potential-centering capacitors and resistors.
	- Removed buzzer.
	- Added bleed indicator LEDs.
	- Added turret test points to MCP3913 inputs.
	- Added edisc override DIP switch.
	- Removed USB VBUS diode to 5P0.
	- Switched MPPT fuse from solder-in to holder (lower current required).
* Layout
	- Added high- and low-side contactor silkscreen labels.
	- Added +/- silkscreen labels to HV connectors.
	- Fixed TO-247 heatsink-to-heatsink spacing.
	- Fixed TO-247 heatsink footprint pin spacing and spring clip clearance.

## Changes to consider
* Add TP_GRABBY GND points for Saleae convenience.
* Replace LV-to-LVB device to allow bidirectional current flow.
* Ensure 10 mm of clearance around all screw holes.
* Move USB-C to top side.
* Move Micro-SD card slot to top side.
* Move HV bleed control to separate GPIO from precharge.
* Add high side switch to harness LV output; switch to LVB.
* Add BPS strobe interface.
* Add e-stop button interface.
* Consider a mechanism to measure pack to chassis isolation.
* Onboard error display: https://www.good-display.com/product/437.html
* DIP switches to STM32 for mode configuration.
* Measure LV system current.
* Measure HV->LV power converter current.

## Changes 11.2.0 --> 12.0.0
* Add one temperature sensor input per cell input
* Enlarge the bleed resistors to accelerate balancing
* Add fan headers
* Switch from barrier blocks to TE "Elcon" ET connectors for HV
* Add a low-voltage battery for ASC compliance
* Update contactors to modern part
* Update Ethernet PHY to modern part
* Update LV buck to modern part
* Harmonize STM32 SKU to modern vehicle computer
* Remove battery-facing HV->LV buck converter
* Remove excessive relays for sensing
* Use properly-rated precharge relay
* Dramatically speed up precharge
* Clean up bill of materials (BOM)
* Simplify precharge logic
* Add second state control loop
* Add CAN transceivers (may not be useful)
* Add micro-SD card slot (may not be useful)
