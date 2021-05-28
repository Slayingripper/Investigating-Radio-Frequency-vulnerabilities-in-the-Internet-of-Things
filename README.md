# Investigating-Radio-Frequency-vulnerabilities-in-the-Internet-of-Things
this 

# Introduction 




## Hack RF 
## Zigbee 
The Zigbee protocol is a IOT specific protocol used for the transmission of data from sensors and automotation control networks using the IEEE 802.15.4 standard. It uses very low data datarates of around 250Kpbs which operated on the microwave frequency allocation of 868 , 902-928 Mhz and 2.4 ghz frequencies. Usually higher frequencies are used to transfer data between devices at higher datarates but closer range. Usually Zigbee devices have a maximum range of 100m (assuming propagation allows)

https://www.sciencedirect.com/topics/engineering/zigbee-protocol
### Zigbee infastracture
The structure of the Zigbee network is consists of three main devices. The coordinator , Router and End Device . A zigbee network cannot function without a coordinator as is bridges the device with the network . The coordinator is in charge of storing and the information sent by the end device while the router with retransmit the data to the appropriate device . 
## Bluetooth 

## Harmonics 
Every electornic device which utilises Radio frequencies for communication and operation such as wifi , zigbee  , lora etc.. are prone to harmonic frequecy emission . This is one of the fundamental properties of electromagnetic radiation . Electronic devices are under heavy regulation from bodies like the FCC which are in charge of reducing and controlling the behaiviour of these emissions . 

| Harmonic | No. of waves  | No. of Nodes  | No. of anti-Nodes | Length vs Wavelength Relationship  |
|----------|---------------|---------------|-------------------|------------------------------------|
| 1        | 1/2           | 2             | 1                 | Wavelength = (2/1) * L             |
| 2        | 1             | 3             | 2                 | Wavelength = (2/2) * L             |
| 3        | 3/2           | 4             | 3                 | Wavelength = (2/3) * L             |

L=n/2 (lambda)

λ [wavelength] = c [speed of light] / ƒ [frequency]

When a wave oscllates it will produces harmonic waves with a reduction in bandwidth everytime which results in an oscillation on a different frequency . In our case this could allow for attacks to be carried out by using even less "sophisticated" equipment by transmitting on lower freuquencies.

Harmonics can cause unintended interferece to other devices operating on the frequency which the hormonic will oscillate. As we get closer to the third harmonic and the wavelengh increases it will increase the noise floorof the electrical signal which in turn can cause "jamming" of legitimate signal reaching their intended receivers . Furthermore , they can cause the capacitance level of power factor capacitors to flactuate and inductance of the power supply to become unstable causing the device or neighbouring devices to behave irregularly. 

Harmonic Spurious emission are also a huge issue in electronic devices as they produce unwanted oscillationd close to the fundumental frquency aswell as harmonic frequencies which can cause inteference . For example a device transmitting at exactly 433mhz with a bandwidth of 25 khz will also bleed onto other frequencies well over its bandwidth without proper filtering . This is especially prominent in dual side mode modulations such as Frequency Modulation (FM), Amplitude Modulation (AM) , Dual Side Band (DSB) ,Phase Modulation (PM).
Protocols like Wifi use a combination of Binary Phase Shift keying (BPSK) and Quandrature Phase Shift Keying(QPSK). The protocol switches between modulation types to optimise transmission rate and error correcton .

https://www.tutorialspoint.com/wi-fi/wifi_radio_modulation.htm
https://www.rfwireless-world.com/Terminology/spurious-vs-harmonics.html
https://punchthrough.com/harmonics-part-1-introduction-to-harmonics-ble-2/
### Filtering 
For any device to be FCC compliant it should have adequate filtering to reduce the harmonic emission from the device . The harmonic produced by a device should be segnificantly less powerfull than the fundemental frequency of operation . To limit the spread of spurious emissions and harmonics adequate filtering should be used such as a low pass and high pass filter to only allow emission on a specified frequency range. 