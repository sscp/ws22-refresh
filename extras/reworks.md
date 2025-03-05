# WS22 reworks

## Introduction
There are a number of small improvements that can be made to the ~~Tritium~~ Prohelion Wavesculptor 22 that can improve efficiency or quality of life.

## Reduce DC/DC losses
The stock DC/DC is quite old at this point, and there are more-efficient devices available.

## Reduce LED losses
The always-on LED across the low voltage bus dissipates nearly 250 milliwatts. While not a disastrous amount of power for a solar-powered vehicle, it's needlessly wasteful and can be reduced.

## Replace FETs
The stock International Rectifier IRFP4668 have a very-low on-state resistance, but are quite large and have substantial switching losses. More importantly, they are only rated for 200 volts, and it's very easy to exceed that by opening the contactor under regenerative braking. One can remove all 18 MOSFETs are replace them with just six of the Infineon IMW65R007M2H SiC FET.
