Chapter 8

# FAX

## General Information

In addition to the normal teletype modes the PTC-IIpro supports the
following modes; FM-FAX (Shortwave), AM-FAX (Satellites), SSTV (All
present standards) and NFSK-Demodulation for decoding various shortwave
teleprinting methods.

The algorithms used here, profit from the relatively high computing
power of the PTC-IIpro and allow the system to easily reach the
theoretical limits regarding definition, filter performance and
resistance to interference in all picture operating modes. Additionally,
particular for STTV, a new concept for recognizing and filtering the
synchronization impulses has been incorporated. With the use of DSP
techniques, the system delivers excellent linearity, both in the receive
and transmission paths. This means very good color rendering and
reproducibility. A possibility for manually setting the filter bandwidth
and maximum picture definition allow the user to adjust for actual
signal conditions.

Transmit operation is also supported for FM-FAX/FSK, AM-FAX and SSTV.
The FM/FSK modulator is phase-continuous and highly linear, producing an
extremely clean transmitted signal.

The FM/FSK demodulated signal is available as a 1 bit square wave at PIN
6 of the RS-232 interface in addition to the usual 8-bit serial
transfer. This allows full compatibility with the widely used radio
teleprinter programs such as Zorns Lemma.

The PTC-IIpro operates in all special MODEM functions as a FULL-DUPLEX
modem. This means the appropriate demodulator generates the correct data
even during the transmit phase. This is in most cases however, only of
interest for testing purposes.

## Basic info concerning FAX and SSTV

### AM-FAX

This FAX variant is found mainly in the typical VHF/UHF/SHF FM
frequencies, despite the fact that one tends to think of AM as a
shortwave mode. In practice, AM-FAX is an FM transmission, but is
concerned with the transmission of an amplitude modulated low frequency
carrier. The frequency of the carrier tone is normally 2400 Hz. The
instantaneous amplitude relates to the brightness information. When the
tone is at its maximum amplitude, then the receive program must paint a
white pixel. When the tone is very soft, then a black pixel must be
displayed. (NOTE: with FM, the loudness of the transmitted signal has no
relation to the strength of the received HF-signal).

