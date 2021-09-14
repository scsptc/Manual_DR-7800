# Installation

The installation of the PTC-IIpro is simple, as all settings are done
via software. You need only correctly configure the cable between the
PTC-IIpro and transceiver, if this is not already available.

<img src=".//media/image2.wmf" style="width:6.01389in;height:1.22222in" alt="ProBack" />

Figure 3.1: The PTC rear panel.

## Power supply

The PTC-IIpro has two inputs for its power connections which can be used
alternatively. Either connect via the DC-in supply socket at the rear of
the unit, or via the connector for the short-wave transceiver (Audio).
Both connections are decoupled with diodes and protected against reverse
polarity. An input voltage between 10…20 VDC is allowed, the current
consumption depends due to use of a switch mode regulator internally on
the input voltage and how the PTC-IIpro is equipped (e.g. Modems, RAM
etc) and also the present processor speed. It is usually around 200 mA
at 13.8 V. Basically the higher the input voltage the lower the current
consumption. The power supply inputs on the PTC-IIpro are especially
filtered so that harmonics of the switch mode regulator cannot pass
outside the unit. The inputs are also protected by a self-resetting
fuse.

## The serial interface (RS232/V24)

The **SCS**-PACTOR controller communicates with the computer or terminal
via a serial interface using the RS232/V24 standard.

For communication between PTC and computer, the data format is **8 bits,
1 stopbit, no parity and half duplex**. The baudrate can either be
automatically sensed by the PTC, or set via a command to a given value
(see **SERBaud** command, chapter 6.87, page 100).

If the auto baudrate sensing is active, then, after switching on, the
PTC waits for keyboard input. **AUTOBAUD** and **press CR** are
displayed alternately on the digital display. It will then wait, until
either the operator, or the terminal program, sends an appropriate
character. The PTC reacts to \<CR>, \<ESC>, and the freely programmable
ESCchr (refer to chapter 6.39, page 79). Due to the internal operation
of the processor, the auto baudrate sensing can use only characters with
an odd ASCII value: \<CR> (ASCII 13), \<ESC> (ASCII 27) or as an example
for the freely programmable ESCchr \<Ctrl-A> (ASCII 1), \<Ctrl-C> (ASCII
3).

The connection for the serial interface is the 9-pole SUB-D socket on
the rear of the PTC. The connection type is that of a modem (DCE) with a
9-pole SUB-D socket. The PTC can thus be connected to the computer with
a standard 9-pole cable (1 to 1 connections). All handshaking lines are
connected and can be controlled by the PTC. In the present PACTOR
software, however, handshaking is not used.

1.  CD - Output (Scan Stop).

2.  TxD - Transmit data output (to computer).

3.  RxD - Receive data input (from computer).

4.  DTR - Input (RxD secondary serial port).

5.  Ground (GND).

6.  DSR - Output.

7.  CTS - Input.

8.  RTS - Output.

9.  RI - Output (TxD secondary serial port).

<img src=".//media/image3.wmf" style="width:2.22222in;height:0.88889in" />

Figure 3.2: RS232 Connections

For more information for the Scan-Stop-Signal (refer to chapter 13.23,
page 212).

The handshake signals (pin 4 and 9) are used as secondary RS232 channel
e.g. to connect a GPS receiver to the PTC-IIpro.

## Connections to the transceiver

PACTOR-II uses Differential Phase Shift Keying (DPSK), which leads to a
very narrow bandwidth signal. In order to maintain this advantage of
PACTOR-II on the bands, correct setting up of the transceiver is
required. Overdriving of the transceiver will lead to a greatly
increased bandwidth. The optimal adjustment from the PTC-IIpro to the
radio equip­ment is described in chapter 3.3.4 on page 17.

**The complex PACTOR-II modulation scheme is totally different, and has
nothing what­soever to do with simple FSK. It is therefore IMPOSSIBLE to
use the FSK modulators found in some transceivers to generate the
signal. The PACTOR-II signal must always go via the indirect route, by
using SSB to generate the HF signal. This is of no disadvantage
providing the transceiver is not overdriven.**

Some hints to adjust the settings of your transmitter:

-   If possible use a 500 Hz IF-filter. Never use a IF-filter with a
    smaller bandwidth than 500 Hz! IF filter (SSB-filter) with wider
    bandwidths won´t cause problems at all. Although the filtering by
    the DSP of the PTC-IIpro is always optimized, it is desirable to
    prevent noise from the input of the PTC-IIpro as far as possible.

-   Under no circumstances use audio processors. The peech-compressor of
    the transceiver will damage the PACTOR-II signal in the same way as
    external DSP audio filters being so popular at the moment. These
    external DSP audio filters create inpredictable signal propagation
    delays which are absolutely undesirable. The PTC-IIpro filters the
    signal optimal with the integrated DSP and needs no “external help”.

-   Noise blanker and notch filter should be switched off.

The PTC is connected to the transceiver via an 8 PIN DIN socket.

**PIN 1:** **Audio output from the PTC to the transmitter.** The
PTC-IIpro supplies a pure audio signal to the microphone input of the
transceiver. The output amplitude can be adjusted with the **FSKA** and
**PSKA** commands from 30 to 3000 mV (peak to peak) open circuit. The
output impedance of the PTC-IIpro is 1 kΩ.

**PIN 2:** **Ground (GND).** Collective grounding point for all signals.

**PIN 3:** **PTT output.** While transmission this output from the
PTC-IIpro is grounded, so that virtually all modern transceivers are
suitable. A VMOS-field-effect transistor is used as the switch, which
gives optimum results. The switched current should not exceed 1 A.

**PIN 4:** **Audio from the receiver to the PTC-IIpro.** The PTC-IIpro
gets its information directly from the loudspeaker output of the
receiver. The volume should not be turned up too far. A *fairly low*
volume is quite sufficient. It is better to take the AF signal from a
low level output which is independent of the volume control. These
outputs are often labeled AUX or ACC. The input impedance of the PTC is
47 kOhm. The PTC-IIpro operates with an input signal down to approx. 5
mV<sub>RMS</sub> and should not exceed 1 V<sub>RMS</sub>.

