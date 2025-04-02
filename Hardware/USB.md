USB uses a pair of wires to transmit data between receiver and device. There are two modes of signaling that I learned about:
- One wire acts as a clock, sending pulses every clock cycle, and the other wire transmits bits that can be read per the clock wire. 
- **Differential signaling (what USB uses):** both the wires act as complements of each other. The receiver has its own clock recovery circuit to distinguish the clock. 
The bits being sent have a few features:
- NRZI encoding: a 1 is represented by the voltage staying the same, a 0 is represented by the voltage changing. Easier to distinguish than 1 is high voltage and 0 is low
- Bit stuffing: Insert a 0 in a run of 1's so that a long stretch of constant signal can be clocked easily
In USB, the receiver constantly polls the device for any data input. This happens once every <1 ms. The polls and responses are sent as packets:
- IN packet sent by the receiver to query whether any data has been changed, or the USB has any new data to send
- OUT packet by the device that represents new data, or a NACK that says nothing has changed / nothing to report
- SETUP / CONTROL packets used for establishing the connection

Historically, most USB devices operate at "half-speed" or "full-speed", the latter of which is magnitudes faster. Two wires for data means each USB connector only requires four pins total - one for power, one for ground, and two data wires.

USB 3.0 introduced a different standard completely, which had full-duplex support for transmission.