# TRX

The `TRX`-command (without argument) activates the transceiver remote
control menu (**trx:**-menu). The command prompt takes the form
**trx:**. The following commands are allowed within the **trx:**-menu:

```
DD, DUmp, Frequency, Help, IType, KType, Offset, Parity, Quit, RTS, SAP, Transfer, TYpe, YType
```

All other (*normal*) commands are not available from within the
**trx:**-menu. The **trx:**-menu may be closed either with `DD` or
`Quit`.

The `TRX`-command may also contain an argument, this being a suitable
command from the **trx:**-menu. In this case the modem will then carry out
this command, without switching to the **trx:**-menu. The control
command may be said to be fed through.

Example:
This command, for example, would change the frequency of a connected
transceiver directly to 14079.0 kHz - without having to divert to the **trx:**-menu.
```
cmd: TRX Frequency 14079.0<Return>
```
All important TRX-parameter are stored in the Flash-ROM directly at
input and are reloaded with the `RESTart` command:

`Type`: Transceiver type, baudrate, address/VFO, V24 parameter  
`Parity`: Parity  
`KType`: Kenwood type  
`YType`: Yaesu type  
`RType`: R&S type

The **trx:**-menu commands in detail:


## DD

Leave the **trx:**-menu. The command prompt returns to
its *normal* form (**cmd:**). Identical to the [`Quit`](#quit) command.


## DUmp

|                        |     |                     |     |
|------------------------|-----|---------------------|-----|
| **Default setting: 0** |     |                     |     |
|                        |     |                     |     |
| Parameter:             | 0   | Dump mode disabled. |     |
|                        | 1   | Dump mode enabled.  |     |

With the command **Dump** 1 \<Return>, the PTC-IIpro is switched to
transceiver dump mode, this mode providing a very simple Host mode for
direct communication between the terminal program and the transceiver.
The PTC-IIpro only serves as a level converter or baudrate converter,
and delivers, as required, the necessary signal preamble (for SGC
transceivers), but the actual control sequences must be delivered by the
host computer, or terminal program. In dump mode, the information given
out by the transceiver is transferred direct to the host computer, and
must be processed there.

TRX dump sequences from the host computer (terminal) to the PTC-IIpro
have the same format as the TRX dump sequences from the PTC-IIpro to the
host computer, these consisting of:

1.  TRX dump header, for unambiguous recognition of the TRX dump
    sequences.

<!-- -->

11. The actual data field, in hexadecimal form, (identical to the data
    field when using the Transfer command for SGC, ICOM and YAESU).

12. The end character, CR, (ASCII 13).

Dump sequences always begin with the TRX dump header, this header
consisting of the following; \<Ctrl-E>\<#>\<T>\<X>\<:>, where \<..>
denotes in each case one byte (ASCII), corresponding to 05H 23H 54H 58H
3AH.

The header is only then valid when it appears complete. If, for example,
the third header byte is defective, then the PTC-IIpro behaves as if the
Ctrl-E start character is an accidental Ctrl-E, or an actual Ctrl-E that
has not been input as a TRX control character, the PTC-IIpro then
sending the buffered characters of the intended dump header into the
normal command interpreter or transmit buffer.

If one types, for example, Ctrl-E#TXXX, during an actual PACTOR link,
then these characters would be transmitted over the HF link, and would
not be transferred to the transceiver.

A restrictive processing of the header allows through transfer of
transceiver sequences, WITHOUT, in practice, limiting the data
transparency, the danger of a piece of text being *swallowed*, due to an
accidental Ctrl-E is virtually 0.

The host computer, or terminal program, should, naturally also
thoroughly check the transferred TRX dump sequence, and a "defective"
header should be fed back into the normal process, (e.g. output as text
in the receive window).

The dump header can be followed by up to 256 bytes (or 512 places) of
actual transfer information in hexadecimal form, spaces in this data
field being ignored, and if an uneven number of hexadecimal places
(nibbles) are given, then the PTC-IIpro ignores the last nibble.

A TRX dump sequence is always closed with an ASCII 13 (carriage return),
although this last character is not transferred to the transceiver by
the PTC-IIpro, and the TRX dump sequences from the PTC-IIpro to the host
computer are also closed with ASCII 13.

Example:

The control sequence FA; should be sent directly to a KENWOOD
transceiver via TRX dump. The ASCII character string for this is:

\<Ctrl-E>#TX:46413B\<CR>

Here, the \<..> symbolizes an ASCII special character, CR = carriage
return, and the transceiver answers this command in its turn with a
longer sequence, which the PTC-IIpro passes directly as a TRX dump to
the terminal.

IMPORTANT: Some Transceivers (e.g. KENWOOD TS-450) ONLY accept remote
control commands in the receive condition. The terminal must take this
into consideration, in that (for example), during the linked state, each
of the following acknowledgments are checked to see if the command has
been accepted by the transceiver. If not, then the command must be
repeated after approx. 100 msec, etc. (Possibly with timeout and error
message displays).

Timing of the TRX dump sequences:

Dump sequences to the transceiver are sent a few milliseconds after the
closing \<CR>, as a continuous string, without pauses (idles).

Sequences from the transceiver are transferred, via the PTC-IIpro, to
the terminal as dump sequences when...

1.  With KENWOOD or ICOM Transceivers, the appropriate end character
    (delimiter) is recognized.

<!-- -->

13. The string length reaches 40 characters. That means that the maximum
    info length of the TRX dump from the PTC-IIpro to the terminal is 40
    bytes, although with YAESU transceivers the maximum string length is
    restricted to 19 bytes.

14. If no further information is received from the transceiver for
    longer than 40 byte lengths, and information from the TRX is
    available. (For SGC transceivers this idle timeout has been reduced
    to 20 byte lengths).

There is only a few milliseconds delay between the recognition of the
end condition, and the beginning of the dump sequence,

**Important Note:**

Ctrl-E should no longer be used as *Hot-key*, e.g., as changeover or QRT
key, when the dump mode is activated. If, however, the Ctrl-E should be
defined as a control character, then the PTC-IIpro will not give an
error message, the processing of the Ctrl-E as *Hot-key* being delayed
when the dump mode is active, for a minimum of one character, and the
respective following characters are checked, to see if they are valid
for the TRX dump header, in other words, a buffering taking place.

The Frequency command in the **trx:**-menu, (without argument), requests
the output of the TRX frequency, but with an active dump mode, these
transceiver outputs caused by the **F** command are also shown as dump
sequences, and no longer as a decimal ASCII string. The **F** command in
this case, then also gives a TRX dump sequence. (This is, however, not
the case in remote control access, when the dump mode is ignored).

## DWell

|                         |     |                                   |     |
|-------------------------|-----|-----------------------------------|-----|
| **Default setting: 30** |     |                                   |     |
|                         |     |                                   |     |
| Parameter:              | X   | 5... 1,000, dwell time in 100 ms. |     |

**DWell** sets the dwell time of the PTC scanner on each channel in 100
ms steps. A **DWell** time of 30 means, for example, that the scanner
will pause on each channel for exactly 3 seconds.

## Frequency

|                           |     |                 |     |
|---------------------------|-----|-----------------|-----|
| **Default setting: NONE** |     |                 |     |
|                           |     |                 |     |
| Parameter:                | X   | Frequency data. |     |

Allows the direct setting of the TRX frequency, without having to define
a scan channel. The format is, however, that as described in the
**Channel** command.

Without a parameter the Frequency command returns the current operating
frequency from the transceiver.

|     |                                                                                                                                                                               |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | If a beep is heard during frequency input or scanning, that’s not the PTC-IIpro, that’s the transceiver. Refer to the transceiver manual to switch off the confirmation beep! |

## Help

Gives a short list of the commands used in the **trx:**-menu. The Help
command may also contain a command word from the **trx:**-menu as
argument, whereby a description of that command is given.

Special information to the **Channel** command

**trx:** **Help** Channel \<Return>

## KType

|                  |     |                                                         |
|------------------|-----|---------------------------------------------------------|
| Default setting: | 0   |                                                         |
| Parameter:       | 0   | Normal Kenwood protocol.                                |
|                  | 1   | Modified Kenwood protocol for newer Yaesu transceivers. |

Modern Yaesu transceivers, e.g. FT-450, FT-950, FT-2000, FT-9000 utilize
a new communications protocol on the remote control port (CAT), which is
quite similar to the protocol used by Kenwood transceivers. Therefore, a
slight adaption of the Kenwood protocol is sufficient to achive
compatibility with the transceivers mentioned above. This transceivers
are controllable with the setting

**trx:** KTyp**e** 1 \<Return>

followed by

**trx:** Typ**e K 4800 A V24** \<Return>

with the PTC-IIpro.

## List (remotable as command TRX List)

Lists the entire defined PTC frequency list. Refer also to the
**Channel** command, chapter 13.1

## Offset

|                        |     |                                 |
|------------------------|-----|---------------------------------|
| **Default setting: 0** |     |                                 |
|                        |     |                                 |
| Parameter:             | X   | -5,000... 5,000, offset in kHz. |

Frequency format as for the **Channel** command

The Offset value is applied to **every** frequency (Channel list,
Frequency command etc). before it is output to the transceiver.

This allows, even whilst in SSB mode, the transceiver to be set to the
Mark frequency of the PTC of the other station. If, for instance, Low
tones are being used (1200/1400 Hz **TOnes**-Parameter=0) and USB, then
the TRX is set on 14077.60 kHz in order to transmit the Mark frequency
of 14079.00 kHz. As the transceiver displays the frequency of the
(imaginary) carrier, then, in USB, the frequency of the audio Mark tone
(1400 Hz) must be added to the carrier frequency, for the actual Mark
frequency to be calculated. If on the other hand, the Mark frequency is
taken from a BBS list, the Mark tone frequency must be subtracted, in
order to find the correct frequency to tune the SSB transceiver to. If
the Offset value is defined as 1.4 kHz, the PTC-IIpro does the required
frequency correction for the Mark frequency automatically. It is thus
only necessary to give the wanted Mark frequency, and the correct offset
is automatically applied. For example, one can give the command
"Frequency 14079.0 \<Return>. The PTC-IIpro then sets the transceiver to
14077.6 kHz, which automatically, with Low tones and USB, gives the
correct transmit and receive frequency of 14079.0 kHz. Similarly with
LSB (only here the positive Space tone frequency would be chosen as
Offset) and with different tone pair frequencies.

## Parity

|                  |     |                          |
|------------------|-----|--------------------------|
| Default setting: | 0   |                          |
| Parameter:       | 0   | No parity bit (default). |
|                  | 1   | Odd parity               |
|                  | 2   | Even parity              |

Some transceiver types require a data format with parity bit for
communication on their remote control port. The **Parity** command
provides the possiblity of inserting a parity bit at the end of every
transferred byte on the trx control port. The **Parity** parameter only
affects the “Kenwood” data format (i.e. **TYpe** must be set to
“Kenwood”, see **TYpe** command in **trx:-**menu).

## Ptime

|                         |     |                                        |     |
|-------------------------|-----|----------------------------------------|-----|
| **Default setting: 50** |     |                                        |     |
|                         |     |                                        |     |
| Parameter:              | X   | 1... 1,000 pulse time in milliseconds. |     |

Sets the time (in Milliseconds) for the Up and Down keying pulse, that
can be initiated from the **Up** and **Down** commands (**trx:**-menu).
A **Ptime** value of 50 means that the respective switch in the
PTC-IIpro per impulse is closed for 50 ms and open for 50 ms.

## Quit

Leave the **trx:**-menu. The command prompt returns to its
*normal* form (**cmd:**). Identical to the [`DD`](#dd) command.

## RType

|                  |     |              |
|------------------|-----|--------------|
| Default setting: | 0   |              |
| Parameter:       | 0   | R&S XK-2000. |
|                  | 1   | R&S XK-852.  |

As default setting the PTC-IIpro supports the R&S model XK-2000. If
**RType** is set to 1 than the PTC-IIpro does support the R&S
transceiver model XK-852 for remote control. The VFO information readout
is currently *not* possible in this configuration.

This command is only active, if R&S as transceiver is selected with the
**TYpe** command.

## Scan

|                  |     |                                      |
|------------------|-----|--------------------------------------|
| Default setting: | 0   |                                      |
| Parameter:       | 0   | Stop scanner.                        |
|                  | 1   | Start scanner.                       |
|                  | C   | 1... 32, toggle channel scan status. |

The **Scan** command has two different functions: If, as argument, a 1
or 0 follows, then that means the scanner is switched on or off
respectively. This can be said to be the *main switch* for the scanner.

If, as argument, the word Channel (Minimum abbreviation: C) follows,
then the PTC requires a further argument the Channel number from the
frequency list (refer to the **Channel** command, chapter 13.1, page
201). Such a command switches the Scan status for the given channel
number. If the Channel 5 of the frequency list has not been defined as a
scanned channel up until now (Scan-Status: NO), then it may be declared
as such with the command Scan Ch 5 \<Return>. Through this command,
Channel 5 then obtains the Scan Status YES in the frequency list. A new
input of the command Scan Ch 5 \<Return> toggles the Scan status back to
NO, whereby Channel 5 would be skipped again on scanning.

If a beep is heard during frequency input or scanning, that’s not the PTC-IIpro, that’s the transceiver. Refer to the transceiver manual to switch off the beep for confirmation! |

## TImer

It is possible to define 10 timers (Timer number, length of time with
start and stop times). Each time "window" can be taken as an individual
timer, and thus in the following text, the words time "window" and timer
are synonymous.

There are various input formats possible:

**trx: TI** 1 4:00-5:00 \<**Return**\>

**trx: TI** 5 0700 0930 \<**Return**\>

**trx: TI** 2 23:00-3:00 \<**Return**\>.

The first argument is the number of the timer (0 to 9) that one wishes
to view or change. The second is the time period in hours and minutes
indicating the start and stop times. The "end" time can also be earlier
than the "start" time, which means the timer remains active through
midnight and into the next day.

It is essential that hours **and** minutes are given, i.e. at least
three places e.g. 300-400 for the period 3:00 to 4:00. The hyphen
between the start and stop times is optional and can be replaced with a
space. Leading zeros are also optional.

If the **TImer** command is given without arguments, then the PTC lists
the entire timer table. If only the timer number is given as argument,
then the PTC-IIpro shows the times defined for only this timer.

A single hyphen as a timer period erases the timer.E.g.:

**trx: TI** 1 - \<Return>

## Transfer

The command **Transfer** allows any character sequences to be sent via
the normal command interpreter of the PTC-IIpro to a connected
transceiver.

If the transceiver type has been set to KENWOOD, then ASCII characters
can directly follow the **Transfer** command, as KENWOOD transceivers
work directly with ASCII sequences. The Transfer sequence is closed with
\<Return>.

Commands the KENWOOD transceiver to switch to VFO A, and to return the
frequency of the VFO A.

**trx:** **T** FA; \<Return>

In the case of transceiver types SGC, YAESU, or ICOM, the transfer
sequences must be given in hexadecimal form.

Example:

Commands the SG 2000 to switch to the next operating mode ('step radio
mode' command).

**trx**: **T** F18A8A \<Return>

With the hexadecimal input spaces are ignored, and both upper and lower
case letters are allowed.

Transfer sequences may be easily stored as Fixtext or Fixfiles, for
individual control of transceivers.

## TYpe

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 4%" />
<col style="width: 24%" />
<col style="width: 47%" />
<col style="width: 9%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="3"><strong>Default setting: ICOM 1200 04</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td colspan="2"></td>
<td></td>
</tr>
<tr class="odd">
<td>Parameter:</td>
<td>X</td>
<td colspan="3"><p>CODAN, ICOM / KENWOOD / NMEA ICOM / R&amp;S / SGC / YAESU<br />
Baudrate (1200 – 115200 Bd)<br />
ICOM ID / VFO (A/B).</p>
<p>V24/TTL</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td colspan="2"></td>
<td></td>
</tr>
</tbody>
</table>

Enables the configuration of the PTC-IIpro TRX interface. There are up
to three arguments allowed.

The first argument indicates the transceiver, the following transceiver
are supported:

-   CODAN

-   ICOM

-   KENWOOD

-   NMEA ICOM

-   R&S Rhode & Schwarz

-   SGC

-   YAESU

The first letter is sufficient.

Then follows as the second argument, the baudrate. The PTC-IIpro
supports the following values: 1200, 1800, 2400, 3600, 4800, 7200, 9600,
12000, 14400, 16800, 19200, 28800, 38400, 57600, 76800, 115200.

For NMEA ICOM the given baudrate is ignored and is set to fixed 4800
baud.

For the third argument differs depending on the selected transceiver
type:

ICOM and NMEA ICOM

The PTC requires the ICOM equipment address number. The address can be
entered decimal (0 to 255) or hexadecimal ($0 to $FF). If entered
hexadecimal the $ has to be entered first, same for $F0 or $6C. Leading
zeros are suppressed.

In manuals you sometimes will find the following expression: e.g. 4Eh.
The small h indicates that the value is a hex number. (But smarty pants
would have recognized this before. The marking usually is not necessary,
because an E is never part of a decimal number!). The PTC-IIpro expects
the input $4E, i.e., the h is not given!

KENWOOD and YAESU

The VFO (A or B) that should be addressed by the PTC. With SGC and R&S
the third parameter is obsolete.

The following restrictions have to be cared of for R&S:

Data from the receiver is not reformatted by the PTC-IIpro, but simply
fed through directly to the terminal. For the **Frequency** command
without argument not the offset corrected frequency in kHz will be
displayed, but the original string from the transceiver.

The fourth argument defines if the tranceiver is controlled with TTL or
V24 levels. Refer to the transceivers manual to determine if it requires
TTL or V24 levels.

**If your transceiver has a 9-pole SUD-D connector for remote-control then it´s most propable that it uses V24 levels.**

CODAN

If the first parameter is “Codan”, the **TYpe** command only allows up
to 2 parameters. PTC-II modems with V24 support always work in mode
“V24” if **TYpe** is set to “Codan”. (Codan transceivers are V24
compatible.)

The function of the transfer command (trx t ...) for Codan transceivers
is identical to the function for Kenwood transceivers, i.e. ASCII
strings are simply transferred transparently.

ATTENTION:

In order that Codan NGT transceivers accept commands at a remote port
(“RS232 15-way” or “RS232 9-way”), the CICS command must be activated
(config menu, only after admin login).

Another, very important restriction must be considered: Only frequencies
that are predefined in a “channel” (within the transceiver) can be
chosen through the remote port. If an exact match cannot be found, the
channel with the next higher frequency is selected.

Commands for different transceivers:

**trx:** **TY** C 38400 \<Return>

**trx:** **TY** I 1200 4 \<Return>

**trx:** **TY** I 1200 $1C \<Return>

**trx:** **TY** K 4800 A \<Return>

**trx:** **TY** K 4800 A V \<Return>

**trx:** **TY** N 4800 2 \<Return>

**trx:** **TY** Y 9600 B \<Return>

**trx:** **TY** S 9600 \<Return>

If less that four arguments are given, the PTC-IIpro only changes the
explicitly given parameters. The command **TY** I 9600 \<Return> for
example sets only the type to ICOM and the baudrate to 9600 Bd. The
equipment address remains unchanged.

For the moment, with the TRX type NMEA ICOM only setting the frequency
is supported and also scanning. Frequency readback as well as *Transfer*
is not possible.


## Wait

|                         |     |                            |     |
|-------------------------|-----|----------------------------|-----|
| **Default setting: 10** |     |                            |     |
|                         |     |                            |     |
| Parameter:              | X   | 1... 240, time in seconds. |     |

Defines the time (in seconds) that the scanner waits after the end of a
link, before it switches to the next channel. The waiting time for the
re-synchronization of AMTOR is not influenced, as the phasing condition
in AMTOR ARQ is interpreted internally within the PTC as a continuous
connect, and the scanner therefore remains switched off.

## XGate

|                           |     |                      |     |
|---------------------------|-----|----------------------|-----|
| **Default setting: none** |     |                      |     |
|                           |     |                      |     |
| Parameter:                | X   | Channel number 1… 32 |     |
|                           | S   | Switch 0 or 1        |     |

**XGate** allows the Gate parameter to be set for a channel defined
within the TRX list.

Set Gate parameter of channel 5 to YES.

**trx:** **XG** 5 1 \<Return>

Set Gate parameter of channel 10 to NO.

**trx:** **XG** 10 0 \<Return>

If a channel has been defined new with the **Channel** command, the Gate
parameter is defaultly set to NO. If the PR->PACTOR gateway operation
shall be enabled, the **XGate** command has to be used onece for each
admitted channel.

## XScan

|                           |     |                      |     |
|---------------------------|-----|----------------------|-----|
| **Default setting: none** |     |                      |     |
|                           |     |                      |     |
| Parameter:                | X   | Channel number 1… 32 |     |
|                           | S   | Switch 0 or 1        |     |

The **XScan** command allows the Scan parameter to be set for a channel
defined within the TRX list.

As an alternative to the previous scan enabling possibility of two
arguments (e.g. S C 5), that *toggled* (switched) the scan function on
or off, the **XScan** command allows particularly channel scan
definition:

Set Scan parameter of channel 10 to NO.

**trx:** **XS** 10 0 \<Return>

Set Scan parameter of channel 4 to YES.

**trx:** **XS** 4 1 \<Return>

The **XScan** command is particularly useful in the
initialization/configuration file of the PTC-IIpro, because a new
defined state can be set without knowing the current state of the scan
parameter.

## YType

|                  |     |                                 |
|------------------|-----|---------------------------------|
| Default setting: | 0   |                                 |
| Parameter:       | 0   | YAESU Type FT-890               |
|                  | 1   | YAESU Type FT-990/FT-1000       |
|                  | 2   | YAESU Type FT-1000 MP           |
|                  | 3   | YAESU Type FT-100               |
|                  | 4   | YAESU Type FT-920               |
|                  | 5   | YAESU Type FT-847               |
|                  | 6   | YAESU Type FT-817/FT-857/FT-897 |

Specifies a special YAESU transceiver as sub-type to enable the
PTC-IIpro to readback the frequency from the transceiver. This command
is only effective, if a YAESU transceiver has been selected with the
`TYpe` command.

## External scan stop signal

The PTC-IIpro offers an external scan stop signal via its RS232
interface, on which TRX control programs in the larger mailbox systems
(e.g. WINLINK) can react. PIN 1 (CD) of the SUB-D-9 socket delivers a
negative level (approx. -8 to -10 V) as long as no scan stop conditions
are available, i.e. the external scanner may change the RX frequency.
PIN 1 (CD) of the SUB-D-9 socket delivers a positive level (approx. +8
to +10 V) as soon as a scan stop condition is detected, i.e. the
external scanner must hold the RX frequency constant.

IMPORTANT: After the link has been closed, or the reason for the scan
stop condition has ended, the scan-stop signal (positive CD level)
remains for a time which may be adjusted by the WAIT-TIME command
(**Wait** command) within the **trx:**-menu. The scan stop condition
reaction timing is that of the SYNCH-Status (status byte), and thus
reacts even to incomplete callsigns for a connect, and is thus extremely
fast.

## Special Features

### Direct Channel Selection for YAESU Transceivers

If as a TRX type YAESU is selected, the frequencies (also in the channel
and scanner list of the PTC-IIpro) smaller than 100 Hz (e.g. 0.099 kHz)
are interpreted as channel numbers. In this case not a frequency string
is sent to the TRX (for **F**-command or while scanning), but the
*Recall Memory* command, that means a channel preset in the TRX itself
is selected. This has the advantage that filter settings and sideband
information etc. are additionally stored in the TRX and therefore under
controll of the PTC-IIpro.

## Channel attributes

The desired channel attribute must be given when setting up the (scan)
channel list, in the comment field. Here for example it is possible to
define at which time the channel shall be *active* and which antenne
shall be choosen for the channel.

The way one goes about defining a channel command (in the **trx:**-menu)
is explained in the **Channel** command description (refer to section
13.1 on page 201). Here is a short example of how one could define
channel 1:

**trx:** **C** 1 3584.00 COMMENT ...\<Return>

In order that the channel attribute becomes operative, the scanner (**Scan** command) must be turned on and the appropriate channel must have its scan status set to ON (**XS** command).

The characters #: (hash and colon without a space) are used in order to
seperate the scan attribute from the "normal" comment in the channel
comment field. There can be multiple channel attributes after such a
character string. Multiple #: characters in a comment field are also
allowed. (This is required for example with Rhode and Schwarz specific
V0/1 channel attributes, which must always follow directly after its own
#: string.) The number of channel attributes is only limited by the
length of the comment field (52 characters). A space indicates the end
of a channel attribute chain.

What attributes are possible, follows in the next sections. For example
however here are some possible comment fields with channel attribute
chains.

**trx:** **C** 1 3584.00 #:a0t3t4 #:V0 \<Return>

**trx:** **C** 2 14079.00 DL6MAA #:A2T3P6 \<Return>

**trx:** **C** 3 3584.24 #:P3P2T6A1 DL3FCJ \<Return**\>**

**trx:** **C** 4 3584.00 #:t1 \<Return>

Either capitals or small letters may be used for the attribute.

### Preamp switching at R&S XK-2000 Transceiver

When frequency information is sent to the XK-2000 transceiver (be it
directly given with the **F**-command or automaticly by the channel
list), the PTC-IIpro automaticly switches on the transceiver´s
preamplifier on frequencies above 20 MHz and off at frequencies below 20
MHz. This automatism can be overridden by the channel attributes #:V0
and #:V1 in the comment field of the channel list. That means, when the
sequence #:V0 appears in the comment field, the preamplifier is always
disabled for the respective channel. With the sequence #:V1 it is always
enabled, independent on the frequency the channel specifies.

### Controlling the Antenna Switch

The *A* attribute serves to choose one from four possible antennas with
an external antenna relay. Format: *A* followed by a number in the range
0 to 3. The number defines which antenna should be activated. The output
is the open drain output for "A0" (Pin 8) and "A1" (Pin 6) of the 8 pin
radio port socket. The number 0 to 3 may be described in binary using
two bits: 0=00, 1=01, 2=10, 3=11. The righthand bit is the lowest value
bit and controls the A0 output. The left bit controls the A1 output. The
outputs are low resistance when the controlling bit is set to 1. This
all sounds relatively complex, but in practice is very easy.

| **Antenna number** | **A1 output conducts** | **A0 output conducts** |
|--------------------|------------------------|------------------------|
| 0                  | No                     | No                     |
| 1                  | No                     | Yes                    |
| 2                  | Yes                    | No                     |
| 3                  | Yes                    | Yes                    |

Table 13.1: Antenna Switch Conditions

Either a small 2 bit decoder circuit can be connected, or a maximum of
two relays may be connected DIRECTLY to the A0 and A1 outputs.

|     |                                                                                       |
|-----|---------------------------------------------------------------------------------------|
|     | The relay current must not exceed 100 mA, and the voltage should not exceed 15 volts! |

To switch between two antennas it is enough to connect an antenna relay
directly to the A1 output and supply the relay with (e.g.) 12 volts.
(don´t forget to connect GND). The Antenna attribute A0 keeps the relay
unenergised. Antenna attribute A1 energises the relay, (single
changeover contact) and switches a different antenna to the transceiver.

An antenna attribute of A0 to A3 can also appear as argument in a
frequency command, after the actual frequency input:

**trx:** **F** 14000 A0 \<Return>

This sets the transceiver to 14,000 MHz and also activates antenna 0.
This "feature" may be used with FFB scripts. The #: string is not for
direct input of the antenna attributes.

### Timer Attributes

The timer attributs T and P use the timer "windows" defined with the
**TImer** command. If a T attribute appears in a channel comment field,
then this channel would only be actually chosen in a scan operation,
when the actual time is within the time "window" defined by the T
attribute. Is this not the case the channel is skipped. E.g.:

One sets the timer 0 with the **TImer** command to a time span of 14:00
to 15:00 (Command **TI** 0 14:00-15:00 \<Enter>). The attribute #:T0
then limits the "active" time of a scan channel to 14:00 to 15:00. If no
further **TImer** attributes are given for this channel, then the
channel is only scanned between 14:00 and 15:00. At all other times, the
channel is skipped. Multiple, even overlapping **T** attributes are
possible, enabling a very flexible time control of various functions.
E.g.: #:T3T2T7P0.

Everything written for timer attribute **T** is also valid for timer
attribute **P**, except the **P** attribute concerns PRIORITIY times.
This means that during an active **P** time "window" the scanner stays
ONLY on this ONE channel, and does not scan! With the given example of
timer 0, an attribute #:**P**0 in a channel attribute would mean that
between 14:00 and 15:00 the system would sit on that channel. It is
therefore best to be careful with the **P** attribute, so that the
scanner is not mistakenly disabled. The **P** attribute also allows
cascading and overlapping. The **P** attribute is however very suitable
for use with timecontrolled NAVTEX reception.

If the **T** or **P** attributes are used for a non-defined **TImer**
number, then the PTC-IIpro just ignores them.

### Hex Attribute

|     |                                                                                                                                                                  |
|-----|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | We recommend that only experienced PTC users utilize the #:h attribute because improper usage can cause a general malfunction of the transceiver remote control. |

With the aid of the new channel attribute #:h arbitrary binary data can
be transferred to the transceiver through the TRX port. For example, a
different IF filter bandwidth can be assigned to each scan channel and
thus automatically be changed during scanning. Changing the bandwidth is
useful when narrow (“PACTOR-II only”) channels and wideband channels are
supported simultaneously.

The binary data must be appended directly to the h attribute in
hexa-decimal format. All hex nibbles (represented by characters
0-9/A-F/a-f) are grouped to bytes (MS nibble first) when the PTC
processes the hex string and then transmitted to the transceiver in
binary format.

If the number of nibbles is odd, the last nibble will be ignored.

Each character which cannot represent a hex nibble can be used as
“delimiter” (end of string indicator), e.g. the letters T and P. Hence,
channel attributes T (timer) and P (priority timer) can directly be
appended to the hex string without inserting an additional delimiter. If
an A attribute directly follows the hex string, a delimiter must be
inserted, e.g. a space character, see example.

> **trx:** **C** 1 3584.00 #:h0000c3540c a1 \<Return>

### Level Attribute

With the Level Attribute L2 (# :L2) a channel can be limited to
PACTOR-I/II operation only. This can be used if on the dedicated channel
PACTOR-III transmissions are not wanted e.g. because of bandwidth
issues.

> **trx:** **C** 2 14079.00 DL3FCJ #:L2 \<Return>

## TRX Control Channel on Hostmode

Virtual hostmode channel 253 serves as transparent data channel between
PC and TRX port. Arbitrary data can be exchanged between PC and
transceiver on channel 253. This enables, for example, direct
transceiver remote control from the PC side. There is one length
limitation: If more than 1000 bytes of data sent from the transceiver
are already buffered, the PTC does not accept more data until the buffer
is flushed (data fetched by the PC application).
