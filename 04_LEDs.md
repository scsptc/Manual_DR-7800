Chapter 4

# LED's

<img src=".//media/image14.wmf" style="width:6.01389in;height:1.22222in" alt="ProFront" />

Figure 4.1: The PTC-IIpro front.

The **SCS** PTC-IIpro is equipped with 15 LED´s to display the most
essential status information, a fifteen LED tuning indicator and a ten
character alphanumeric LED display to show the operating mode. The
meaning of the LED´s is shown below.

**Idle/Request:**

When Idle lights, then it means that at least one filler character
(idle) is contained in the present packet. If Request lights, then the
other station has requested a repeat of the last sent data or control
packet.

**Traffic/Error:**

When Traffic is lit, then the system is transferring data, and the HF
channel is un-interrupted. During the STBY condition, (not in Listen
mode) then the Traffic LED shows when the channel is occupied (channel
busy). If Error lights, then it means the packet or control signal had
bit errors, and can therefore not be identified with certainty.

**Send/CHO:**

Send displays that the PTC is the actual packet sender. The CHO LED
displays that at the moment, a change over (change of transmit
direction) is being carried out. The CHO LED extinguishes when a change
over is acknowledged by the other station.

**Compress2/Compress1:**

Displays which compression method is at present being used. Compress 1
is Huffman coding, Compress 2 being pseudo Markow coding. If the LED
extinguishes, then the actual packet is an ASCII packet.

**Tracking/Phasing:**

Tracking lights for a short while when the PTC-IIpro changes the carrier
frequency during a PT-II link (see also **AQrg** command in chapter 6.5,
page 61). Phasing is active if a new phasing takes place in AMTOR (ARQ &
FEC).

**MARQ-OK/MARQ-IN:**

MARQ-OK lights if the actual packet has been correctly reconstructed
using memory ARQ. MARQ-IN shows that the present packet is being
reconstructed, and is not classed as a Request Packet.

**DQPSK/DBPSK:**

These are activated respectively (also during Unproto and Listen mode)
depending on if the packet is DQPSK or DBPSK.

**MaxSpeed/HiSpeed:**

MaxSpeed lights during 16-DPSK packets (also with Unproto and Listen
modes). HiSpeed lights during PT-I packets which are 200 baud (also with
Unproto and Listen), and when PT-II packets using 8-DPSK are being used.

**Connected/Mail:**

Connected lights permanently in the connected condition (AMTOR, PACTOR).
In the STBY condition, Mail lights if there is unread mail for one's own
address (MYcall callsign) in the PTC mailbox.

**Tune:**

Under optimum conditions, only the two outermost LED´s of the tuning
indicator light up. With PACTOR-II the frequency offset is additionally
displayed (center display LED) in red. In this case the middle of the
tuning indicator is corresponding to the own frequency and the red LED
in the middle represents the frequency of the distant station. If the
middle indicator drifts to the left, the frequency of the distant
station is too low. If the middle indicator drifts to the right, the
frequency of the distant station is too high.

**Matrix Display:**

The matrix display indicates the actual operating modes of the
PTC-IIpro. For detailed information refer to table 6.1. Only the display
of Packet-Radio connects needs more detailed information: The first
digit indicates the used Packet-Radio port. **X** for port 1 and **Y**
for port 2. The second and third digit indicate the channel the QSO ties
up. The fourth digit indicates with the sign ˆ (ASCII 94) a connection
to the Packet-Radio mailbox. A . (ASCII 46) at the fourth digit
indicates that there are unconfirmed packet at the PTC-IIpro.

At more than one connect the different channels are displayed in a 1.5 s
alternating sequence.

| **Message** | **Description**                                                 |
|-------------|-----------------------------------------------------------------|
| Ready       | The PTC-IIpro is in BIOS mode.                                  |
| loading     | The firmware is loaded from the Flash-ROM into the RAM.         |
| ---STBY---  | The PTC-IIpro is in standby mode.                               |
| CON>DL6MAA  | A connection to DL6MAA is build up.                             |
| C DL0HO     | Reception of connect frames for DL0HO.                          |
| MON PT1     | Monitoring of PACTOR.                                           |
| MON PT2     | Monitoring of PACTOR-II.                                        |
| PT1 DL1ZAM  | PACTOR connection to DL1ZAM.                                    |
| PT2 DL6MAA  | PACTOR-II connection to DL6MAA.                                 |
| X01 DB0ZDF  | Packet-Radio connection on port 1, channel 01 to DB0ZDF.        |
| Y02 DB0AIS  | Packet-Radio connection on port 2, channel 02 to DB0AIS.        |
| Y02ˆDK9FAT  | DK9FAT has connected the Packet-Radio mailbox of the PTC-IIpro. |
| Y02.BD0AIS  | There are still packets for DB0AIS unconfirmed.                 |

Table 4.1: Examples for the matrix display.

**PACKET**

**PTT:**

The PR modem is keying the transmitter to send data.

The PTT-LED of port 2 has a special function. It blinks when the
PTC-IIpro is in power-down condition initiated with the OFF command.

**Connected:**

The PTC-IIpro is linked to another station (Connected).

**Carrier:**

The modem has detected a valid Packet-Radio signal.

**PACTOR-III**

| **Speedlevel** | **DQPSK/DBPSK-LED** | **MaxSpeed/HiSpeed-LED** |
|----------------|---------------------|--------------------------|
| 1              | red                 | \-                       |
| 2              | green               | \-                       |
| 3              | \-                  | red                      |
| 4              | \-                  | green                    |
| 5              | red                 | green                    |
| 6              | green               | green                    |

Table 19: PACTOR-III Speedlevels

PTC-IIpro: The single LED in the tuning display shows the frequency
error and lits red when the error is greater than 10 Hz. It lits green
when the error is smaller than 10 Hz, which usually happens after the
automatic frequency tracking has been completed.

<table>
<colgroup>
<col style="width: 9%" />
<col style="width: 90%" />
</colgroup>
<tbody>
<tr class="odd">
<td></td>
<td><p>For unlimited usage of PACTOR-III and the other extended features of the firmware you need a license key. Without this license key you just have 20 connects to test the extended featurs. Refer to the <strong>LICENSE</strong> command in chapter <strong>6.47</strong> on page <strong>82</strong>.</p>
<p>For prices and a detailed manual for the extended firmware functions refer to the <strong>SCS</strong> homepage <a href="http://www.scs-ptc.com">http://www.scs-ptc.com</a> in the Internet.</p></td>
</tr>
</tbody>
</table>

<img src=".//media/image15.wmf" style="width:6.01389in;height:2.47222in" alt="pro-front" />

Figure 4.2: The PTC-IIpro front panel