**PIN 5:** **Optional power supply input.** The PTC can be supplied with
power via this input. This is especially useful if the transceiver gives
a power supply output via the AUX socket. The PTC-IIpro requires
approximately 9 to 20 Volts DC at a maximum of 1A.

**PIN 7:** **FSK output from the PTC to the transmitter.** When using
the modes PACTOR-I, AMTOR and RTTY, an additional FSK keying output is
available. This may be connected to the FSK input of the transmitter
(often labeled as RTTY). The PTC-IIpro output uses TTL levels. High is
equivalent to Mark, low is Space.

The A0/A1 connections might be used for automatic and frequency
dependent antenna switching. For more information refer to chapter
13.25.2 on page 213.

**PIN 6:** **A1.** General purpose switch output (can e.g. be used to
control an antenna switch). When active, the output is switched to
ground (for technicians: open Drain).

**PIN 8:** **A0.** General purpose switch output (can e.g. be used to
control an antenna switch). When active, the output is switched to
ground (for technicians: open Drain).

Use the attached 8-pole DIN cable to connect the PTC-IIpro to the
transceiver:

| **PIN** | **Color** |     |     | **PIN** | **Color** |     |     |
|---------|-----------|-----|-----|---------|-----------|-----|-----|
| 1       | Violet    |     |     | 5       | Blue      |     |     |
| 2       | White     |     |     | 6       | Red       |     |     |
| 3       | Yellow    |     |     | 7       | Black     |     |     |
| 4       | Green     |     |     | 8       | Brown     |     |     |

Table 3.1: Cable Colors: 8-pole DIN-cable

The socket is wired as follows (Viewed from the rear of the PTC-IIpro).

1.  Audio output from the PTC to the transmitter.

2.  Ground.

3.  PTT output. (to transmitter PTT line)

4.  Audio input from the receiver to the PTC. (loudspeaker or
    appropriate AUC/ACC socket)

5.  Optional power supply input.

6.  A1.

7.  FSK output from the PTC to the transmitter.

8.  A0.

<img src=".//media/image4.wmf" style="width:1.79167in;height:1.81944in" />

Figure 3.3: Connection to the transceiver.

**NOTE:** Unfortunately, there are 8-pole plugs with different pin
numbering for the PINs 7 and 8. The PTC-IIpro needs an 8-pole plug with
U-shaped contact footprint. Plugs with circular contact footprint don’t
fit or can only be connected to the PTC-IIpro with damaging force! One
should not blindly rely on the printed numbers on the plug. The
connections as shown here in the handbook should be used as a reference.

The 8-pole DIN socket is mechanically designed that a 5-pole DIN plug
(180<sup>0</sup>) may be plugged into it too. An existing cable for the
Z80-PTC can be used without changes, the pin-out is the same of the
Z80-PTC set for AFSK.

It is possible to use a 5-pole DIN plug if an 8 pin is not available, or
the extra functions are not required. If a 5 pin DIN plug is used, then
the connections are as shown:

1.  Audio output from the PTC to the transmitter.

2.  Ground.

3.  PTT output. (to transmitter PTT line)

4.  Audio input from the receiver to the PTC. (loudspeaker or
    appropriate AUX socket)

5.  Optional power supply input.

<img src=".//media/image5.wmf" style="width:1.79167in;height:1.81944in" />

Figure 3.4: Connections to the transceiver (5 PIN DIN).

### Connection to ICOM transceivers:

Most ICOM transceivers that use 8 pin DIN plug (ACC) can be connected
this way:

| **Signal**                                                                             | **PTC** |     | **Color** | **ICOM 8 pin** |
|----------------------------------------------------------------------------------------|---------|-----|-----------|----------------|
| GND                                                                                    | PIN 2   |     | white     | PIN 2          |
| PTT                                                                                    | PIN 3   |     | yellow    | PIN 3          |
| AF-OUT                                                                                 | PIN 1   |     | violet    | PIN 4          |
| AF-IN                                                                                  | PIN 4   |     | green     | PIN 5          |
| POWER                                                                                  | PIN 5   |     | blue      | PIN 7          |
| **This cable is available completely assembled. Refer to Appendix A on page** **243.** |         |     |           |                |

Table 3.2: ICOM 8 pin connection

The *smaller* ICOM transceivers (e.g. IC-706) often use a 13 pin DIN
plug for ACC:

| **Signal**                                                                             | **PTC** |     | **Color** | **ICOM 13 pin** |
|----------------------------------------------------------------------------------------|---------|-----|-----------|-----------------|
| GND                                                                                    | PIN 2   |     | white     | PIN 2           |
| PTT                                                                                    | PIN 3   |     | yellow    | PIN 3           |
| AF-OUT                                                                                 | PIN 1   |     | violet    | PIN 11          |
| AF-IN                                                                                  | PIN 4   |     | green     | PIN 12          |
| POWER                                                                                  | PIN 5   |     | blue      | PIN 8           |
| **This cable is available completely assembled. Refer to Appendix A on page** **243.** |         |     |           |                 |

Table 3.3: ICOM 13 pin connection

### Connection to Kenwood transceivers:

Most Kenwood transceivers that use 13 pin DIN plug (ACC2) can be
connected this way:

<table style="width:76%;">
<colgroup>
<col style="width: 23%" />
<col style="width: 0%" />
<col style="width: 12%" />
<col style="width: 18%" />
<col style="width: 21%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Signal</strong></th>
<th colspan="2"><strong>PTC</strong></th>
<th><strong>Color</strong></th>
<th><strong>Kenwood</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GND</td>
<td colspan="2">PIN 2</td>
<td>white</td>
<td>PIN 4, 8, 12</td>
</tr>
<tr class="even">
<td>PTT</td>
<td colspan="2">PIN 3</td>
<td>yellow</td>
<td>PIN 9</td>
</tr>
<tr class="odd">
<td>AF-OUT</td>
<td colspan="2">PIN 1</td>
<td>violet</td>
<td>PIN 11</td>
</tr>
<tr class="even">
<td>AF-IN</td>
<td colspan="2">PIN 4</td>
<td>green</td>
<td>PIN 3</td>
</tr>
<tr class="odd">
<td colspan="4"><strong>This cable is available completely assembled.<br />
Refer to Appendix A on page</strong> <strong>243.</strong></td>
<td></td>
</tr>
</tbody>
</table>