The most interesting signal sources of AM-FAX are mainly the weather
satellites (NOAA-Satellites on 137 MHz or the geostationary Meteosat 5
or GOES (USA) on approx. 1.7 GHz.

To receive these satellites, it is recommended that a special receiver
is used with an IF bandwidth of approx. 30-50 kHz. For the 1.7 GHz band,
a small dish or Yagi-antenna with a low noise LNA or LNC will also be
required.

Meteosat 5 for example, transmits almost continuous IR and VIS pictures
with a resolution of 2.5 to 5 km in a format of 800 x 800 pixels. Many
programs are able to automatically sense the beginning of each picture
by using additional digital information, and to make very impressive
weather films. These films are interesting not only for amateur
meteorologists, but also for sailors, mountain climbers etc.

The pixel-rate from Meteosat 5 is 3360 pixels per second - 4 lines are
transmitted per second. The resulting bandwidth (relating to the
appropriate Nyquist filtering) is ± 1680 Hz or a total of 3360 Hz. The
PTC-IIpro allows the maximum possible resolution of the Meteosat signal
to be displayed.

### FM-FAX

Frequency modulated FAX is the established standard for weather maps and
press photographs on shortwave and longwave. This very old
*WEFAX-Standard* is however rapidly losing importance in the commercial
sector. One reason is that the quality of the FAX image is strongly
influenced by the effective signal to noise ratio and the propagation
conditions (e.g. multipath propagation). In amateur use however, FM-FAX
is a useful mode as it allows high definition in comparison to SSTV, for
transmission of highly detailed pictures on good to very good HF paths.

The center frequency for FM-FAX has established itself as 1900 Hz. On
longwave, a frequency shift of 150 Hz is usual. On shortwave it has
standardized at 400 Hz. This means that in a normal FAX signal on
shortwave, the brightness information *white* is transmitted by a tone
of 1900 + 400 Hz i.e. 2300 Hz, and "black" is represented by 1900... 400
Hz or 1500 Hz. A gray-scale is given by the appropriate frequencies
between the limits represented by 1500 and 2300 Hz.

The Nyquist bandwidth associated with FM-FAX is approximated by the
formula pixelrate + 2\*shift. With a pixelrate of 1600/sec, one
calculates a Nyquist bandwidth of 800+400+400+800 = 2400 Hz. The
PTC-IIpro allows a resolution of up to 2600 pixels/sec. The bandwidth of
such a signal is approximately 3400 Hz, so that a steep sided 2.4 kHz
SSB filter would be too narrow to allow the full resolution to be used.
It is only useful to increase the receiver bandwidth above 2.4 kHz when
it is known that the transmitted bandwidth is not limited to 2.4 kHz.
Here only trial and error will tell if the received picture resolution
is improved with a wider receiver IF bandwidth.

The majority of FM-FAX transmissions are carried out with a speed of 120
lines per minute, however 90 and 60 lines are also used by various
agencies for special purposes. The speed may be guessed, with a bit of
practice, from the sound of the signal from the station loudspeaker. If
one is not sure, then it can be found by counting (for example for half
a minute) the typical rhythmical beat of the FAX transmission.

The start and end of an FM-FAX transmission is usually signaled by a
long (several seconds) tone sequence. This method is called APT, which
means nothing more than Automatic Picture Transmission. FAX-Programs can
evaluate these APT tones automatically.

FM-FAX signals may be found all over the shortwave bands, and are easily
recognized by their typical rhythmical and somewhat *rough* tone. The
receiver should be set to USB for FM-FAX reception, so that the correct
relationship between brightness and frequency information is maintained.
(If the wrong sideband is chosen then the pictures are *inverted*, i.e.
black lines are drawn white and vice-versa).

### SSTV

With use of a computer creeping into virtually every shack, the SSTV
mode has changed from a technical challenge for a few specialists, to a
relatively wide-spread and amusing amateur radio pastime. Above all it
is also interesting for *epicures in private* to observe the large
number of STTV transmissions on 20 and 80 m. In the early days of SSTV,
it was only possible to transmit relatively low definition Black and
White pictures. The new generation of SSTV standards, under good
propagation conditions, offer an astoundingly good, high resolution,
true-color picture. In the last few years, two variants have established
themselves as de-facto standards. **MARTIN 1** in and around Europe, and
**SCOTTIE 1** in the US and US-influenced areas of the world. Both
standards are very similar, and differ only in small details.

In order to allow high definition and also color transmissions to be
made, the new standards have a transmission time of approximately 2
minutes per frame (as against only 8 seconds for the original
Black/White SSTV pictures).

One of the main problems of the old *steam SSTV* was the persistence of
the CRT on which the pictures were viewed. In this digital age, with
electronic storage, the problem is no longer there. The developer has
more or less a free choice, and is virtually only dictated by the wishes
of the user.

Unfortunately, this freedom in transmission times has led to an
unnecessary number of different SSTV sub-standards, some of which are
poorly documented. A real technical requirement for these multiplicity
of standards is not to be found. By limiting the SSTV practice to a few
modes, it is possible to keep a reasonable overview of the entire SSTV
scene.

Like in the early *steam SSTV* period, the modern systems still use FM
as the means for video transmission, very similarly to the FM-FAX
standard (refer to chapter 8.2.2, page 124). The center frequency is
usually 1900 Hz, with a shift of 400 Hz, so that as in FM-FAX, the
frequency limits are 1500 Hz and 2300 Hz representing the *black* and
*white* respectively.

The difference between FM-FAX and SSTV is that SSTV uses picture and
line synchronization in the form of a special tone frequency which is
*blacker* than *black*, that is 1200 Hz. A tone-burst with a frequency
of 1200 Hz and a duration of 30 ms signals the start of a picture frame.
At the start of every SSTV line, a tone of 1200 Hz with a duration of 5
ms is inserted as a horizontal synch pulse, so that the exact start of a
line can be marked. The exact and rapid processing of this horizontal
synch pulse is the key to satisfactory SSTV reception.

The resolution of MARTIN 1 and SCOTTIE 1 is approximately 300 pixels per
line. The color palette is obtained by mixing the colors red, blue and
green. Every line transmitted actually consists of three lines, each
containing the intensity components of the respective colors.
Effectively, each line contains three *sub lines*. When using this
transmission system, incorrect tuning does not lead to color errors. It
leads instead only to changes in color intensity.

SSTV signals are often found in the band segment 3730-3740 kHz, as well
as 14230 and 14240 kHz. After a short period of getting used to things,
the sound of SSTV, as in all other forms of picture transmission, is
rapidly recognized by its distinctive sound from the station
loudspeaker.

## FAX and SSTV with JVComm32

As with **WIN95** the real-time processing is not reliable enough,
**JVComm32** also had problems using the PTC SSTV/FAX transmission
routine at slower PCs. For transmission the PTC needs a continuous data
stream with a high baud rate (usually 57600 baud) from the PC´s serial
interface. No interrupt should occur, as gaps and shifts within the
transmitted picture would be tht result. But a continuous data stream
using **WIN95** is only possible with very fast PCs – and also this is
no guarantee – it depends on the computing capacity occupied by other
applications.

The second problem of the older implementation: The transmission timing
must be provided by the PC. But PCs only use inacurate and unadjusted
oscillators so a relatively complicated procedure for skew correction on
the transmission side was necessary.

Both problems are solved with the new modem command **JVComm** within
the **fax:**-menu, activating a new transmission routine. On the
receiving side the JVComm modem of the PTC-IIpro has the same behavior
as the previous FMfax modem (also activated within the **fax:**-menu).
The only difference is that the PTC provides no receiving data while the
JVComm modem of the PTC-IIpro is in transmission state. That means that
no full-duplex with loop back is possible.

The JVComm transmission routine provides a buffered data exchange with
handshake. This dramaticly reduces the real-time requirements of Win95.
The PTC transmits data exactly with a rate of 1/20 \* Mbaud rate on the
HF side (DSP modem). Because the data rate on account of the 10
steps/byte at the serial interface could be at a maximum 1/10 \* Mbaud
rate, the PC has a lot of time to fill the transmission buffer of the
PTC.

### Specifications

**PTC-data buffer size** over all: 13312 byte

**Handshake** (RTS, PIN 8 at the SUB-D-9 socket of the PTC)

-   Activated (=XOFF, -10 V) at: 8000 byte or more in the buffer

-   Deactivated (=XON, +10 V) at: 6000 byte or less in the buffer

After XOFF the PC could still send about 5000 bytes without causing a
buffer overflow.

**Output data rate**: exactly 1/20 \* Mbaud rate

A skew correction usually is not necessary because the PTC-IIpro quartz
is adjusted up to some ppm.

### Reference of databytes concerning the PTC

<table>
<colgroup>
<col style="width: 13%" />
<col style="width: 50%" />
<col style="width: 26%" />
<col style="width: 9%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Value</strong></td>
<td><strong>Reference</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>0-240</td>
<td>Normal, linear frequency transmission data</td>
<td>0 = 1500 Hz<br />
24 = 2300 Hz</td>
<td></td>
</tr>
<tr class="odd">
<td>241</td>
<td>Sync tone</td>
<td><blockquote>
<p>1100 Hz</p>
</blockquote></td>
<td></td>
</tr>
<tr class="even">
<td>242</td>
<td>Sync tone</td>
<td>1200 Hz</td>
<td></td>
</tr>
<tr class="odd">
<td>243</td>
<td>Sync tone</td>
<td>1300 Hz</td>
<td></td>
</tr>
<tr class="even">
<td colspan="4">The values 0-243 trigger the PTT and the transmission mode of the JVComm modem. As soon as one of these bytes is received, the PTC usually switches to transmit and keeps this condition for (2500 * 1/data rate) seconds (re-triggerable). At a modem baud rate of 57600 baud the TX tail has a length of 0,868 seconds.</td>
</tr>
<tr class="odd">
<td>244-250</td>
<td colspan="2">Reserved for future extensions (no functionality, bytes are ignored)</td>
<td></td>
</tr>
<tr class="even">
<td>251</td>
<td colspan="2">Activates the phasing LED at the PTC front panel.</td>
<td></td>
</tr>
<tr class="odd">
<td>252</td>
<td colspan="2">Deactivates the phasing LED at the PTC front panel (Direct analysis, not via data buffer). This LED can be used during the receiving operation to signalize sync pulses etc.</td>
<td></td>
</tr>
<tr class="even">
<td>253</td>
<td colspan="2">Deletes the transmission data buffer and shortens the TX tail to 0. (Direct analysis, not via data buffer). This command can be used to terminate a picture.</td>
<td></td>
</tr>
<tr class="odd">
<td>254</td>
<td colspan="2">Deletes the transmission data buffer and shortens the TX tail to 0. (Analysis via data buffer). This byte defines the regular end of a picture. It must be added to each picture to deactivate the transceiver directly after picture end.</td>
<td></td>
</tr>
<tr class="even">
<td>255</td>
<td colspan="2">Ends the JVComm modem. Jump to the STBY mode of the PTC (Direct analysis, not via data buffer).</td>
<td></td>
</tr>
</tbody>
</table>

### LED functions

**Receiving mode**

The LED behavior is the same as in the Fmfax modem.

But it is possible to control the phasing LED from the PC side with the
data bytes 251/252.

**Transmission mode**

-   Send LED active.

-   Phasing LED active, as long as the data byte processing is in the
    range of 241-243.

-   Traffic LED active in the XOFF state.

-   LED´s of the tuning indicator. Data byte 0=left-corner, data byte
    240= right-corner.

**Important Note:**

The JVComm transmission routine of the PTC-IIpro is supported from the
JVComm32 version newer than 0.96c beta by JVComm32.

It is possible to download JVComm32 in the internet from the
JVComm-WWW-Site http://www.jvcomm.de[2].

## Fax:-menu commands

When in the main-menu (**cmd:**-prompt), the **FAX** -command leads to
the **fax:**-menu. The menu announces itself only with the prompt
**fax:** (the description **fax:** is misleading because within this
menu additional modes are available). In the **fax:**-menu the following
commands are available:

**Amfax**, **Fmfax**, **Jvfax**, **JVComm**, **Sstv**, **FSk**,
**Comparator**, **PR300**, **AGain**, **AResolut**, **FResolut**,
**SResolut**, **FSKBAud**, **Deviation**, **MBaud**, **SMode**,
**TXcomp**, **HSynch**, **JSynch**, **ASynch**.

All other (*normal*) commands are not available in the **fax:**-menu!
**Quit** or **DD** exit the **fax:**-menu.

All commands in the **fax:**-menu may also be carried out from the main
menu, by setting the prefix **FAX** before the actual command.

**cmd:** **FAX** JVFAX \<Return>

This is corresponding with the usual convention of the other sub-menus,
e.g**. sys:**-menu or **trx:**-menu.

The **fax:**-menu consists of two basic types of commands, the *MODEM*
commands and the *PARAMETER* commands.

The carrying out of a Modem command sets the PTC-IIpro into the actual
FAX/SSTV/AUX modem function. It loads the appropriate new routines into
the signal processor, adjusts the tuning indicator to the new function
and at once starts passing the demodulated signal to the RS-232
interface - which may have had its baud rate changed during the Modem
command, refer to the **MBaud**-Parameter command.

The MODEM operation of the PTC-IIpro can be ended at any time by
inputting a byte with the value 255 (dec). via the RS-232 port. It is
essential to use the correct baud rate (see MBaud-command!). After the
ending of Modem operation, the PTC-IIpro announces itself with the
normal **cmd:**-prompt, and is at once in the main menu. The baud rate
is automatically returned to the value it was before the Modem command
was called.

The PARAMETER commands are used for setting the various values needed
for the particular Modem mode chosen, e.g. the actual baud rate during
Modem operation (**MBaud**), the deviation for FM-FAX (**Deviation**),
or the internal amplification for AM-FAX (**AGain** parameter).

The Parameters must be set before the start of the chosen Modem
function! During MODEM operation, the Parameter commands are not
available; only the change of particular operating parameters in the
operating mode **JVFAX** is possible using special control-codes (refer
to the **JVFAX** modem command).

Note concerning the data-rate during MODEM operation:

The received data is sent with the maximum possible speed to the serial
interface in all MODEM operating modes. There are no pauses between the
individual characters, not even through excessive use of the
Packet-Radio function of the PTC-IIpro multi-tasking. With an
**MBaud**-rate for example, of 57600 bits/sec, there is a new value
available for the connected PC approximately every 170 μsec (10 steps of
1/57600 sec per step). A guarantee of modem data synchronization over a
long period, cannot however be given.

| Connects in Packet-Radio from outside are also possible during active MODEM functions without restrictions. Receiving data will be buffered as far as buffer is available. |

## The PTC-IIpro as COMPARATOR-MODEM

The PTC-IIpro is capable to be used as a simple COMPARATOR-Modem. This
allows compatibility to all at present available RTTY/FAX/SSTV programs
that allow use of a *simple modem* (e.g. HAMCOMM modem). The operation
as a COMPARATOR is completely different to that of the other MODEM
variants of the PTC-IIpro. In the normal MODEM operation (**Amfax**,
**Fmfax**, **SSTV** commands), the DSP undertakes the demodulation of
the signal itself, and uses relative complex algorithms. In the
COMPARATOR mode, it is only used as an adjustable pre-filter (bandpass
filter, Fresol command). The prefiltered signal is then only hard
limited, and passed to PIN 6 (DCD) of the RS-232 interface. The actual
demodulation must be undertaken by the PC program, so that considerable
differences in quality may occur.

## MODEM commands in detail

|     | Activating the MODEM commands is the task of the displaying programs on the PC, e.g. JVCOMM32 or MSCAN. They are not intended for direct user access. If somebody tries to call for example SSTV out of terminal programs like PlusTerm, he will be punished with the output of a never ending data stream of hex characters |

### Amfax

Starts the AM-FAX-MODEM. The measured amplitude of the 2400 Hz tone
frequency is given over the RS-232 interface at the rate set using the
**MBaud** command.

The time-resolution required, and filter bandwidth may be pre-set using
the **AResolut** parameter. The internal amplification may be pre-set
using the **AGain** parameter. The output values reach from 0 to 255.
Measured values greater than 255 are limited to 255 by the PTC-IIpro.
(The data width is limited to 8 bits by the serial format.) With an AF
input amplitude of 500 mV, and a standard setting of **AGain** (50), the
PTC-IIpro gives an output value of 255. With an input of 250 mV the
output value is appropriately 128.

The tuning indicator displays the output values. The lower signal values
lie to the left, the greater to the right.

For transmission use when using AM-FAX, refer to chapter 8.7.1, page 134
and chapter 8.7.1, page 134.

### Fmfax

Starts the FM-FAX-MODEM. The measured *instantaneous* signal frequency
is sent via the RS-232 serial interface, at the rate set by the
**MBaud** command.

The time-resolution required, and filter bandwidth may be pre-set using
the **FResolut** parameter. The *steepness* of the FM-detector may be
pre-set using the **Deviation** parameter. The output values reach from
0 to 255. Measured values smaller than 0 are output as 0. Values greater
than 255 are limited to 255 by the PTC-IIpro. The center frequency is
exactly 1900 Hz. With a frequency of 1900 Hz as AF input, the PTC-IIpro
always gives out the appropriate value of 128. With the standard setting
of 400 Hz shift (Deviation = 400), then an output value of 255 is
obtained with an input frequency of 2300 Hz, and the input frequency of
1500 Hz gives an output value of 0.

The tuning indicator displays the output values. The *left-hand limit*
represents 1500 Hz (by the standard setting of 400 Hz shift) and the
*right-hand limit* 2300 Hz.

For transmission use when in FM-FAX operation, refer to chapter 8.7.1,
page 134.

### Sstv

Starts the SSTV-MODEM. This MODEM resembles very closely the FM-FAX-
MODEM (see Fmfax- MODEM command). It consists of an FM detector with a
center frequency of 1900 Hz and a pre-set shift of 400 Hz. (Independent
from the Deviation-Parameter). The Black and White limit frequencies are
appropriately 1500 and 2300 Hz. The maximum possible resolution and
input filter bandwidth may be pre-set using the **SResolut** parameter.

Unlike the FM-FAX-Modem, values smaller than 0 (measured frequency lower
than 1500 Hz) or greater than 255 (measured frequency higher than 2300
Hz) are not just limited to 0 or 255. In SSTV, It has been found
advantageous to *fold-back* *incorrect* values into the correct area. If
the system, for example, measures a frequency of 2700 Hz, then it does
not give out a value of 255. Instead, the output value is calculated
using the formula

255- (2700-2300)/800\*128.

This *folding-back* has been shown to give less color errors in
*multipath* propagation conditions, and with other interference
conditions. As the tuning indicator also displays the output values in
SSTV-Modem operation, this *folding-back* can perhaps be somewhat
confusing during tuning operation.

The SSTV synchronization pulse using a frequency of 1200 Hz is filtered
independently from the FM-Detector, and is processed with the help of a
relatively complex threshold value method. Basically, the PTC-IIpro
interprets these pulses as being a separate amplitude modulated signal,
independent of the picture information. As a special new development,
the PTC-IIpro can use a processing method especially designed for the
line synch-pulse, that virtually accumulates the information over a
number of lines. As this processing algorithm requires the line
synch-pulse timing for correct operation, there exists a special command
(**SMode**), with the help of which the PTC-IIpro is informed of the
current SSTV sub-mode being used. The multi-line check may be turned
off, which deteriorates the synch recognition, but however, does allow
*unknown* SSTV-transmissions to be processed without problem when a good
signal to noise ratio is available.

The PTC-IIpro uses the standard given in the **JVFAX** documentation, to
pass the recognized synchronization pulses to the PC program. The system
uses the lower two bits of every byte to indicate the synch pulse. Bits
0 and 1 are set to 1 in the resting state. As soon as the PTC-IIpro
recognizes a correct synch-pulse on the 1200 Hz frequency, it sets the
bits 0 and 1 to 0 for the time the synch-pulse occurs. (Note: the VIS
code is at present not processed by the PTC-IIpro, and therefore bit 2
is actually redundant for the signaling condition.) The small decrease
in color resolution caused by only having 6 bits to signal brilliance
information can, in practice, be ignored.

The JVFAX sync method used by the PTC may be turned off using the
**JSynch** parameter command. In theory, the PTC-IIpro may be used with
the JVFAX in the operational condition **LSB-SSTV-SYNCH NO**. Then the
system uses the full 8 bit data width for picture information. The
practical results however speak against using this method.

With the **JSynch** parameter turned on (default setting), the
recognized synchronization pulse is signaled to the user by using LED´s:

Line synch-pulses are shown by the PTC-IIpro with a short blink of the
Phasing-LED (red). A vertical synch-pulse (picture new start) lights the
Connected-LED (yellow) shortly. A small time offset of the line-synch
pulse may be set by use of the **HSynch** parameter. This allows the
whole picture to be shifted slightly left or right.

For transmission use when in SSTV-MODEM operation, refer to chapter
8.7.1, page 134.

### Jvfax

Starts the JVFAX mode. This mode does not contain its own Modem as such.
Instead, it offers a sort of "*springboard*" to FM-FAX, AM-FAX and SSTV
by using special control sequences, that are recognized in this mode by
the PTC-IIpro. Directly after switching to JVFAX operation, the
PTC-IIpro is in Modem mode FM-FAX, using a shift which has been preset
using the **Deviation** parameter (normally 400 Hz). In addition to the
actual operating mode, the PTC-IIpro's matrix display also shows the
characters JV as its first two characters, signaling that control
sequences will be accepted.

The following *1-Byte commands* are accepted by the PTC-IIpro when in
JVFAX mode:

| Byte | **Function**                         |
|------|--------------------------------------|
| $49: | Switches to AM-FAX                   |
| $4A: | Switches to AM-FAX                   |
|      |                                      |
| $4B: | Switches to SSTV                     |
|      |                                      |
| $41: | Switches to FM-FAX with 150 Hz shift |
| $42: | Switches to FM-FAX with 200 Hz shift |
| $43: | Switches to FM-FAX with 300 Hz shift |
| $44: | Switches to FM-FAX with 350 Hz shift |
| $45: | Switches to FM-FAX with 400 Hz shift |
| $46: | Switches to FM-FAX with 500 Hz shift |

Table 8.1: JVFAX Control Bytes

All shift settings done via the control sequences changes the shift for
the moment (*local*). The value of the **Deviation**-parameters remains
unchanged.

### JVComm

Starts the JVComm modem of the PTC-IIpro.

Entering no argument the PTC-IIpro displays the string **JVCComm32**.
Any string can be entered for the display. The first character of the
argument will not be displayed, it only marks the start of the string,
this makes it possible to enter blanks in the display.

The string TESTFAX can be entered in the display in the following way:

**fax:** **JVC** : TESTFAX \<Return>

At a maximum 10 characters can be displayed. In the example the colon
has the function to mark the beginning of the string (started with a
blank). The colon will not be displayed.

### FSK

Starts the NFSK-Modem. This is very similar to the FM-FAX demodulator.
This detector however is designed for a very much slower data rate
compared to the FM-FAX detector. The input bandpass-filter can be
considerably narrower than that for FAX operation. The base-band
low-pass filter at the output of the demodulator may be changed to 200,
300 or 400 baud signal rate, by using the **FSKBaud** Parameters
command.

The PTC-IIpro is therefore highly suitable, when used in the MODEM
operational mode FSK as a demodulator for widely differing transmission
methods. Packet-Radio with 300 Baud and multi-FSK systems such as
PICCOLO etc. may be received when the appropriate PC program is
available.

The NFSK-demodulator gives the measured frequency value to the RS-232
interface, at a baud rate set by the **MBaud** command. The center
frequency is here also 1900 Hz. This frequency causes an output value of
128. A frequency range of ±500 Hz gives an output value of between 0 and
255. For frequencies outside this *measurement* range, the PTC-IIpro
gives values of 0 or 255 whilst in FSK-MODEM operation.

Additionally, as in all FM modes, the data from the demodulator is
available at PIN 6 of the RS-232 interface. It has passed a trigger
stage, which results in a 1-bit digitized signal as output. If the
PTC-IIpro measures an input frequency of greater than 1900 Hz, then PIN
6 goes to -10 Volts. For frequencies lower than 1900 Hz, the PTC-IIpro
sets PIN 6 to +10 Volts.

As in other FM-MODEM operating modes, the tuning indicator indicates the
output value directly.

For transmission using the NFSK-MODEM, refer to chapter 8.7.1, page 134.

### Comparator

This MODEM command switches the PTC-IIpro into the COMPARATOR mode. The
prefiltered receive signal, (filter bandwidth may be set with the
**FResolut** parameter command), is limited and transferred to PIN 6
(DCD) of the RS-232 interface. The RS-232 port is, as in all other MODEM
operations, still able to receive data. The COMPARATOR operations may be
aborted when a byte value of 255 is received by the RS-232 interface.
The baudrate is also during COMPARATOR operation set to the value given
in the **Mbaud** command.

The PC-program used must be configured to simple modem such as
**HAMCOMM** or **COMPARATOR**

<table>
<colgroup>
<col style="width: 10%" />
<col style="width: 89%" />
</colgroup>
<tbody>
<tr class="odd">
<td></td>
<td><p>The multitasking system of the PTC-IIpro is turned off during COMPARATOR operation due to the very high time resolution needed to form the limited square wave receive signal on the DCD PIN.</p>
<p>PR-operation using the integrated modules of the PTC-IIpro during COMPARATOR-MODEM operation is not possible!</p></td>
</tr>
</tbody>
</table>

### PTC-IIpro with 300 baud HF Packet

|     |                                                                                                                                                                                                         |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This chapter describes a way to operate 300 baud HF Packet, but it is not the best and recommended way to do it. It is recommended to use the DSP Packet-Radio-Module-II to operate 300 baud HF Packet! |

300 Baud Packet operation is possible with the PTC-IIpro when using the
program **TFX** in addition. **TFX** is started on the PC as a TSR
program (memory resident) and discretely operates the packet protocol in
the background. The PTC-IIpro itself operates as a modulator/demodulator
in this case, such as **BayCom** or **PC-COM**. The combination of
PTC-IIpro and **TFX** emulates a *real* hostmode TNC for 300 baud Packet
that can be operated with a hostmode terminal program such as **GP**.
The command **PR300** starts the **TFX** compatible 300 baud PR modem.

|     |                                                                                                         |
|-----|---------------------------------------------------------------------------------------------------------|
|     | Multitasking is disabled in this case, therefore no VHF/UHF Packet operation is possible the same time. |

The LED´s are set to medium brightness, i.e. the **BRightness**
parameter has no function.

**TFX** should be used with *hardware DCD* turned on. The MARK tone is
the one also valid for PACTOR and the SPACE tone is always located
exactly 200 Hz below the MARK tone.

The **TFX** program is available at nearly every Packet-Radio mailbox or
in the internet at

http://www.nordlink.org[3]

## Transmission during MODEM operation

In every MODEM-operational mode, independent of if it is AM-FAX, FM-FAX,
SSTV or FSK, the PTC-IIpro keys the transmitter (PTT becomes active)
when it receives bytes with a value between 0 and 63. The transmitter
stays on for exactly 166.7 ms after receiving each *transmit-byte*. If
the PC program sends the transmit data appropriately fast, then the
transmitter stays in the transmit condition. If the data does not change
within the 166.7 ms (for example when in FM-FAX only *white* must be
transmitted), then the PC program must send data to the PTC-IIpro at
least every 166.7 ms, so that the transmitter stays on transmit. By
using this system, an extra PTT-command is not required.

The maximum transmit amplitude is set using the **FSKAmpl** in the main
menu. It is not necessary for any new setting to be undertaken, and can
be left at setting for PACTOR or RTTY.

The PTC-IIpro displays the present transmit data on the tuning indicator
directly. The *left-hand limit* represents the value 0, the *right-hand
limit* 63.

During the transmit operation, the appropriate demodulator operates
unchanged (up to the LED-display). The PTC-IIpro always operates in the
special modes as a FULL-DUPLEX MODEM.

### Transmission in AM-FAX-Modem mode

For transmit operation in AM-FAX a constant carrier tone of 2400 Hz is
generated. The transmit data controls the amplitude of this tone: The
value 0 means the carrier tone disappears. The value 63 causes the
maximum amplitude to be generated (that set by the **FSKAmpl** command).
The transmit data controls the signal processor directly and without
delays. The transmit signal bandwidth is also not limited through any
hardware filter.

### Transmission in FM-FAX/FSK/SSTV-Modem mode

For transmit operation in all FM variants, a constant amplitude signal
is generated (that set by the **FSKAmpl** command), the frequency of
which relates to the transmit data amplitude. The transmitted data
controls the instantaneous frequency of the output signal. For the value
0, the PTC-IIpro generates a frequency of 1500 Hz. The value 63 produces
a frequency of 2300 Hz. Values between these limits produce the
appropriate frequencies between 1500 and 2300 Hz. The frequency
modulator in the DSP operates phase-continuous, and therefore produces a
very clean and spectrally narrow signal. An output bandpass filter has
thus been omitted.

The steepness of the frequency modulator is independent of the
**Deviation** parameter, or other settings. The maximum possible shift
of the transmitted FSK signal however is thus limited to 800 Hz.

In order to generate the synchronization signal below 1500 Hz, the
PTC-IIpro must *understand* (as stated in the JVFAX-standard) three
further bytes outside the 0-63 as transmit-data:

125 (dec.) generates the frequency 1100 Hz.

126 (dec.) generates the frequency 1200 Hz.

127 (dec.) generates the frequency 1300 Hz.

The Phasing-LED lights red during transmission of a synchronization
tone.

### Transmission in COMPARATOR mode

The transmission using the COMPARATOR MODEM is controlled with the
**TXcomp** parameter (please refer chapter 8.8.11, page 139TXcomp). If
**TXcomp** is switched on, the handshake line CTS is used to control the
PTT line, and the RxD PIN of the port supplies the transmission data.
This method provides a very clear transmission signal, but has to be
supported by a corresponding PC program.

If **TXcomp** is switched off, the PTT control via the CTS line is
ignored. The transmission is completely handled by the PC program. As
modulation signal, the audio signal of the *PC speaker* is used.
However, this method is usually not recommended and hardly needs to be
used.

## The Parameter commands in detail

### AGain

|                         |     |                                            |     |
|-------------------------|-----|--------------------------------------------|-----|
| **Default setting: 50** |     |                                            |     |
|                         |     |                                            |     |
| Parameter:              | X   | 1... 200, amplification factor for AM-FAX. |     |

Sets the internal amplification factor for AM-FAX reception. The
brilliance of the received picture can thus be set, without having to
change the receiver volume. Some receivers offer an AF-output with a
virtually constant amplitude. In this case, **AGain** offers almost the
only possibility to adjust the brilliance of the received picture. With
the **AGain** default value of 50, an input signal of 500 mV causes the
maximum output value of 255 at the RS-232 interface. The **AGain**
-Parameter operates as a linear amplification factor.

### AResolut

|                        |     |                 |     |
|------------------------|-----|-----------------|-----|
| **Default setting: 2** |     |                 |     |
|                        |     |                 |     |
| Parameter:             | 0   | 1680 Pixel/sec. |     |
|                        | 1   | 2500 Pixel/sec. |     |
|                        | 2   | 3400 Pixel/sec. |     |

Gives the maximum possible time resolution of the received signal in
AM-FAX. Also the **AResolut** parameter adjusts the bandwidth of the
input bandpass-filter appropriately. With noisy signals, it is
recommended that the **AResolut** parameter is set to 0, as the
effective signal to noise ratio is thereby increased. The maximum
resolution is as follows: 0=1680 pixels/sec., 1=2500 pixels/sec, 2=3400
pixels/sec.

### FResolut

|                        |     |                 |     |
|------------------------|-----|-----------------|-----|
| **Default setting: 2** |     |                 |     |
|                        |     |                 |     |
| Parameter:             | 0   | 1000 Pixel/sec. |     |
|                        | 1   | 1500 Pixel/sec. |     |
|                        | 2   | 2000 Pixel/sec. |     |
|                        | 3   | 2800 Pixel/sec. |     |

Gives the maximum possible time resolution of the received signal in
FM-FAX. Also the **FResolut** parameter adjusts the bandwidth of the
input bandpass-filter appropriately. With noisy signals, it is
recommended that the **FResolut** parameter is set to 0, as the
effective signal to noise ratio is thereby increased. The maximum
resolution is as follows: 0=1000 pixels/sec., 1=1500 pixels/sec, 2=2000
pixels/sec, 3=2800 pixels/sec.

### SResolut

|                        |     |                 |     |
|------------------------|-----|-----------------|-----|
| **Default setting: 2** |     |                 |     |
|                        |     |                 |     |
| Parameter:             | 0   | 1000 Pixel/sec. |     |
|                        | 1   | 1500 Pixel/sec. |     |
|                        | 2   | 2000 Pixel/sec. |     |
|                        | 3   | 2800 Pixel/sec. |     |

Gives the maximum possible time resolution of the received signal in
SSTV. Also the **SResolut** parameter adjusts the bandwidth of the input
bandpass-filter appropriately. With noisy signals, it is recommended
that the **SResolut** parameter is set to 0, as the effective signal to
noise ratio is thereby increased. The maximum resolution is as follows:
0=1000 pixels/sec., 1=1500 pixels/sec, 2=2000 pixels/sec, 3=2800
pixels/sec.

### FSKBaud

|                        |     |           |     |
|------------------------|-----|-----------|-----|
| **Default setting: 3** |     |           |     |
|                        |     |           |     |
| Parameter:             | 2   | 200 Baud. |     |
|                        | 3   | 300 Baud. |     |
|                        | 4   | 400 Baud. |     |

Gives the maximum possible baud rate that the NFSK-demodulator can
process without inter-symbol interference (ISI, signal-smearing). With
noisy signals, it is recommended that the **FSKBaud** parameter is set
to 2, provided the received signal has a baud rate of 200 or less, as
the effective signal to noise ratio is thereby increased. Baud
rate-settings: 2=200 Bd, 3=300 Bd, 4=400 Bd.

### Deviation

|                          |     |                                                     |     |
|--------------------------|-----|-----------------------------------------------------|-----|
| **Default setting: 400** |     |                                                     |     |
|                          |     |                                                     |     |
| Parameter:               | X   | 100... 1000, shift of the FM-FAX demodulator in Hz. |     |

Sets the steepness (shift) of the FM-FAX demodulator. (NOTE: in
JVFAX-mode, the shift can be changed using special control bytes
independently of the **Deviation**-Parameter settings.) A **Deviation**
value of 400 means that the demodulator will process a frequency range
from 1500 Hz to 2300 Hz, i.e. frequencies from 1900-400 Hz to 1900+400
Hz.

### MBaud

|                            |     |                                                  |     |
|----------------------------|-----|--------------------------------------------------|-----|
| **Default setting: 57600** |     |                                                  |     |
|                            |     |                                                  |     |
| Parameter:                 | X   | 1200... 115200, baudrate during modem operation. |     |

Sets the baud rate used by the serial interface during MODEM operation,
i.e. whilst a FAX, SSTV or FSK-Modem is active. For the optimum display
of high resolution FAX pictures, it is recommended that the rate is set
to at least 57600, as long as the PC-program in use will support that
speed. Additionally, if at all possible, the baudrate should be a
multiple of 19200, in order that the SSTV synchronization processing
works correctly.

### HSynch

|                         |     |                                        |     |
|-------------------------|-----|----------------------------------------|-----|
| **Default setting: 50** |     |                                        |     |
|                         |     |                                        |     |
| Parameter:              | X   | 10... 100, position of the sync pulse. |     |

Sets the effective point in time where a recognized SSTV synchronization
pulse, as such, is inserted into the received data-stream. Small
corrections to the positioning of the picture edges can be made here by
shifting the entire picture right or left. Normally, no changes in the
**HSynch** default setting is required.

### JSynch

|                        |     |                         |     |
|------------------------|-----|-------------------------|-----|
| **Default setting: 1** |     |                         |     |
|                        |     |                         |     |
| Parameter:             | 0   | LSB-SSTV-Sync disabled. |     |
|                        | 1   | LSB-SSTV-Sync enabled.  |     |

Activates (1) or de-activates (0) the LSB-SSTV synchronization mode for
SSTV. In this mode, the PTC-IIpro processes the SSTV synch-pulses
separately, and re-introduces them, according to the JVFAX convention,
into the two lowest bits of each of the data-bytes given out to the
RS-232 interface. If there is no synch-pulse present, then the two
lowest bits (0 and 1) are set to 1. The PTC-IIpro erases the two lower
bits for the period of a synch-pulse.

### SMode

|                        |     |                         |     |
|------------------------|-----|-------------------------|-----|
| **Default setting: 1** |     |                         |     |
|                        |     |                         |     |
| Parameter:             | X   | 0... 15, SSTV sub mode. |     |

Sets the SSTV sub-mode required. The **SMode** parameter is only used
for the SSTV line-synch processing, as it is only here that specific
information about the various SSTV sub-modes is required. If one wishes
to work with any sort of SSTV signal, that is not in the following list,
then the **SMode** parameter must be set to 0.

This has the effect that multiple-line checking of the synch processing
is turned off. The PTC-IIpro works perfectly satisfactory in this mode,
but weak signals naturally lead sometimes to a loss of synch with the
normal synch pulse processing, with it's resultant picture distortion.

|     |                                                                                                                                                                                                                              |
|-----|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | The multiple synch-check (**SMode** parameter not equal to 0) will only work without problem when the Modem baud rate (set via the **MBaud** parameter) a multiple of 19200, i.e. 19200, 38400, 57600, 76800 or 115200 Baud. |

The PTC-IIpro shows the SSTV-submode with a 2 character long
abbreviation of the first 2 characters of the green matrix display.

The following SSTV-modes are supported by the PTC-IIpro:

| **SMode** | **MODE-Name**     | **Abbr. in display** |
|-----------|-------------------|----------------------|
| 0         | ALLMODE           | --                   |
| 1         | MARTIN 1          | M1                   |
| 2         | MARTIN 2          | M2                   |
| 3         | SCOTTIE 1         | S1                   |
| 4         | SCOTTIE 2         | S2                   |
| 5         | SCOTTIE DX        | SD                   |
| 6         | 8 sec / 120 line  | 08                   |
| 7         | 16 sec / 120 line | 16                   |
| 8         | 32 sec / 240 line | 32                   |
| 9         | WRAASE 24/128     | W1                   |
| 10        | WRAASE 48/128     | W2                   |
| 11        | WRAASE 48/256     | W3                   |
| 12        | WRAASE 96/256     | W4                   |
| 13        | WRAASE 120/256    | W5                   |
| 14        | WRAASE 180/256    | W6                   |
| 15        | ROBOT 72/256      | R1                   |

Table 8.2: STTV sub modes

### TXcomp

|                        |     |                         |     |
|------------------------|-----|-------------------------|-----|
| **Default setting: 0** |     |                         |     |
|                        |     |                         |     |
| Parameter:             | 0   | COMPARATOR Tx disabled. |     |
|                        | 1   | COMPARATOR Tx enabled.  |     |

This PARAMETER-command activates (1) or de-activates (0) the
TXD-modulator in the COMPARATOR mode. With **TXcomp** switched on, it is
possible for many programs that support the HAMCOMM-modem to send FAX
and SSTV direct from the PTC-IIpro. The PTC-IIpro looks at the voltage
appearing on the CTS-line (PIN 7 of the RS-232 interface). When +10
volts appears, the PTT line for the shortwave port is activated. The PTT
line is de-activated (turned off) when the voltage is -10 V. When in the
send condition, the PTC-IIpro measures the incoming data as square wave
modulation data on the RxD PIN.

The zero crossing point is measured very exactly, and then modulates the
*VCO* in the DSP. The PTC-IIpro has a very good transmit resolution even
in the *Simple Modem* mode, providing the PC program works as precisely.
The translation of the transmit-data into a *clean* analogue signal is
not just through an RC low pass filter (as is usual). Instead, the
system calculates exactly the reverse of the simple demodulator
principle.

## LED functions and matrix-display

### The LED´s whilst receiving

When the **Jsynch** parameter is turned on, the Phasing-LED (red) shows
a line-synch pulse by blinking. The Connected-LED (yellow) blinks when a
vertical (frame) synch-pulse is received during SSTV operation.

### The LED´s whilst transmitting

The Phasing-LED displays tones between 1100 and 1300 Hz.

The tuning indicator displays directly in every mode the output value
(0-255) or input (whilst transmitting) value (0-63). The *left-hand
limit* represents value zero, the *right-hand limit*, the maximum value.

During transmit, the modulator has priority with respect to the LED
control. The tuning indicator displays the transmitted data condition,
although the PTC-IIpro, operating as a FULL-DUPLEX MODEM, continues to
produce receive data.

### Information in the Matrix Display

If a branch is made to the FAX sub-menu, then **FAX MENU** is displayed.

In each MODEM condition, the center of the display shows the Modem mode,
e.g.  
**AM-FAX**, **FSK**, **SSTV** etc.

If the actual MODEM is chosen from the JVFAX-MODE by use of a
control-byte (refer to chapter 8.6.4, page 131), the first two
characters of the display show the letters **JV**. Otherwise -- is
displayed.

During SSTV operation, the last two characters show an abbreviated form
of the chosen SSTV sub-mode (refer to **SMode** parameter command,
chapter 8.8.10, page 138).

The NFSK-MODEM shows the last three characters of the maximum baud rate
limit of the demodulator (refer to **FSKBaud** parameter command,
chapter 8.8.5, page 137).

### Tuning- and LED display in COMPARATOR mode

The tuning indicator covers the range 1900 ± 800 Hz in both transmit and
receive operation. In addition, during transmit, the Send-LED on the
PTC-IIpro lights green. The green alphanumeric display shows
**COMPARATOR** during COMPARATOR operation.

The LED´s are always switched to middle brightness during COMPARATOR
operation, again due to the computer time needed. The **BRightn**
parameter has no thus effect during the time the PTC-IIpro is switched
to COMPARATOR.

### LED´s in PR300 operation

The following LED´s are in use: Tuning-display, Send-LED (green) for
PTT, Phasing-LED (red) for DCD (digital carrier detect).

## Tips and Tricks

### IF-SHIFT

With the normal SSB speech reception, the speech frequencies stretch
from 300 to 2700 Hz. Steep sided SSB filters usually have a 6 dB
bandwidth of around 2.4 kHz. The FM-FAX standard sets a center frequency
of 1900 Hz. With standard resolution FAX and SSTV pictures, the signal
requires a bandwidth of approximately 2.5 kHz. The audio limit
frequencies that should be transmitted are 1900-1250 Hz and 1900+1250 Hz
or 750 Hz and 3150 Hz. The frequency band for FAX/SSTV appears to be
shifted about 400 to 500 Hz higher in frequency. With normal SSB
reception, the higher FAX/SSTV tones suffer great attenuation and
thereby cause asymmetrical reception.

In order to help this situation, it is recommended that the IF-SHIFT
control be used. With the TS-450 for example, it has been found that the
best setting is around *3 o’clock*. The ideal setting is that at which
the tuning indicator flickers symmetrically around the middle point when
only noise is present on the receive channel.

### Tuning with SSTV

The FAX/SSTV tuning indicator is (by its very nature) a somewhat
*diffused* and in-exact indicator. It has been shown, that tuning for a
*clean* and rhythmical blinking of the Phasing-LED at line frequency, is
a good way of tuning in SSTV signals. The **JSynch** parameter must
naturally be set to 1.
