# 4x4-MIMO-prototype-system
This web page provides a 4x4 MIMO prototyping system in practical wireless MIMO communications. 

The prototyping implements important features of an orthogonal frequency division multiplexing (OFDM) physical layer, with third generation partnership project (3GPP) long-term evolution (LTE) time-division duplex (TDD)-like specifications.
* **Details about of the 4x4 MIMO prototype system** and **channel meaasurements** can refer to the  [4x4-MIMO-prototype-system.pdf](https://github.com/www09324063/4x4-MIMO-prototype-system/blob/main/4x4-MIMO-prototype-system.pdf). 
* **MIMO Channel Database** can be download from GoogleDrive [here](https://drive.google.com/file/d/1-eUTTWh8ZjWfEVatLC91Mi_Zp9zIGL76/view?usp=sharing).

## Table of Contents

- [Hardware Description](#hardware-description)
- [Radio Frame Format](#radio-frame-format)
- [MIMO Channel Measurements](#mimo-channel-measurements)
  - [Indoor-office measurements](#indoor-office-measurements)
  - [Indoor-hall measurements](#indoor-hall-measurements)
- [MIMO Channel Database](#mimo-channel-database)


## Hardware Description


![system1](https://user-images.githubusercontent.com/48883247/146186261-12aa8764-4b44-4f1f-979b-86800d063075.jpeg)

&nbsp;&nbsp; To measure the channel characteristics of the MIMO channels,  4 universal software radio peripherals (USRP) are used to form a 4x4 MIMO prototyping system, which operating at 3.5GHz microwave band.  

&nbsp;&nbsp;&nbsp;&nbsp;Each USRP comprises two omni-directional antennas, two radio chains, and the respective ADC/DAC modules. It implements OFDM functionality such as (I)FFT  as well as digital front end functionality such as re-sampling on an FPGA. We use 4 antenna elements (2 USRPs) as the RX, thereby emulating a MIMO BS (Fig. \ref{fig:HD}).  

&nbsp;&nbsp;Data arriving from the 4 antennas of BS is forward to the MIMO processors, which are implemented on a independent FPGA device in the PXI-Chassis. The FPGA device comprises MIMO processing operations such as precoding and equalization, as well as channel estimation in frequency domain. 

&nbsp;&nbsp;Two USRPs equipped with 4 antennas are used as transmitters (Fig. \ref{fig:HD}), each USRP is connected with a controller computer. Note that a single USRP supports two antennas. It also supports the signal processing for two single antenna mobile stations which operate independently. Here we utilize 4  antenna to represent four independent users.


## Phsical Layer Description

## MIMO Channel Measurements

### Indoor-office measurements

### Indoor-hall measurements

## MIMO Channel Database

## Install

This module depends upon a knowledge of [Markdown]().

```
```

### Any optional sections

## Usage

```
```

Note: The `license` badge image link at the top of this file should be updated with the correct `:user` and `:repo`.

### Any optional sections

## API

### Any optional sections

## More optional sections

## Contributing

## Liscense

See [the contributing file](CONTRIBUTING.md)!

PRs accepted.

Small note: If editing the Readme, please conform to the [standard-readme](https://github.com/RichardLitt/standard-readme) specification.

### Any optional sections