Table 3.4: Kenwood 13 pin connection

The TS-50 can only be connected via the microphone jack:

| **Signal** | **PTC** | **Color** | **Kenwood** |
|------------|---------|-----------|-------------|
| GND        | PIN 2   | white     | PIN 7, 8    |
| PTT        | PIN 3   | yellow    | PIN 2       |
| AF-OUT     | PIN 1   | violet    | PIN 1       |
| AF-IN      | PIN 4   | green     | PIN 6       |

Table 3.5: Kenwood TS-50 connection

The TS-480 has a 6 pin Mini-DIN connector:

<table style="width:75%;">
<colgroup>
<col style="width: 24%" />
<col style="width: 12%" />
<col style="width: 17%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Signal</strong></th>
<th><strong>PTC</strong></th>
<th><strong>Color</strong></th>
<th><strong>YAESU</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GND</td>
<td>PIN 2</td>
<td>white</td>
<td>PIN 2</td>
</tr>
<tr class="even">
<td>PTT</td>
<td>PIN 3</td>
<td>yellow</td>
<td>PIN 3</td>
</tr>
<tr class="odd">
<td>AF-OUT</td>
<td>PIN 1</td>
<td>violet</td>
<td>PIN 1</td>
</tr>
<tr class="even">
<td>AF-IN</td>
<td>PIN 4</td>
<td>green</td>
<td>PIN 5</td>
</tr>
<tr class="odd">
<td colspan="4"><strong>This cable is available completely assembled.<br />
Refer to Appendix A on page</strong> <strong>243.</strong></td>
</tr>
</tbody>
</table>

Table 3.6: KENWOOD 6 pin Mini-DIN

### Connection to Yaesu transceivers:

Some YAESU transceivers use a 5 pin DIN plug (Packet) and can be
connected this way:

| **Signal** | **PTC** | **Color** | **YEASU** |
|------------|---------|-----------|-----------|
| GND        | PIN 2   | white     | PIN 2     |
| PTT        | PIN 3   | yellow    | PIN 3     |
| AF-OUT     | PIN 1   | violet    | PIN 1     |
| AF-IN      | PIN 4   | green     | PIN 4     |

Table 3.7: Yaesu connection

Smaller YAESU’s use a 6 pin Mini-DIN connector, whereby with multiband
transceivers two different connection schemes must be destinguished:

\- For HF and 1k2 Packet-Radio:

<table style="width:76%;">
<colgroup>
<col style="width: 24%" />
<col style="width: 12%" />
<col style="width: 17%" />
<col style="width: 21%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Signal</strong></th>
<th><strong>PTC</strong></th>
<th><strong>Color</strong></th>
<th><strong>YAESU</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GND</td>
<td>PIN 2</td>
<td>white</td>
<td>PIN 2</td>
</tr>
<tr class="even">
<td>PTT</td>
<td>PIN 3</td>
<td>yellow</td>
<td>PIN 3</td>
</tr>
<tr class="odd">
<td>AF-OUT</td>
<td>PIN 1</td>
<td>violet</td>
<td>PIN 1</td>
</tr>
<tr class="even">
<td>AF-IN</td>
<td>PIN 4</td>
<td>green</td>
<td>PIN 5</td>
</tr>
<tr class="odd">
<td colspan="4"><strong>This cable is available completely assembled.<br />
Refer to Appendix A on page</strong> <strong>243.</strong></td>
</tr>
</tbody>
</table>

Table 3.8: YAESU 6 pin Mini-DIN

\- For 9k6 Packet-Radio:

<table style="width:76%;">
<colgroup>
<col style="width: 23%" />
<col style="width: 0%" />
<col style="width: 12%" />
<col style="width: 18%" />
<col style="width: 21%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Signal</strong></th>
<th colspan="2"><strong>PTC</strong></th>
<th><strong>Color</strong></th>
<th><strong>YAESU</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GND</td>
<td colspan="2">PIN 2</td>
<td>white</td>
<td>PIN 2</td>
</tr>
<tr class="even">
<td>PTT</td>
<td colspan="2">PIN 3</td>
<td>yellow</td>
<td>PIN 3</td>
</tr>
<tr class="odd">
<td>AF-OUT</td>
<td colspan="2">PIN 1</td>
<td>violet</td>
<td>PIN 1</td>
</tr>
<tr class="even">
<td>AF-IN</td>
<td colspan="2">PIN 4</td>
<td>green</td>
<td>PIN 4</td>
</tr>
<tr class="odd">
<td colspan="4"><strong>This cable is available completely assembled.<br />
Refer to Appendix A on page</strong> <strong>243.</strong></td>
<td></td>
</tr>
</tbody>
</table>

Table 3.9: YAESU 6 pin Mini-DIN

### Amplitude Adjustment

The PTC-IIpro output amplitude has to be adjusted very carefully to the
connected transceiver. If you don’t pay attention on this item a signal
much too wide will be the result!.

The output amplitude are adjusted separately depending on the modes FSK
(PACTOR-I, AMTOR, RTTY, etc). and the modes PSK (PACTOR-II). A common
adjustment with one command was in practice not the best way.

The audio input sensitivity of most transceivers is adapted to the
output voltage of a common dynamic microphone. 100 % modulation is
reached at low MIC-Gain settings with 200 mV (Peak to peak) input
voltage. It is not recommended to use very high **PSKAmpl** values and
compensate this by lowering the MIC-Gain setting, because this may
already overdrive the first amplifier stages which are very sensitive
and located in the signal path before the MIC-Gain controlling device.
We recommend for the first approach to use the default PSKA value of 140
and then regulate the output power for PSK with the mic-gain setting (if
available). To do this connect the TRX to a dummyload resistor capable
to dissipate the power or to an antenna with good SWR (Take care that
the frequency being used is not already occupied). Entering **U** 3
\<Return> starts the Unproto mode 3 (=100 Bd DBPSK). Now you can use the
MIC-Gain knob to increase the transmitting power until the ALC voltage
reaches the allowed limit.

