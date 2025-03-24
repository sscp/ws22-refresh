# WS22 Companion PCBA

## Introduction
This circuit board pairs with the Wavesculptor 22 to wrap its electrical interface and soften some rough edges around the OEM hardware. It is meant to pair with an additional enclosure to better seal and cool the motor controller.

## New features vs original Wavesculptor 22
* Adds substantial DC bus capacitance to reduce voltage ripple.
* Puts a very large TVS diode across the HV bus to reduce likelihood of EOS.
* Adds capacitance from the DC bus to the chassis to mitigate charge injection.
* Fan controller for thermal management.
* Resolver, differential- or single-ended encoder, and Hall sensor inputs.
* Switchable CAN termination.
* Ethernet connection to onboard STM32.
* USB DFU or SWD programming.
* Ampseal connectors for motor and bus harness interfaces.
* Isolated pseudo "motor interface board" interface to the Wavesculptor 22.

## Changes 1.0.0 --> 1.1.0
* Consider onboard buck-boost to produce stable rail for resolver excitation.
