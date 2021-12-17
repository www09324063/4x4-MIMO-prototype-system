# 4x4-MIMO-prototype-system
This web page provides a 4x4 MIMO prototyping system in practical wireless MIMO communications. 

The prototyping implements important features of an orthogonal frequency division multiplexing (OFDM) physical layer, with third generation partnership project (3GPP) long-term evolution (LTE) time-division duplex (TDD)-like specifications.
* **Details about of the 4x4 MIMO prototype system** and **channel meaasurements** can refer to the  [4x4-MIMO-prototype-system.pdf](https://github.com/www09324063/4x4-MIMO-prototype-system/blob/main/4x4-MIMO-prototype-system.pdf). 
* **MIMO Channel Database** can be download from GoogleDrive [here](https://drive.google.com/file/d/1-eUTTWh8ZjWfEVatLC91Mi_Zp9zIGL76/view?usp=sharing).

## Table of Contents

- [Hardware Description](#hardware-description)
- [Phsical Layer Description](#phsical-layer-description)
- [MIMO Channel Measurements](#mimo-channel-measurements)
  - [Indoor-office measurements](#indoor-office-measurements)
  - [Indoor-hall measurements](#indoor-hall-measurements)
- [MIMO Channel Database](#mimo-channel-database)


## Hardware Description
<div align=center>
  <img src="https://github.com/www09324063/4x4-MIMO-prototype-system/blob/main/imag/hardware.jpg" width="50%" />
</div>

To measure the channel characteristics of the MIMO channels,  4 universal software radio peripherals (USRP) are used to form a 4x4 MIMO prototyping system, which operating at 3.5GHz microwave band.  

Each USRP comprises two omni-directional antennas, two radio chains, and the respective ADC/DAC modules. It implements OFDM functionality such as (I)FFT  as well as digital front end functionality such as re-sampling on an FPGA. We use 4 antenna elements (2 USRPs) as the RX, thereby emulating a MIMO BS.  

Data arriving from the 4 antennas of BS is forward to the MIMO processors, which are implemented on a independent FPGA device in the PXI-Chassis. The FPGA device comprises MIMO processing operations such as precoding and equalization, as well as channel estimation in frequency domain. 

Two USRPs equipped with 4 antennas are used as transmitters, each USRP is connected with a controller computer. Note that a single USRP supports two antennas. It also supports the signal processing for two single antenna mobile stations which operate independently. Here we utilize 4  antenna to represent four independent users.


## Phsical Layer Description
The prototyping system implements parts of an LTE-like physical layer in TDD mode. Uplink and downlink are based on OFDM using 20 MHz channel bandwidth.

### Radio Frame Format
<div align=center>
  <img src="https://github.com/www09324063/4x4-MIMO-prototype-system/blob/main/imag/RadioFrame.jpg" width="50%" />
</div>

This MIMO system uses a standard 3GPP LTE radio frame structure as shown in Figure \ref{fig:RF}. Radio frames of 10 ms duration are sub-divided into 10 subframes of 1 ms duration each. Each subframe contains two slots of 0.5 ms duration. A slot is further split into 7 OFDM symbols.
###  Resource Block
<div align=center>
  <img src="https://github.com/www09324063/4x4-MIMO-prototype-system/blob/main/imag/Resource%20Block.jpg" width="80%" />
</div>
This OFDM system utilize a total of 1200 subcarriers with the bandwidth 18MHz, of which are divided into 100 resource blocks (RBs), i.e., each RB contains 12 OFDM subcarriers, and the bandwidth of each subcarrier is 15KHz.

### OFDM Symbols Description
Each OFDM symbol carries a single signal type as listed below:
* Primary Synchronization Signal (PSS):The PSS is compliant with the LTE standard . The PSS sequence generation is implemented statically for Cell-ID 0.
* Pilot Signals: The same length-1200 quadrature phase-shift keying (QPSK) sequence is used to derive uplink and downlink pilots. Pilot sequences corresponding to different mobile stations are transmitted in a frequency orthogonal fashion, e.g., a pilot corresponding to mobile station 1 occupies the first subcarrier in each RB. A pilot corresponding to mobile station 2 occupies the second subcarrier in each RB and so forth. Note that in our 4*4 MIMO-OFDM prototyping system, users occupy 4 subcarriers of total 12 subcarriers in each RB. To estimated the MIMO channel, a radio frame must contain at least one uplink pilot symbol. A new MIMO channel estimate is obtained whenever a pilot symbol is received. The data symbol which follows this pilot symbol is equalized using this new channel estimate already. The channel estimate is held constant until the next pilot symbol is received.
* Physical Downlink Shared Channel (PDSCH): Downlink payload data is transmitted over the PDSCH without forward error correction coding. PDSCH processing comprises:
  * Scrambling using a polynomial in accordance to the LTE specifications.
  * Modulation in accordance to the LTE specifications. 
* Physical Uplink Shared Channel (PUSCH): The PUSCH is symmetric to the PDSCH.
* Guard: One OFDM symbol including cyclic prefix (CP) where nothing is transmitted in uplink or downlink direction.
Finally, we summarize the system main parameters as follows:
| **Parameter**     | **Value**    | 
| :-------------: | :-------------: |
| Center Frequency [GHz]      | 3.5     | 
|  Channel bandwidth [MHz]     | 20      | 
| Fast Fourier transform (FT) Size      | 2048      | 
| Number of used subcarriers     | 1200    | 
|  Number of RBs    | 100   | 
|  OFDM symbol duration [us]     |66.67     | 
| OFDM symbols per slot    | 7     | 
| Slot duration [ms]    | 0.5   |

## MIMO Channel Measurements
In the OTA test, we conduct two scenarios of indoor channel measurements, indoor-office, and indoor-hall. Each scenario including the static and dynamic MIMO channels.

<div align=center>
  <img src="https://github.com/www09324063/4x4-MIMO-prototype-system/blob/main/imag/scenario.jpg" width="80%" />
</div>

### Indoor-office measurements
The indoor-office measurements are conducted at a typical office room, where a wealth of scatterers and reflectors exists. 
As shown in (a), the base station is fixed in the central of the office room to collect uplink channel data, and four mobile antennas are separated into two different places.
The first case is a line-of-sight (LOS) case (marked in blue), where users are positioned close to the base station with LOS paths
available. The second case is non-line-of-sight (NLOS)case, where mobile antennas are surrounding the library with the
LOS path blocked by desks and tables (marked in pink red).
The sky blue edges indicate glass doors and windows.
We altered two setup configurations for the indoor-office measurements, including mobile antennas stay still and keep moving at a uniform speed of $1m/s$ inner the office room (horizontal plane only).

### Indoor-hall measurements
For the indoor-hall measurements shown in (b), we also selected the base station as receiver which fixed in the left central of a open indoor-hall.
Four mobile antennas remain stationary or slow-moving at a uniform speed of $1m/s$ in the front semicircle of the base station, which have LOS paths available to the base station.

## MIMO Channel Database
**MIMO Channel Database** can be download from GoogleDrive [here](https://drive.google.com/file/d/1-eUTTWh8ZjWfEVatLC91Mi_Zp9zIGL76/view?usp=sharing).