|     |                                                                                              |
|-----|----------------------------------------------------------------------------------------------|
|     | Don’t overdrive the TRX because in this case the signal will be spreaded by intermodulation! |

With proper settings the peak envelope power will nearly be equal to the
maximum output power of the TRX. In this case the average power will
approximately be the half of the maximum power, so also continuous
operation will not cause problems at all. Don’t be confused as many
modern TRX only display the peak envelope power. If it is necessary to
set the MIC-Gain value to more than half of ist maximum, it is
recommended to increase the **PSKAmpl** value. This for example can be
done entering \<ESC> **FSKA** 200 \<RETURN> If no MIC-Gain potentiometer
is available the proper PSK amplitude setting has to be evaluated with
only using the **PSKAmpl** command.

|     |                                                                                                                                                                                                               |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | After the PSK amplitude is carefully adjusted, the MIC-Gain setting at the transceiver should not be touched any more, otherwise it could be difficult to achieve the desired output level for non-PSK modes. |

To adjust the output level for non-PSK modes (FSK, CW, PACTOR-I, AMTOR,
RTTY) only the **FSKAmpl** command should be used now. Entering **U** 1
\<RETURN> starts the Unproto mode 1 (=100Bd FSK). Now you have the
chance to adjust the output value using the **FSKAmpl** command e.g.
\<ESC> **FSKA** 100 \<RETURN>. Same as before, during this procedure
take care for not to exceed the ALC limit.

To prevent damage from the transceiver at continuous operation we
recommend to limit the FSK output level to half of the maximum possible,
that means 50 W if the transceiver is made for 100 W at max.

#### PACTOR-III

For optimum PACTOR-III data throughput, the transmit signal must be
clean and undistorted. Make sure that ground loops and RF feedback
effects are avoided in your installation. A 1:4 voltage divider placed
directly at the transmit audio input of the transmitter may help to
improve the effective transmit SNR. Then you have to set FSKA and PSKA
to appropriate higher signal levels. PSKA levels lower than 80 are
generally not recommended. If possible, minimize the wiring between the
PTC and other devices: If the transceiver provides a power supply output
(e.g. 13.8 V), do not use an extra power supply for the PTC but connect
the PTC to the DC output of the transceiver. Use additional RF chokes
wherever applicable.

|     |                                                                                                            |
|-----|------------------------------------------------------------------------------------------------------------|
|     | Do not overdrive the transmitter (under no circumstances): The ALC level must not exceed the proper range! |

Some “noise blankers” as well as other “noise reduction tools” tend to
distort the PACTOR-III receive signal. In case of receiving problems try
out if switching off the “noise blanker” etc. improves the throughput.

Make sure that the PACTOR-III receive signal is centered properly within
the IF filter passband (see “tone monitor”). Adjusting the “passband
tuning / IF shift” improves the throughput in some cases.

## Transceiver Remote Control

The **SCS** PTC-IIpro is equipped with a connector for controlling all
the usual modern amateur radio transceivers. Virtually all newer
transceivers from KENWOOD, ICOM, YAESU, SGC and R&S allow remote
controlling of various functions, via a serial interface. Depending on
type and manufacturer, almost all the transceiver parameters can be
called up and changed. For example frequency, filter, operating mode,
and much more, can be controlled. With radio equipment that is digitally
controlled, the list of functions is almost unlimited.

The PTC-IIpro uses this features mainly to set and readout the frequency
of the transceiver. You find more about the transceiver remote control
in chapter 13 on page 201.

1.  RxD TTL.

2.  RTS V24.

3.  TXD V24.

4.  CTS V24.

5.  CTS TTL.

6.  ICOM.

7.  Not connected.

8.  RxD V24.

9.  TxD TTL.

10. RTS TTL.

11. AF out.

12. AF GND.

13. GND.

The 13 PIN DIN Remote-control socket is connected as follows. **(Viewed
from the back of the PTC-IIpro)**:

<img src=".//media/image6.wmf" style="width:1.59722in;height:1.59722in" alt="13pol-DIN-1" />

Figure 3.5: Transceiver remote-control

<table>
<colgroup>
<col style="width: 17%" />
<col style="width: 82%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong><br />
<br />
TxD TTL</strong></td>
<td>Transmit data from the PTC to the transceiver. TTL-level!</td>
</tr>
<tr class="even">
<td><strong>RxD TTL</strong></td>
<td>Receive data from the transceiver to the PTC. TTL-level!</td>
</tr>
<tr class="odd">
<td><strong>CTS TTL</strong></td>
<td>Handshake signal from the transceiver to the PTC. TTL-level!</td>
</tr>
<tr class="even">
<td><strong>RTS TTL</strong></td>
<td>Handshake signal from the PTC to the transceiver. TTL-level!</td>
</tr>
<tr class="odd">
<td><strong>TxD V24</strong></td>
<td>Transmit data from the PTC to the transceiver. V24-level!</td>
</tr>
<tr class="even">
<td><strong>RxD V24</strong></td>
<td>Receive data from the transceiver to the PTC. V24-level!</td>
</tr>
<tr class="odd">
<td><strong>CTS V24</strong></td>
<td>Handshake signal from the transceiver to the PTC. V24-level!</td>
</tr>
<tr class="even">
<td><strong>RTS V24</strong></td>
<td>Handshake signal from the PTC to the transceiver. V24-level!</td>
</tr>
<tr class="odd">
<td><strong>ICOM</strong></td>
<td>Special bi-directional data signal for controlling ICOM equipment.</td>
</tr>
<tr class="even">
<td><strong>GND</strong></td>
<td>Ground.</td>
</tr>
<tr class="odd">
<td><strong>NF out</strong></td>
<td>Audio output signal that can directly be connected to a speaker. This output is only activated together with the PTC-IIpro´s Audio-functions!</td>
</tr>
<tr class="even">
<td><strong>NF GND</strong></td>
<td>RETURN for the speaker signal <strong>NF out</strong></td>
</tr>
</tbody>
</table>

