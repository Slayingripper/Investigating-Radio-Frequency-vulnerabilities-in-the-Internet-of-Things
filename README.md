# Investigating-Radio-Frequency-vulnerabilities-in-the-Internet-of-Things

this

# Introduction

## Hack RF

The HackRF is a half-duplex sdr transceiver designed for RF investigation. It has an operating frequency of 1Mhz - 6Ghz with a 8-bit quadrature sample rate. The hackrf has a maximun transmition power of 30mW this makes it suitable for transmittion at close ranges but it prone to emission of sperodic emissions which could compromise nearby equipement if used with amplification equipment.
The HackRF is compatable with GNU-Radio allowing it be calibrated to work with multiple other equipment and protocols. One of the main disadvatages of the HackRF is its subpar receive perfomance .
![HackRF one](https://greatscottgadgets.com/images/h1-preliminary1-445.jpeg)

## Zigbee

The Zigbee protocol is a IOT specific protocol used for the transmission of data from sensors and automotation control networks using the IEEE 802.15.4 standard. It uses very low data datarates of around 250Kpbs which operated on the microwave frequency allocation of 868 , 902-928 Mhz and 2.4 ghz frequencies. Usually higher frequencies are used to transfer data between devices at higher datarates but closer range. Usually Zigbee devices have a maximum range of 100m (assuming propagation allows)

https://www.sciencedirect.com/topics/engineering/zigbee-protocol

### Zigbee infastracture

The structure of the Zigbee network is consists of three main devices. The coordinator , Router and End Device . A zigbee network cannot function without a coordinator as is bridges the device with the network . The coordinator is in charge of storing and the information sent by the end device while the router with retransmit the data to the appropriate device .

## Bluetooth

Bluetooth is a shortrange low power mode for transfering data between two devices. It is usually used to sync between devices in a mesh network, send files between devices , stream music etc. It operates on the 2.4Ghz portion of the spectrum utilising 79 channels of 1mhz bandwidth each. Bluetooth network operates using a frquency hopping to minimise intereference to other devices and try to mitigate any potential impact it might have to other devices. When two devices connect to each other using bluetooth they initiate a handshake signal which usually requires authorisation of both parties with some sort of pop up notification or by entering a one time password. Bluetooth devices are organised a star topology meaning that there is one master server which sends data to multiple slave nodes. For example a master server could be a phone and the slaves are the wireless earphones or speakers.
A bluetooth packet is made up of three parts :

1. Access Code
2. Packet Header
3. Payload

![alt text](https://www.technologyuk.net/telecommunications/communication-technologies/images/bluetooth_packet_format.gif)

This allows the protocol to work either Syncronous mode for voice calls or Asyncronous Mode for data transfer.

https://www.scientificamerican.com/article/experts-how-does-bluetooth-work/

https://techspirited.com/how-does-bluetooth-work
https://ieeexplore.ieee.org/abstract/document/824570?casa_token=dUcTveas6GkAAAAA:B5RAywdmD74wiBePLyszuzFhUsvzuin--HUvxDcrDBfQY0qjGUhoPZE0zQevAXHAdCjfZtP4

### Bluetooth Controller

The Bluetooth controller is in charge of inplimenting the physical layer (Layer 1) of bluetooth which is made up of the radio , baseband and link managment layer. It establishes the initial communication with the destination device using the Host Controller Interface . The link managment layer is in charge of creating that initial connection between two devices in turn use the baseband layer to create an access control system through the radio link layer . 


"Multi-level Bluetooth Intrusion Detection System" (cite)


### Host Controller Interface (HCI)

The HCI layer is a mediator between the controller and host. The host uses the host controller interface to establish a link between it and the bluetooth controller .  

"Multi-level Bluetooth Intrusion Detection System" (cite)

### Bluetooth Host 
The Blutooth Host houses the bluetooth protocols logical stack  components which allow the bluetooth protocol to be used with different applications .

"Multi-level Bluetooth Intrusion Detection System" (cite)


## Harmonics

Every electornic device which utilises Radio frequencies for communication and operation such as wifi , zigbee , lora etc.. are prone to harmonic frequecy emission . This is one of the fundamental properties of electromagnetic radiation . Electronic devices are under heavy regulation from bodies like the FCC which are in charge of reducing and controlling the behaiviour of these emissions .

| Harmonic | No. of waves | No. of Nodes | No. of anti-Nodes | Length vs Wavelength Relationship |
| -------- | ------------ | ------------ | ----------------- | --------------------------------- |
| 1        | 1/2          | 2            | 1                 | Wavelength = (2/1) \* L           |
| 2        | 1            | 3            | 2                 | Wavelength = (2/2) \* L           |
| 3        | 3/2          | 4            | 3                 | Wavelength = (2/3) \* L           |

L=n/2 (lambda)

λ [wavelength] = c [speed of light] / ƒ [frequency]

When a wave oscllates it will produces harmonic waves with a reduction in bandwidth everytime which results in an oscillation on a different frequency . In our case this could allow for attacks to be carried out by using even less "sophisticated" equipment by transmitting on lower freuquencies.

Harmonics can cause unintended interferece to other devices operating on the frequency which the hormonic will oscillate. As we get closer to the third harmonic and the wavelengh increases it will increase the noise floorof the electrical signal which in turn can cause "jamming" of legitimate signal reaching their intended receivers . Furthermore , they can cause the capacitance level of power factor capacitors to flactuate and inductance of the power supply to become unstable causing the device or neighbouring devices to behave irregularly.

Harmonic Spurious emission are also a huge issue in electronic devices as they produce unwanted oscillationd close to the fundumental frquency aswell as harmonic frequencies which can cause inteference . For example a device transmitting at exactly 433mhz with a bandwidth of 25 khz will also bleed onto other frequencies well over its bandwidth without proper filtering . This is especially prominent in dual side mode modulations such as Frequency Modulation (FM), Amplitude Modulation (AM) , Dual Side Band (DSB) ,Phase Modulation (PM).
Protocols like Wifi use a combination of Binary Phase Shift keying (BPSK) and Quandrature Phase Shift Keying(QPSK). The protocol switches between modulation types to optimise transmission rate and error correcton .
Many of these spurious emissions are generated by Low Noise Amplifier embeded in the devices which are used the amplify the low powered signal transmitted from the device. Using this type of amplification causes not only the desired transmition signal to be amplfied but also any hamonics or "noise" it generates by:

"INSERT EQUATION HERE"

<br>

<br>
https://www.tutorialspoint.com/wi-fi/wifi_radio_modulation.htm
https://www.rfwireless-world.com/Terminology/spurious-vs-harmonics.html
https://punchthrough.com/harmonics-part-1-introduction-to-harmonics-ble-2/
### Filtering 
For any device to be FCC compliant it should have adequate filtering to reduce the harmonic emission from the device . The harmonic produced by a device should be segnificantly less powerfull than the fundemental frequency of operation . To limit the spread of spurious emissions and harmonics adequate filtering should be used such as a low pass and high pass filter to only allow emission on a specified frequency range.

One of the advatages on installing filtering is the increase in transmission quality as the packet drop rate deacreses.

https://www.tjprc.org/publishpapers/2-15-1476517420-6.%20Electrical%20-%20IJEEER-Filter%20Application%20Effects%20for%20Removing%20the%20Spurious%20Emissions%20Inducing%20in%20CDMA%20Systems.pdf

## Gnu Radio
![GNU RADIO](https://www.gnuradio.org/imgs/gnuradio_logo_glyphs_as_paths.svg)


GNU RADIO is a open-source software development platform used to create virtual signal processing block which can be implemented with software defined radio such as the Hackrf. By using the platform is allows low cost rf radio exquipment to be "equiped" virtually with decoders , filters , processing blocks to encode and decode data in the RF spectrum. 
Using Gnu Radio allows us to make complex RF signal simulations without the need for expensive hardware thus reducing the cost of testing equipment.

## Attenuation 
https://www.dataloggerinc.com/wp-content/uploads/2016/11/16_Basics_of_signal_attenuation.pdf

https://www.electronics-notes.com/articles/radio/rf-attenuators/what-is-an-rf-attenuator-types.php

Attenuation is the degradation of signal stregth during transmission, this is causes inteferance to devices close to the transmitting device which might cause it to loss data. Attenuation is reprenseted using decibels(dB). Decibels are the logarithms amplification by a factor of 10 by an input signal and devided by the output .

![FORMULA](https://wikimedia.org/api/rest_v1/media/math/render/svg/db593d0adac70afe8299b6e46a122719a48fc0a9)

Attenuation decreases the efficiency of a transmitted electrical signal due the absorbsion or scattering of the photons. One of the main benefits of using 2.4ghz for protocols like wifi and bluetooth is the lack of inteference due to weather conditions.