To connect the PTC-IIpro to your transceiver use the attached 13-pole
DIN-cable.

| **PIN** | **Color** |     |     | **PIN** | **Color**   |     |     |
|---------|-----------|-----|-----|---------|-------------|-----|-----|
| 1       | violet    |     |     | 8       | red         |     |     |
| 2       | white     |     |     | 9       | pink        |     |     |
| 3       | yellow    |     |     | 10      | light blue  |     |     |
| 4       | green     |     |     | 11      | black/white |     |     |
| 5       | blue      |     |     | 12      | grey        |     |     |
| 6       | black     |     |     | 13      | orange      |     |     |
| 7       | brown     |     |     |         |             |     |     |

Table 3.10: Cable Colors: 13-pole DIN-cable

|     |                                                                                                                                                                             |
|-----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | All unused wires of the TRX control cable **must not** be twisted or soldered together. All unused wires have to be **insulated seperately** avoiding to touch each others. |

### Connections PTC - KENWOOD

Many KENWOOD radios use a 6 pin DIN socket for remote control. With some
equipment types however, the serial interface has to be modified. Please
read the equipment handbook or consult your dealer.

| **Signal** | **PTC** | **Color**  | **KENWOOD** |
|------------|---------|------------|-------------|
| TxD        | PIN 9   | pink       | PIN 3       |
| RxD        | PIN 1   | violet     | PIN 2       |
| CTS        | PIN 5   | blue       | PIN 5       |
| RTS        | PIN 10  | light blue | PIN 4       |
| GND        | PIN 13  | orange     | PIN 1       |

Table 3.11: KENWOOD TTL

Newer Kenwood transceiver (since TS-570) have a 9-pole-sub-D connector
and operate with V24 levels for transceiver control. It´s indended for
direct connection to a COM port of a PC. Also these transceivers can
easily be controlled by the PTC-IIpro. Just solder a 9-pole connector to
the attached cable as shown in the following table below.

| **Signal**                                                                             | **PTC** |     | **Color** | **KENWOOD** |
|----------------------------------------------------------------------------------------|---------|-----|-----------|-------------|
| TxD                                                                                    | PIN 3   |     | yellow    | PIN 3       |
| RxD                                                                                    | PIN 8   |     | red       | PIN 2       |
| CTS                                                                                    | PIN 4   |     | green     | PIN 8       |
| RTS                                                                                    | PIN 2   |     | white     | PIN 7       |
| GND                                                                                    | PIN 13  |     | orange    | PIN 5       |
| **This cable is available completely assembled. Refer to Appendix A on page** **231.** |         |     |           |             |

Table 3.12: KENWOOD V24

Also have a look to the accessory-list for a completely assembled cable.

###  Connections PTC - ICOM

Nearly all ICOM equipment has a 3.5 mm jack socket for remote control.
Bi-directional communication is carried out over a single cable, in
order that data can be both sent and received. Various equipment carries
different addresses, so it is possible for more than one piece of
equipment to be connected to the remote control cable. Further
information can be found in the appropriate literature from ICOM.

| **Signal**                                                                             | **PTC** | **Color** | **ICOM** |
|----------------------------------------------------------------------------------------|---------|-----------|----------|
| ICOM                                                                                   | PIN 6   | black     | inner    |
| GND                                                                                    | PIN 13  | orange    | outer    |
| **This cable is available completely assembled. Refer to Appendix A on page** **231.** |         |           |          |

> Table 3.13: ICOM Figure 3.6: ICOM plug

### Connections PTC - YAESU

Many new YAESU radios, like the FT890 or FT990, contain a 6 PIN Mini-DIN
socket for remote control. Please read the equipment handbook or consult
your dealer.

| **Signal** | **PTC** | **Color** | **YAESU** |
|------------|---------|-----------|-----------|
| TxD        | PIN 9   | pink      | PIN 3     |
| RxD        | PIN 1   | violet    | PIN 2     |
| GND        | PIN 13  | orange    | PIN 1     |

Table 3.14: YAESU FT 890/990

The FT980 is equipped with a normal 6-pole DIN socket for remote control
use. The pin connections are according to Table 3.14.

Due to an error in the PTC-IIpro main processor, it is unfortunately not
possible to directly read out the frequency of YAESU transceivers. The
following circuit however allows this error to be corrected and the
readout to be done.

Older transceivers like the FT757 supports serial input only. In this
case the PTC-IIpro adjusts the frequency but could not read-out it.

| **Signal** | **PTC** | **Color** | **YAESU** |
|------------|---------|-----------|-----------|
| TxD        | PIN 9   | pink      | PIN 3     |
| GND        | PIN 13  | orange    | PIN 1     |

Table 3.15: YAESU FT 757

Newer Yaesu transceiver (e.g. FT-920, FT847, FT-1000MP) have a
9-pole-sub-D connector and operate with V24 levels for transceiver
control. It´s indended for direct connection to a COM port of a PC. Also
these transceivers can easily be controlled by the PTC-IIpro. Just
solder a 9-pole connector to the attached cable as shown in the
following table below.

| **Signal**                                                                             | **PTC** |     | **Color** | **YAESU** |
|----------------------------------------------------------------------------------------|---------|-----|-----------|-----------|
| TxD                                                                                    | PIN 3   |     | yellow    | PIN 3     |
| RxD                                                                                    | PIN 8   |     | red       | PIN 2     |
| GND                                                                                    | PIN 13  |     | orange    | PIN 5     |
| **This cable is available completely assembled. Refer to Appendix A on page** **231.** |         |     |           |           |

Table 3.16: YAESU V24

Portable transceivers like the FT-100, FT-817 or FT-897 use a 8 pin
Mini-DIN connection:

| **Signal**                                                                             | **PTC** |     | **Color** | **YAESU** |
|----------------------------------------------------------------------------------------|---------|-----|-----------|-----------|
| TxD                                                                                    | PIN 1   |     | violet    | PIN 4     |
| RxD                                                                                    | PIN 9   |     | pink      | PIN 5     |
| GND                                                                                    | PIN 13  |     | orange    | PIN 3     |
| **This cable is available completely assembled. Refer to Appendix A on page** **231.** |         |     |           |           |

|     |                                                                                                                  |
|-----|------------------------------------------------------------------------------------------------------------------|
|     | Don’t forget to set thje exact transceiver-type using the **YType** command! Refer to chapter 13.22 on page 212. |

## The Packet-Radio Modules

The optional DSP Packet-Radio-Module-II expands the PTC-IIpro to a
universal multiport controller. It provides the following modes:

-   600 Baud Robust HF-Packet

-   300 baud AFSK (modem tones are fixed to 2300/2100 Hz, *High-Tones*)

-   1200 baud AFSK

-   9600 baud FSK (direct-FSK, compatible to G3RUH standard)

-   19200 baud FSK (direct-FSK, compatible to G3RUH standard)

    The well known AFSK- and FSK-modules and the DSP-module are out of
    production and are mentioned here for completeness only.

-   **AFSK module:** for 1200 and 2400 baud AFSK with a standard modem
    chip TCM3105 and a fully digital carrier detection.

-   **FSK module:** for the G3RUH compatible FSK method (9600 Baud etc).

-   **DSP module:** for 300, 1200 baud AFSK and 9600, 19200 baud FSK
    (G3RUH standard).

The modules contain all necessary electronics for signal processing. The
actual packet protocol processing is done within the PTC-IIpro.

|     |                                                                                        |
|-----|----------------------------------------------------------------------------------------|
|     | Don’t forget to adjust the output amplitude of the Packet modules to your transceiver! |

### Installation

The modules must be installed very carefully. Please check that all pins
on the PTC-IIpro are correctly plugged to the corresponding socket of
the modem. Checking three times is better than switching on the
PTC-IIpro with an incorrectly plugged in modem !!

Figure 3.9 shows the position of both packet-radio modules. It does not
matter which socket is used for which modem module. The PTC-IIpro
automatically checks after power-on if a module is installed and which
it is. The module(s) found are announced in the power-on message, or may
be viewed using the Version command.

### The DSP-Module-II

<img src=".//media/image7.png" style="width:5.23611in;height:1.66667in" />

Figure 3.7: The DSP-Module-II.

|     |                                                                   |
|-----|-------------------------------------------------------------------|
|     | To use the DSP-Module-II you need firmware version 3.6 or higher! |

The **SCS** DSP-Module-II is an universal module for 300, 1200, baud
AFSK, 9600 and 19200 baud FSK (G3RUH compatible), as well as for 600
baud robust HF Packet. The use of a signal-processor ensures optimized
filtering and demodulation for the supported modes. With this the best
possible performance in Packet-Radio can be achieved.

The PTC-IIpro automaticly recognizes the DSP-PR-module directly after
power-on and loads the DSP software into the module. Recognition and
successful initialization of the module is signalised by a short blink
of the connected-LED of the corresponding port.

As the software of the DSP-PR-module is a part of the PTC-IIpro firmware
it can be improved and expanded via firmware updates. The enormous
flexibility of the PTC-IIpro concept also includes the packet radio
side.

The choice or setting of the correct modulation for the actual baudrate
is automatically made by the PTC-IIpro. The DSP PR modem is capable of
full duplex and mixed baudrate in all modes.

The DSP concept for PR also allows the software setting and adjustment
of all modem parameters. The output-level is set with the command
**TXLevel** (see chapter 9.7.39 on page 167) in the range of 20mVpp to
3Vpp. The adjustment of a potentiometer is not necessary.

The PTT-transistor is a powerful VMOS-FET which can reliably switch 16V
at 1A to ground.

The input-sensitivity of the module can be choosen by the jumper J1. The
initial condition of the jumper is closed. It can be found on the
component location plan as a 0 Ω resistor on the left side of the PTT
transistor Q1.

For 9k6 operation your transceiver requires a special connection. The
modulation voltage is fed direct to the modulator, and the received
signal is taken directly from the demodulator. Newer equipment sometimes
offers a so called data connector. These *“hybrid”* radios are suitable
for 9k6 operation without modifications. As the data connectors of all
manufacturers have the same pin connections, **SCS** offers a special
cable for use with these transceivers. Transceivers without a data
connector require modification for direct access to the modulator and
demodulator. Information concerning modifications can be found in
practically all Packet-Radio mailboxes.

Here are the technical details:

<table>
<colgroup>
<col style="width: 29%" />
<col style="width: 70%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Modulation</td>
<td><p>AFSK (Audio-Frequency-Shift-Keying) or</p>
<p>FSK (Frequency-Shift-Keying)</p></td>
</tr>
<tr class="even">
<td>AF output voltage</td>
<td><p>20 mVpp to 3Vpp adjustable.</p>
<p>The output is muted while on receive.</p></td>
</tr>
<tr class="odd">
<td>Output impedance</td>
<td>approx. 1 kΩ</td>
</tr>
<tr class="even">
<td>AF input</td>
<td><p>100 mVpp to 1.6 Vpp (J1 open)</p>
<p>100 mVpp to 8Vpp (J1 closed)</p></td>
</tr>
<tr class="odd">
<td>Input impedance</td>
<td>approx. 47 kΩ</td>
</tr>
<tr class="even">
<td>PTT</td>
<td>max. 16 V, 1 A to GND</td>
</tr>
</tbody>
</table>

Table 3.17: Technical Details of the DSP-Module

### The DSP-Module

**This module is out of production ans is replaced by the
DSP-Module-II.**

The **SCS** DSP-module is an universal module for 300, 1200, baud AFSK,
9600 and 19200 baud FSK (G3RUH compatible). The use of a
signal-processor ensures optimized filtering and demodulation for the
supported modes. With this the best possible performance in Packet-Radio
can be achieved.

The PTC-IIpro automaticly recognizes the DSP-PR-module directly after
power-on and loads the DSP software into the module. Recognition and
successful initialization of the module is signalised by a short blink
of the connected-LED of the corresponding port.

As the software of the DSP-PR-module is a part of the PTC-IIpro firmware
it can be improved and expanded via firmware updates. The enormous
flexibility of the PTC-IIpro concept also includes the packet radio
side.

The choice or setting of the correct modulation for the actual baudrate
is automatically made by the PTC-IIpro. The DSP PR modem is capable of
full duplex and mixed baudrate in all modes.

The DSP concept for PR also allows the software setting and adjustment
of all modem parameters. The output-level is set with the command
**TXLevel** (see chapter 9.7.39 on page 167) in the range of 20mVpp to
3Vpp. The adjustment of a potentiometer is not necessary.

The PTT-transistor is a powerful VMOS-FET which can reliably switch 16V
at 1A to ground.

The input-sensitivity of the module can be choosen by the jumper J1. The
initial condition of the jumper is closed. It can be found on the
component location plan as a 0 Ω resistor on the left side of the PTT
transistor Q1.

For 9k6 operation your transceiver requires a special connection. The
modulation voltage is fed direct to the modulator, and the received
signal is taken directly from the demodulator. Newer equipment sometimes
offers a so called data connector. These *“hybrid”* radios are suitable
for 9k6 operation without modifications. As the data connectors of all
manufacturers have the same pin connections, **SCS** offers a special
cable for use with these transceivers. Transceivers without a data
connector require modification for direct access to the modulator and
demodulator. Information concerning modifications can be found in
practically all Packet-Radio mailboxes.

Here are the technical details:

<table>
<colgroup>
<col style="width: 29%" />
<col style="width: 70%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Modulation</td>
<td><p>AFSK (Audio-Frequency-Shift-Keying) or</p>
<p>FSK (Frequency-Shift-Keying)</p></td>
</tr>
<tr class="even">
<td>AF output voltage</td>
<td><p>20 mVpp to 3Vpp adjustable.</p>
<p>The output is muted while on receive.</p></td>
</tr>
<tr class="odd">
<td>Output impedance</td>
<td>approx. 1 kΩ</td>
</tr>
<tr class="even">
<td>AF input</td>
<td><p>100 mVpp to 1.6 Vpp (J1 open)</p>
<p>100 mVpp to 8Vpp (J1 closed)</p></td>
</tr>
<tr class="odd">
<td>Input impedance</td>
<td>approx. 47 kΩ</td>
</tr>
<tr class="even">
<td>PTT</td>
<td>max. 16 V, 1 A to GND</td>
</tr>
</tbody>
</table>

Table 3.18: Technical Details of the DSP-Module

<img src=".//media/image8.wmf" style="width:5.93056in;height:1.75in" />

Figure 3.8: The DSP-Module.

<img src=".//media/image9.wmf" style="width:6.02778in;height:5.05556in" />
Figure 3.9: Positioning of the Packet-Radio modules.

The PTC-IIpro automaticly recognizes the DSP-PR-module directly after
power-on and loads the DSP software into the module. Recognition and
successful initialization of the module is signalised by a short blink
of the connected-LED of the corresponding port.

As the software of the DSP-PR-module is a part of the PTC-IIpro firmware
it can be improved and expanded via firmware updates. The enormous
flexibility of the PTC-IIpro concept also includes the packet radio
side.

The choice or setting of the correct modulation for the actual baudrate
is automatically made by the PTC-IIpro. The DSP PR modem is capable of
full duplex and mixed baudrate in all modes.

The DSP concept for PR also allows the software setting and adjustment
of all modem parameters. The output-level is set with the command
**TXLevel** (see chapter 9.7.39 on page 167) in the range of 20mVpp to
3Vpp. The adjustment of a potentiometer is not necessary.

The PTT-transistor is a powerful VMOS-FET which can reliably switch 16V
at 1A to ground.

The input-sensitivity of the module can be choosen by the jumper J1. The
initial condition of the jumper is closed. It can be found on the
component location plan as a 0 Ω resistor on the left side of the PTT
transistor Q1.

For 9k6 operation your transceiver requires a special connection. The
modulation voltage is fed direct to the modulator, and the received
signal is taken directly from the demodulator. Newer equipment sometimes
offers a so called data connector. These *“hybrid”* radios are suitable
for 9k6 operation without modifications. As the data connectors of all
manufacturers have the same pin connections, **SCS** offers a special
cable for use with these transceivers. Transceivers without a data
connector require modification for direct access to the modulator and
demodulator. Information concerning modifications can be found in
practically all Packet-Radio mailboxes.

Here are the technical details:

<table>
<colgroup>
<col style="width: 29%" />
<col style="width: 70%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Modulation</td>
<td><p>AFSK (Audio-Frequency-Shift-Keying) or</p>
<p>FSK (Frequency-Shift-Keying)</p></td>
</tr>
<tr class="even">
<td>AF output voltage</td>
<td><p>20 mVpp to 3Vpp adjustable.</p>
<p>The output is muted while on receive.</p></td>
</tr>
<tr class="odd">
<td>Output impedance</td>
<td>approx. 1 kΩ</td>
</tr>
<tr class="even">
<td>AF input</td>
<td><p>100 mVpp to 1.6 Vpp (J1 open)</p>
<p>100 mVpp to 8Vpp (J1 closed)</p></td>
</tr>
<tr class="odd">
<td>Input impedance</td>
<td>approx. 47 kΩ</td>
</tr>
<tr class="even">
<td>PTT</td>
<td>max. 16 V, 1 A to GND</td>
</tr>
</tbody>
</table>

Table 3.19: Technical Details of the DSP-Module

### The AFSK Module

**This module is out of production ans is replaced by the
DSP-Module-II.**

The **SCS** AFSK-Module for Packet-Radio uses the standard baudrate 1200
and 2400 baud. The module uses the well known modem chip TCM3105, and is
because of this fully compatible to the usual standards.

<img src=".//media/image10.wmf" style="width:5.93056in;height:2in" />

Figure 3.10: The 1k2/2k4 AFSK-Module.

The carrier detection is fully digital. This has the the advantage over
the usual tone decoder ciruitry in that (for example) a 1750 call tone
is not detected as a signal. The module only reacts to Packet-Radio
signals.

|     |                                                                                                                                                                                            |
|-----|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | To make the carrier detection safe and fast, the squelch of the connected TRX shall be opened, that means that all the time signal noise is available at the AF output of the transceiver. |

The module also contains a PTT watchdog that prevents a continuous
carrier from being transmitted. A powerful VMOS-FET is used as the PTT
switching transistor. This transistor can reliably switch even 16 Volts
and 1 Amp to ground.

The AF output voltage can be adjusted with the potentiometer P1. It
could be found on the circuit board, labeled as MIC GAIN as Figure 3.10
shows. NOTE: the potentiometer does not contain an end stop, and is able
to be turned through 360 degrees. The potentiometer is delivered set to
its middle setting. The output voltage can be adjusted between 20 mVpp
and 400 mVpp. By bridging over R7 it is possible to increase the output
voltage to a maximum of 2 Vpp.

On delivery the AF input is adjusted for connection to a low level
output (e.g. the demodulator output, a tapping point before the volume
control or a data socket). By closing the link BR5, it is possible to
lower the modules sensivity, and it may thus be directly connected to
the loudspeaker of a transceiver. The volume should however not be
turned up over normal *room* value.

Here are the technical details:

<table>
<colgroup>
<col style="width: 29%" />
<col style="width: 70%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Modulation</td>
<td>AFSK (Audio-Frequency-Shift-Keying)</td>
</tr>
<tr class="even">
<td>Tonepairs</td>
<td>1200/2200 Hz at 1200 Bit/s</td>
</tr>
<tr class="odd">
<td></td>
<td>2000/3666 Hz at 2400 Bit/s</td>
</tr>
<tr class="even">
<td>AF output voltage</td>
<td><p>Approx. 20 mVpp to 400 mVpp adjustable.</p>
<p>The output is muted while on receive.</p></td>
</tr>
<tr class="odd">
<td>Output impedance</td>
<td>Lower than 1 kΩ</td>
</tr>
<tr class="even">
<td>AF input</td>
<td>20 mVpp to 600 mVpp (BR5 open)</td>
</tr>
<tr class="odd">
<td></td>
<td>200 mVpp to 10 Vpp (BR5 closed)</td>
</tr>
<tr class="even">
<td>Input impedance</td>
<td>Approx. 22 kΩ</td>
</tr>
<tr class="odd">
<td>PTT</td>
<td>max. 16 V, 1 A to GND</td>
</tr>
</tbody>
</table>

Table 3.20: Technical details of the 1k2/2k4-Modul

### The 9k6-Module

**This module is out of production ans is replaced by the
DSP-Module-II.**

The **SCS** FSK-Module is fully G3RUH compatible. By using switched
capacitor filters, the module can be used over a wide baudrate range
without hardware changes. Although the module has been especially
developed for 9600 baud, it will work between 4800 and 38400 baud
through the use of the SC-filter.

<img src=".//media/image11.wmf" style="width:5.95833in;height:2in" />

Figure 3.11: The 9k6-Module.

The module also contains a PTT watchdog that prevents a continuous
carrier from being transmitted. A powerful VMOS-FET is used as the PTT
switching transistor. This transistor can reliably switch even 16 Volts
and 1A to ground.

The AF output voltage can be adjusted with the potentiometer P1,
labelled as MIC GAIN as Figure 3.11 shows. NOTE: the potentiometer does
not contain an end stop, and is able to be turned through 360 degrees.
The potentiometer is delivered set to its middle setting. The output
voltage can be adjusted between 20 mVpp and 3Vpp.

For 9k6 operation your transceiver requires a special connection. The
modulation voltage is fed direct to the modulator, and the received
signal is taken directly from the demodulator. Newer equipment sometimes
offers a so called data connector. These *“hybrid”* radios are suitable
for 9k6 operation without modifications. But take care also with there
radios. Due to the relatively high PLL stabilization time after TX/RX
change, the **TXDelay** value has to be set significantly higher than
with pure data-transceivers.

As the data connectors of all manufacturers have the same pin
connections, **SCS** offers a special cable for use with these
transceivers. Transceivers without a data connector require modification
for direct access to the modulator and demodulator. Information
concerning modifications can be found in practically all Packet-Radio
mailboxes.

Here are the technical details:

<table>
<colgroup>
<col style="width: 29%" />
<col style="width: 70%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Modulation</td>
<td>FSK (Frequency-Shift-Keying)</td>
</tr>
<tr class="even">
<td>AF output voltage</td>
<td><p>Approx. 20 mVpp to 3Vpp adjustable.</p>
<p>The output is muted while on receive.</p></td>
</tr>
<tr class="odd">
<td>Output impedance</td>
<td>Lower than 1 kΩ</td>
</tr>
<tr class="even">
<td>AF input</td>
<td>100 mVpp to 3 Vpp</td>
</tr>
<tr class="odd">
<td>Input impedance</td>
<td>approx. 47 kΩ</td>
</tr>
<tr class="even">
<td>PTT</td>
<td>max. 16 V, 1 A to GND</td>
</tr>
</tbody>
</table>

Table 3.21: Technical Details of the 9k6-Modul

### The Packet-Radio connectors

The Packet-Radio connector on the PTC-IIpro is understandably only
available when the appropriate modem is plugged in. The pin-out of the 5
PIN DIN socket follows usual TNC connections:

The 5 PIN DIN socket for Packet is connected as follows. (Viewed from
the back of the PTC):

1.  Audio output from the PTC to the transmitter.

2.  Ground (GND).

3.  PTT output.

4.  Audio input from receiver to the PTC. (loudspeaker or appropriate
    > AUX. connector).

5.  Reserve.

<img src=".//media/image12.wmf" style="width:1.79167in;height:1.77778in" />

Figure 3.12: Packet-Radio connector (5-PIN DIN)

| **PTC** | **Color** |
|---------|-----------|
| PIN 1   | Violet    |
| PIN 2   | White     |
| PIN 3   | Yellow    |
| PIN 4   | Green     |
| PIN 5   | Blue      |

Table 3.22: Cable Colors: 5-pole DIN-cable

**NOTE:** The 5 PIN DIN socket is only available for use when an
appropriate modem is inserted!

<img src=".//media/image13.wmf" style="width:6in;height:4.65278in" alt="pro-total" />

Figure 3.13: View of the PTC-IIpro
