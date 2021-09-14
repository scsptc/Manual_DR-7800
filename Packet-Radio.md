# Packet Radio

The Packet Radio menu (**pac:**-menu) is activated with the command `PACket`. The command prompt takes the form **pac:** .

The following commands are available in the **pac:**-menu:
```
Aprs, Baud, CBell, CHeck, CMsg, Connect**, **CText**,
DIGIpeat, Disconnect, FRack, FSKFilter, FULLdup,
Help, Jhost1, KISS, MAXframe, MCon, MFIlter**,
Monitor, MStamp, MText, MYAlias, MYcall**, **MYMail,
PACLen, PErsist, Port, PRBox, Quit, RESptime,
RETry, Setchn, SLottime, TRACE, TXdelay,
TXLevel, Unproto, USers
```

[[_TOC_]]

All other (*normal*) commands are not available in the **pac:**-menu!
[`Quit`](#quit) or [`DD`](#dd) exit the **pac:**-menu.

The `PACket` command can be followed by a valid **pac:**-command as an argument. As with the other sub functions of the PTC-IIpro, it is also possible to pass through direct commands.

Switch off the Packet Radio listen – without using the **pac:**-menu
```
cmd: PAC M 0<Return>
```

## DAMA

The P4dragon DR-7800 in Packet Radio is full compatible with the DAMA (Demand
Assigned Multiple Access) standard. You easily recognize a DAMA-Digi
with a look to your monitor. The expression \[DAMA\] is added to the
header of the monitored packets, if the packet is received by a
DAMA-Digi. The DAMA mode needs not be activated by the user. The
PTC-IIpro automatically notices if you are working with a DAMA-Digi or
not and behaves respectively.

#### Robust HF-Packet

Robust HF Packet can only be operated with the DSP-Packet-Module-II
installed!

For the selection and configuration of the robust modulation for HF-PR
no special commands are necessary. The selection of the modulations type
follows the usual way with the **Baud** command in the **pac:** menu or
**%B** command in hostmode. The transmit level is taken from the
**PSKAmpl** (PACTOR PSK-amplitude, refer to chapter 6.74 on page 96 and
chapter 3.3.4 on page 17).

The center frequency of the audio signal is fixed to 1500 Hz. On the
receive side the same side band as the transmit side must be used. We
generally recommend USB.

With “Robust PR”-modulation selected the PTC assumes that a connection
will be via a HF Channel and adjusts a few parameters automatically.

> MAXFrame is automatically administrated;
>
> the value given by the user does not matter.

RETries is automatically doubled.

TXDelay is automatically divided by 4.

> The default setting 100 results in the usual 25 msec for Shortwave.

RESptime is automatically halved.

Following additional Parameters of the **Baud** command are available:

> Baud R300: During an X.25 connection automatic / self adaptive
> selection between 200 bit/sec and 600 bit/sec. UI-Packets (e.g. APRS)
> are transmitted in 200 bit/sec.
>
> Baud R600: During an X.25 connection automatic / self adaptive
> selection between 200 bit/sec and 600 bit/sec. UI-Packets (e.g. APRS)
> are transmitted in 600 bit/sec.

The arguments valid for **Baud** are also available in the same form for
the Hostmode command **%B**.

As the Robust-PR demodulator automaticly detects which modulation is
received, e.g. an APRS network can successively grow or be adapted to
the actual requiremens: If only a few users are present but the
distances are large then the longer but more robust modulated packets
can be used. In the opposite case, when many participients are present
but the average distances are smaller, then the faster/shorter packets
can be used.

#### Specialities of 300 Bd AFSK

300 Bd AFSK is normally used via an SSB transceiver, and usually
requires a tuning tolerance of +-30 Hz for satisfactory performance. The
DSP modem thus requires a tuning indicator for this mode. As the
PTC-IIpro only has three LEDs for each port (PTT, Connected, Carrier), a
two dimensional tuning display cannot be realised. Instead, the tuning
takes places by using the brightness of ONE LED. With a bit of practice,
one can obtain a tuning tolerance of +-10 Hz using this method.

The fine adjustment of a received signal takes place with the help of
the brightness of the PTT LED. Maximum brightness corresponding to the
best tuning. The tuning display via the PTT-LED is ONLY active when a
signal is recognised (i.e. initial tuning by ear until the "carrier" LED
lights). If ONLY the PTT-LED lights, then the transmitter is keyed
momentarily. The PTT LEDs then have their normal function. Note: The
"carrier" LED never lights whilst transmitting in full duplex operation,
even when a signal is received.

In practice, the tuning takes place by slowly turning the tuning knob
until the carrier LED lights. With an active carrier LED, further
careful tuning backward and forward is made until the PTT LED is at its
maximum brightness. The PR monitor can also be turned on as a further
tuning help, to see if valid data packets are being received.



## Port & Channel

The terms **Channel** and **Port** are very important for understanding
the functions of the Packet Radio options in the PTC-IIpro, and the
difference must be clearly understood.

**Port:** A port describes the hardware that is required to transmit and
receive the information. To use a port, a modem (PR-module) must be
installed, and the radio then connected to it. The PTC-IIpro contains
two possible ports, which correspond to the two available sockets on the
main board.

**Channel:** An AX.25 QSO may be found on a channel, the number of
channels setting the number of simultaneous links which can be made to
other stations.

The term *Multiport* describes commands that work separately for each
port. It is, for example, quite possible that a different **TXdelay**
may be required on each port. The port input for the multiport commands
is set directly before the parameter, separated with a colon (:), as in:

Command Port:Parameter

No spaces are allowed between the port input, the colon, and the
parameter!

As an example, the **TXdelay** command is being used:

Checking the **TXdelay** on port 1:

**pac:** **TX** 1: \<Return>

Checking the TXDelay on port 2:

**pac:** **TX** 2: \<Return>

Set the **TXdelay** on port 1 to 200 ms:

**pac:** **TX** 1:200 \<Return>

Set the **TXdelay** on port 2 to 90 ms:

**pac:** **TX** 2:90 \<Return>

The PTC-IIpro expects all time parameters in milliseconds!

If one works mainly on one particular port, after a while it becomes a
bit of a chore always having to give the port number, so it has been
made possible to define a standard port with the **Port** command, on
which the multiport commands work when port input is omitted, for
example, the following command sets the standard port to port 2:

**pac:** **Port** 2 \<Return>

Now all multiport commands without a special port number are valid for
port 2.

Checking the TXdelay (on port 2):

**pac:** **TX** \<Return>

Set the **TXdelay** to 150ms (on port 2):

**pac:** **TX** 150 \<Return>

## Modern Times

We hope you have already recognized the following warning:

The PTC-IIpro expects all time parameters in milliseconds!

The settings of the time parameters are very important for proper
Packet Radio operation! How long to wait for the confirmation
(**FRack**). How long is the time until it is checked if the other
station is still available (**CHeck**), etc. The function and most of
all the reliability of a Packet Radio connection depends on the time
parameters.

Because of this, check the initialization files of programs you use in
advance and very carefully. Often the added examples are designed for a
TNC 2. But the TNC 2 expects the time inputs in 10 ms steps, e.g. for a
TxDelay of 100 ms the value 10 has to be given for a TNC 2! But the
PTC-IIpro needs the value in milliseconds, that means 100.

If you use the initialization files without checking, it could happen,
that the very important timing data becomes 10 times too low.

The *most frequently* done mistakes according to wrong times are:

-   At connect establishment all attempts of the PTC-IIpro are
    transmitted in very short distances.

-   On a DAMA-Digi it could happen that suddenly the connection hangs.
    Digi and PTC-IIpro exchange RR frames only.

Please search for the following commands, **CHeck**, **FRack**,
**RESptime**, **SLottime** and **TXdelay**, in the initialization file
of your program and check the settings. In any case you have to adjust
the TX delay (**TXdelay**) due to your needs. It is possible to delete
all other commands within the initialization file or take the default
settings.

## KISS, SMACK and SRP for Packet Radio Operation

### KISS

KISS[4] means „Keep It Simple, Stupid“, which already implies the
simplicity of this interface protocol. In KISS mode, the PTC is degraded
to be a pure “modem” and its intelligence is limited to the physical
protocol level (modulation, demodulation). All higher protocol levels
(e.g. AX.25) are processed on the PC or whatever the KISS-master-system
is. Hence KISS just acts as simple transport medium between the higher
protocol levels and the physical “modem” level. The “modem” does not
have any knowledge any more of the higher protocol levels.

Because of this, KISS is not suitable for e.g. PACTOR: The
timing-critical PACTOR protocol cannot easily be implemented on a PC
with multitasking operating system and transported via a KISS interface
to the modem. **Via KISS only Packet Radio modems can be accessed.
PACTOR operation is not possible with KISS**. ATTENTION: As soon as KISS
mode is started, a running PACTOR connection is terminated immediately.

With the dual port PTC’s two KISS ports are available in parallel, with
the KISS addresses 0 and 1. (With SRP the Ring addresses are assigned
automatically, see below.)

A complete description of the KISS protocol exceeds the limits of this
update information and can be found in relevant literature or in the
Internet.

#### Activating KISS-mode, the commands KISS and @K

The KISS-Mode is activated with the commands **KISS** or alternatively
**@K** out of the normal command mode. This usually happens
automatically by the KISS-PC-software or a KISS capable controller (e.
g. TNC3). The KISS-mode is terminated by a system reset (power off/on
cycle), but can also be terminated by software with sending the decimal
byte sequence 192, 255, 192. The termination by sending the byte
sequence is usually done automatically by the software as well, and may
just once be configured correctly in the setup of the program.

### SMACK

SMACK[5] means “Stuttgart’s Modified Amateurradio-CRC-KISS“. It
represents a KISS mode with added checksum for data protection. SMACK
is supported by many KISS-capable systems. To switch into the
SMACK-mode, first the normal KISS mode needs to be entered. KISS-master
and KISS-modem then automatically negotiate if CRC protection (SMACK)
can be enabled.

A complete description of the SMACK protocol exceeds the limits of this
update information and can be found in relevant literature or in the
Internet.

### SRP

SRP[6] means “Serial Ring Protocol“ and has been developed by Jimy
Scherer, DL1GJI, for XNET, respecticely the TNC3. It is an extended
SMACK with the possibility to operate several “modems” together with one
SRP master in a Token-Ring. This provides the possibility of
<u>establishing a complex system of digipeaters</u>. With this, e.g. two
PTC-IIpro can be operated on one TNC3 (as master) in a ring (network).
The addresses (“ring adresses“) of the single ports are assigned
automatically. A dual ported modem (e.g. PTC-IIpro) receives 2 ring
addresses, e.g. 0 and 1, one address per port. The SRP master can access
both ports independently. With a ring of one TNC3 (without internal
modems) and two PTC-IIpro (as modems) four modem ports are available
(physically provided by the PTC-IIpro’s) for this digipeater. Two ports
can e.g. be used for „Robust Packet Radio“ on shortwave, one port can be
configured as 1200 baud access point and the fourth one as 9600 baud
access point.

To switch into the SRP mode, first the KISS mode has to be enabled. KISS
master and KISS modems automatically negotiate if SRP can be enabled.
All modems in a SRP-ring must be capable of SRP!

A complete description of the SRP protocol exceeds the limits of this
update information and can be found in relevant literature or in the
Internet.

## Commands

### Aprs

|                  |     |                                                                                     |
|------------------|-----|-------------------------------------------------------------------------------------|
| Default setting: | 0   |                                                                                     |
| Parameter:       | 0   | Off, APRS-beacon disabled                                                           |
|                  | 1   | On, APRS-beacon transmits GPS-position data if available                            |
|                  | 2   | FIX, APRS-beacon transmits fixed position data (adjustable with **Aprs Position**). |

In GPS mode the beacon only sends if the position data is not older than
20 minutes. If the GPS receiver fails, the beacon terminates the
transmission after 20 minutes.

The APRS beacon uses as sender call-sign the **MYcall** of the virtual channel 0. As long as this call-sign is not set the APRS-beacon cannot be activated. The **MYcall** of the virtual channel 0 is automatically set to the Pactor **MYcall** (after a **RESTart**), so that normally only a single **MYcall** entry is necessary to set all PACTOR as well as Packet-Radio/APRS **MYcall** to your own call-sign.

Additional to the normal nummeric parametes, the **APRS** command
provides several sub commands:

**COmment**, **PAth**, **POsition**, **SHort**, **SYmbol**, **TImer**

Also refer to chapter 5.9 on page 49.

#### APRS COmment

|                           |     |                             |     |
|---------------------------|-----|-----------------------------|-----|
| **Default setting: none** |     |                             |     |
| Parameter:                | \-  | or at maximum 40 characters |     |

Sets the comment text that is added to every APRS-datagram. E.g. a short
description of the system can be entered: “PTC-IIpro 20 W, Dipole”. The
comments maximum length is 40 characters. Longer comments will be
rejected with an error message. A minus character (-) as first Comment
character sets the Comment to “NONE”, and with this deletes the comment.

APRS comment should be as short as possible as the APRS-datagram will be
longer (sometimes much longer), which can lead to a (unnecessary) high
channel occupation.

#### APRS PAth

|                  |                     |                                                 |
|------------------|---------------------|-------------------------------------------------|
| Default setting: | APRS via RELAY WIDE |                                                 |
| Parameter:       |                     | APRS target call and at max. 8 digipeater calls |

Defines the AX.25 transmit path including target callsign and maximal 8
digitpeater callsigns, also with their respective SSID’s if available.
Examples:

**pac:** A PA CQ ia RELAY \<Return>

**pac:** A PA APRS RELAY WIDE GATE\<Return>

Between the target callsign and (optionally) the digitpeater list a “v”
or “via” can be inserted to increase readability.

A description of the operation of current APRS digipeater callsigns
exceeds the boundaries of this user manual. Appropriate information can
be found in relevant literature e.g. Internet. In case no exact
information of available digipeaters to hand, it is recommended to
select the first digitpeater “RELAY”

#### APRS POsition

|                  |      |                        |
|------------------|------|------------------------|
| Default setting: | NONE |                        |
| Parameter:       |      | XXXX.XXS/N YYYYY.YYW/E |

Allows the entry of the position for the “FIX” operation (Aprs 2, see
9.7.1). The position must be entered exactly in the correct format for
“Latitude Longitude”, which means degrees including leading zeroes,
directly followed by minutes with 2 decimal places and including the
direction. Any other format will be rejected with an error message.
Example:

**pac:** A PO 4810.30N 01030.25W \<Return>

#### APRS SHort

|                  |     |                 |
|------------------|-----|-----------------|
| Default setting: | 1   |                 |
| Parameter:       | 0   | Compression off |
|                  | 1   | Compression on  |

Activates (1) or deactivates (0) the compression of the position data in
the APRS datagram.

The compressed format has only advantages: Shorter datagrams, very
accurate, speed and direction can be included in the transfer. However
because some APRS programs cannot correctly interpret the compressed
format, the **SCS** firmware allows the compression to be switched off.
Also the uncompressed position data can be directly monitored as the
usual “Latitude Longitude format” is sent in plain text.

#### APRS SYmbol

|                  |            |              |
|------------------|------------|--------------|
| Default setting: | 15 \[Dot\] |              |
| Parameter:       |            | 1…94, a1…a94 |

Sets the graphic APRS symbol that an APRS receiving station should
display: e.g. a symbolic car in mobile service (Symbol 30). The symbol
numbers follow exactly the table in the APRS protocol version 1.0. The
complete protocol information is available on the Internet. Symbols from
the alternative table (“alternate table”) can be selected by prefixing
an “a” before the symbol number, e.g.: A SY al3 for “Home(HF)”.

If no symbol number is given as an argument the A SY command (normal
way) displays the actual parameter settings, however with a current
symbol additionally with a short description in square brackets. E.g.:
a13 \[Home (HF)\].

Here is a selection of current symbols or their numbers:

| 6:   | HF Gateway           |
|------|----------------------|
| 7:   | Small Aircraft       |
| 13:  | House QTH (VHF)      |
| a13: | House (HF)           |
| 15:  | Dot                  |
| 27:  | Campground           |
| 28:  | Motorcycle           |
| 30:  | Car                  |
| 47:  | Balloon              |
| 50:  | Recreational Vehicle |
| 53:  | Bus                  |
| 56:  | Helicopter           |
| 57:  | Yacht (sail boat)    |
| 65:  | Ambulance            |
| 66:  | Bicycle              |
| 70:  | Fire Truck           |
| 74   | Jeep                 |
| 75:  | Truck                |
| 83:  | Ship (Power boat)    |
| 86:  | Van                  |

#### APRS TImer

|                  |     |           |
|------------------|-----|-----------|
| Default setting: | 900 |           |
| Parameter:       | X   | 0, 1…7200 |

Sets the beacon interval in seconds. With the default setting 900, the
beacon transmits every 15 minutes, if position data is available and the
“global MYcall” is set on the virtual channel 0.

Parameter 0 activates the speed dependant automatic mode: The interval
is then calculated by the formula: Interval \[sec\] = 1800/GPS speed
(knots). With speeds above 180 knots the interval is limited to 10
seconds. With speeds below 1 knots the interval is limited to a maximum
of 1800 seconds.

The automatic can only work properly when the speed is contained in the
GPS datastream, which means that RMC data must be available from the
connected GPS receiver. If speed data is available the interval in
automatic mode is set to 900 seconds. With “FIX”-Position (Aprs 2, see
9.7.1) and automatic timer, the firmware sets the interval independent
of the speed data from the GPS receiver to 1800 seconds.

### Baud

Default setting: 1200|                                  
Parameter:                        | Rx  | Rx baud rate for the radio link. |     |
|                                   | Tx  | Tx baud rate for the radio link. |     |

Setting / checking the radio link baud rate.

Without a parameter, the **Baud** command shows the modem type, and the
baud rate set.

If a valid baud rate is given as a parameter, then this is set in the
Packet modem, valid baud rates are:

-   For the **SCS** AFSK-Modem: 1200 and 2400.

-   For the **SCS** FSK-Modem: 4800, 9600, 19200, 28800, 38400,
    57600, 115200.

-   For the **SCS** DSP-Modem-II: R300, R600, 300, 1200, 9600, 19200.

Some digipeater work with higher baudrate in direction to the user than
at the *Upload* side, e.g. Digi User 19k2 and User Digi 9k6.

The **Baud** command accepts two arguments, e.g.

**pac:** **Baud** 19200 9600 \<Return>

The first argument is the desired receiving baudrate, the second
argument is the desired transmission baudrate.

If only one argument is given, the PTC-IIpro uses this value for both,
TX baudrate and RX baudrate, e.g.

**pac:** **Baud** 9600 \<Return>

It is also possible to enter the port directly, e.g.

**pac:** **Baud** 2:19200 9600 \<Return>

The baudrate values for ports with the **SCS** DSP-Modem are stored in the Flash-ROM and remain valid also after a **RESTart** or a firmware update.

### CBell

|                  |     |                   |
|------------------|-----|-------------------|
| Default setting: | ON  |                   |
| Parameter:       | OFF | Connect bell off. |
|                  | ON  | Connect bell on.  |

Turns the connect bell on, or off. If the connect bell is turned on,
then every connect is signaled with an acoustic signal, and,
additionally, the PTC-IIpro sends a bell character (\<BEL>, ASCII 7) to
the terminal.

### CHeck

|                  |         |                                       |
|------------------|---------|---------------------------------------|
| Default setting: | 300,000 |                                       |
| Parameter:       | X       | 0... 3,000,000, time in milliseconds. |

The **CHeck** command sets the T3 or link activity timer. If nothing is
heard from the partner station during the time T3, then the link status
is queried.

### CMsg

|                  |     |                                                             |
|------------------|-----|-------------------------------------------------------------|
| Default setting: | 1   |                                                             |
| Parameter:       | 0   | Switch connect text off.                                    |
|                  | 1   | Switch connect text on.                                     |
|                  | 2   | Switch connect text on and evaluation of special functions. |

Enable or disable the connect text.

If **CMsg** is set to 2, the following sequences //B \<CR> and //Q \<CR>
are accepted additionally. The two sequences are noticed if they occur
at the beginning of a line and are closed directly with \<CR> or
\<Return>.

//B initiates the sysop-bell (duration about 14 seconds). After
receiving //Q the PTC initiates a disconnect.

The sysop-bell is set using the **BEll** command of the **cmd:**-menu.
To disable this function (refer to chapter 6.11, page 64)

### Connect

|                  |      |                                           |
|------------------|------|-------------------------------------------|
| Default setting: | none |                                           |
| Parameter:       |      | \<target-call> \[\<Digi1> \<Digi2>.....\] |

**Connect** sets up the AX.25 link. The connect can take place over both
ports in the PTC-IIpro, the required port being given directly before
the target callsign:

DL1ZAM connect via Port 1:

pac: C 1:DL1ZAM \<Return>

DL2FAK connect via Port 2

pac: C 2:DL2FAK \<Return>

If no special port is given, then the PTC-IIpro uses the default port
that has been set using the Port command. If the link takes place via
one or more digipeaters, then the list of digipeaters should be given
directly after the target callsign.

DL6MAA connect via DB0KFB

**pac:** C DL6MAA DB0KFB **\<Return>**

### CONStamp

|                  |     |                 |
|------------------|-----|-----------------|
| Default setting: | OFF |                 |
| Parameter:       | OFF | Time stamp off. |
|                  | ON  | Time stamp on.  |

Activates the display of time stamps on connect and disconnect messages.

### CONVerse

Manually activates the converse mode. This function is seldom needed, as
the PTC-IIpro automatically switches to the converse mode after a
successful link up.

Alternatively a **K** may be used, as abbreviation for **CONVerse**.

The Converse-mode can be terminated with the entry of

**\<ESC>** **CONVerse \<Return>**

or

**\<ESC>** **K \<Return>**

### CStatus

**CStatus** lists the condition of the channel, the link status.

###  CText

|                  |                  |                                    |
|------------------|------------------|------------------------------------|
| Default setting: | `>>> Welcome...` |                                    |
| Parameter:       |                  | String of 249 characters, maximum. |

The Connect text is transmitted when `CMsg`=1 and the PTC receives a
connect.

As the `CText` input uses the command interpreter, a special
convention for the \<CR>-­ character must be used. A \<CR> is
represented in the CTEXT string by a '#'.

\>\>\> Welcome to %'s PTC-IIpro DSP/QUICC System \<\<\<

To leave a MSG, please connect %-8 (PTC-Mailbox)!

The string above would be given as::

**pac:** **CT** \>\>\> Welcome to % 's PTC-IIpro DSP/QUICC System
\<\<\<## To leave a MSG, please connect %-8 (PTC-Mailbox)!
**\<**Return**\>**

The % character serves here as a dummy for the appropriate MYCALL of the
connected channel. The SSID of the MYCALL is ignored. For example if
DL1ZAM is the MYCALL, then the PTC-IIpro will give the following message
to the connected PR station:

\>\>\> Welcome to DL1ZAM's PTC-IIpro DSP/QUICC System \<\<\<

To leave a MSG, please connect DL1ZAM-8 (PTC-Mailbox)!

The Command interpreter buffer is 256 characters long. Commands plus
CTEXT argument should not contain more characters, otherwise the CTEXT
will be truncated.

### DIGIpeat

|                  |     |                       |
|------------------|-----|-----------------------|
| Default setting: | OFF |                       |
| Parameter:       | OFF | Digipeating disabled. |
|                  | ON  | Digipeating enabled.  |

Enable or disable digipeating using the own station.

### Disconnect

Ends an AX.25 link. If there is still data to be sent to the partner
station, then this data is transmitted first, before the disconnect is
carried out.

If the **Disconnect** command is given twice, one after the other, then
the link is broken immediately (corresponding to **DD** in PACTOR).

###  FRack

|                  |       |                                    |
|------------------|-------|------------------------------------|
| Default setting: | 5,000 |                                    |
| Parameter:       | X     | 1... 15,000, time in milliseconds. |

`FRack` sets the time in which a packet must be acknowledged. If the
PTC-IIpro sends a packet, and no acknowledgment is forthcoming within
the Frack time, then the modem queries if the information has
arrived.

The here given value of `FRack` is just the start value. The used
value is dynamicly recalculated during a connection using the formula:
Frack = 2\*SRTT\*X. Hereby X = RETRY if RETRY is \> 2, otherwise X = 1.
SRTT is the “Smoothed Round Trip Time”. X is generally 1 under link
establishment condition.

### FSKFilter

|                        |     |                                                       |
|------------------------|-----|-------------------------------------------------------|
| **Default setting: 0** |     |                                                       |
| Parameter:             | X   | 0... 15, Filter parameter for the **SCS** FSK modem.. |

This command is only valid in connection with **SCS** FSK modem!

The filter parameters provide a certain adaptation of the signal to the
frequency transfer characteristics of the transceiver. In most cases,
good results are already obtained using the default setting 0. If any
problems occur when connecting a certain digipeater, another value
should be tried.

The filter parameter operate in the transmission mode only!

### FUlldup

|                  |     |                       |
|------------------|-----|-----------------------|
| Default setting: | OFF |                       |
| Parameter:       | OFF | Full duplex disabled. |
|                  | ON  | Full duplex enabled.  |

Switches the port into full duplex operation, which allows the
simultaneous transmission and reception of data at a port.

Switches the full duplex on port 1 off:

**pac:** **FUlldup** 1: 0 \<Return>

Switches the full duplex on port 2 on:

**pac:** **FUlldup** 2: 1 \<Return>

Switches full duplex on the present port (default port) off.

**pac:** **FUlldup** 0 \<Return>

### Help

Lists all the Packet-Radio commands.

### JHOST

|                  |     |                                  |
|------------------|-----|----------------------------------|
| Default setting: | 0   |                                  |
| Parameter:       | 0   | Exits the hostmode.              |
|                  | 1   | Starts the hostmode.             |
|                  | 4   | Starts the CRC hostmode.         |
|                  | 5   | Starts the extended CRC hostmode |

Switching to the hostmode.

The command is used by the hostmode software to switch to the hostmode.
During *normal* operation within the terminal mode this command has no
function.

For furthermore information about the PTC-IIpro hostmode refer to
chapter 10, page 169.

It is strictly forbidden to enter the `JHOST` command in the initialization file of the hostmode programs! hostmode programs switch to the hostmode independently.

### KISS

The KISS-Mode is activated with the commands `KISS` or alternatively
`@K` out of the normal command mode. This usually happens
automatically by the KISS-PC-software or a KISS capable controller (e.
g. TNC3). The KISS-mode is terminated by a system reset (power off/on
cycle), but can also be terminated by software with sending the decimal
byte sequence 192, 255, 192. The termination by sending the byte
sequence is usually done automatically by the software as well, and may
just once be configured correctly in the setup of the program.

### MAXframe

|                        |     |                                           |     |
|------------------------|-----|-------------------------------------------|-----|
| **Default setting: 7** |     |                                           |     |
| Parameter:             | X   | 1... 7, number of unacknowledged packets. |     |

Maximum number of unacknowledged info packets (I Frames) in a link, i.e.
**MAXframe** defines the number of packets the PTC-IIpro transmits
continuously. The value should be reduced in case of bad links.

###  MCon

|                  |     |                     |
|------------------|-----|---------------------|
| Default setting: | 0   |                     |
| Parameter:       | X   | 0... 6, frame type. |

**MCon** sets whether the monitor should remain switched on in terminal
mode, even during a connect. Values greater than 0 switch on the
monitor. Values greater than 1 set the type of frames that are
displayed:

0 - Monitor switched off.
1 - Only UI-Frames
2 - Additionally I-Frames
3 - Additionally SABM- and DISC-Frames.
4 - Additionally UA- or DM-Frames
5 - Additionally RNR, RJ and FRMR
6 - Additionally Poll/Final Bit, PID and serial numbers

### MFIlter

|                  |     |                                    |
|------------------|-----|------------------------------------|
| Default setting: | 10  |                                    |
| Parameter:       | X   | 1... 128, max. 4 ASCII characters. |

This command removes the given characters from the data stream (maximum
4 arguments). The arguments must be given in decimal or hexadecimal
(prefixed with a $ character) ASCII values.

**Only** works in PR-terminal-mode, and can only be accessed in that
mode. (Does **not** operate in hostmode!)

Filters received and transmit characters. The default value is 10, i.e.
Linefeed. This has the effect that \<CR>/\<LF> in PR-Terminal-mode no
longer causes incompatibility with **DieBox** mailbox systems.

If the character is set to ASCII 128, then a special filter is
activated, which filters out all CONTROL characters (range 0-31) except
\<CR>, \<LF> and \<TAB>.

Set filter for \<LF> and \<BELL>

**pac:** **MF** 10 \<Return>.

### Monitor

|                  |     |                     |
|------------------|-----|---------------------|
| Default setting: | 0   |                     |
| Parameter:       | X   | 0... 6, frame type. |

Switch monitor on and off.

Values greater than 0 switch the monitor on, and values greater than 1
set which frame types will be monitored.

0 - Monitor switched off.
1 - Only UI-Frames
2 - Additionally I-Frames
3 - Additionally SABM- and DISC-Frames.
4 - Additionally UA- or DM-Frames
5 - Additionally RNR, RJ and FRMR
6 - Additionally Poll/Final Bit, PID and serial numbers

### MStamp

|                  |     |                 |
|------------------|-----|-----------------|
| Default setting: | OFF |                 |
| Parameter:       | OFF | Time stamp off. |
|                  | ON  | Time stamp on.  |

`MStamp` activates the time stamp for packets that are displayed via
the monitor.

### MText

|                                         |     |                                    |     |
|-----------------------------------------|-----|------------------------------------|-----|
| **Default setting: '>\>\> Welcome...'** |     |                                    |     |
| Parameter:                              |     | String of 249 characters, maximum. |     |

Identical to the **CText**-command in the **pac:**-menu, however sets
the connect-text for the PR-mailbox.

The default text is as follows:

\>\>\> Welcome to %'s PTC-IIpro Mailbox \<\<\<

Please type H for help.

The **MText** input is done via the normal command interpreter, so a
convention for the \<CR> character has to be used: The \<CR> is
represented within the **MText** string by #.

This would be input like:

**pac:** **MT** \>\>\> Welcome to %'s PTC-IIpro Mailbox \<\<\<## Please
type H for help. **\<Return>**

The same as in **CText**, the % character serves here as a dummy for the
appropriate MYCALL, independent if it is a BBS callsign or the normal
MYCALL. The SSID of the MYCALL is ignored.

For example if DL1ZAM-8 is the BBS-MYCALL, then the PTC-IIpro will give
the following message:

\>\>\> Welcome to DL1ZAM's PTC-IIpro Mailbox \<\<\<

Please type H for help.

The **MText** always follows the message from the automatic *mail
notifier*, i.e. "\*\*\* NO new MSG for you" or "\*\*\* 2 new MSGs for
you" or similar.

The **MText** cannot be turned off.

### MYAlias

|                  |        |                               |
|------------------|--------|-------------------------------|
| Default setting: | SCSPTC |                               |
| Parameter:       | CALL   | Alternative station callsign. |

`MYAlias` is handled as `MYcall` for incoming connects, and can also
be used as an alternative station callsign.

If the modem is called by the `MYAlias` callsign as a digipeater,
he works as a cross port digipeater, i.e., packets received at port 1
are send out at port 2 and vice versa. The kind of modem at the relevant
port is not important, because of this cross digipeating from 1200 baud
to 9600 baud and vice versa is possible.

The default of the `MYAlias` callsign is the PACTOR MYCALL entered
first of all., but gets the SSID 15. If for example the global MYCALL on
the PACTOR is set to DL6MAA, the PTC-IIpro sets the MYAlias to
DL6MAA-15. This default setting can be changed at any time using the
`MYAlias` command of the **pac:**-menu.

### MYcall

|                  |        |                      |
|------------------|--------|----------------------|
| Default setting: | SCSPTC |                      |
| Parameter:       | CALL   | Callsign of the PTC. |

Callsign for the Packet Radio mode.

For each channel an own callsign can be defined temporarily. After a disconnect the callsign will always be taken from channel 0 again.

After switching on the PTC-IIpro the firmware checks if a valid callsign
is written in the PACTOR-MYCALL. In this case (i.e. no \*SCSPTC\*
defined as PACTOR-MYCALL), the PTC-IIpro copies the PACTOR-MYCALL to all
PR channels which are still having SCSPTC as MYCALL, and overwrite the
SCSPTC with the valid mycall. If the **MYcall** command is executed on
the PACTOR side with a valid callsign as an argument, the PTC-IIpro also
checks all PR channels for SCSPTC, and if necessary the new defined
PACTOR-MYCALL is taken over to the PR channels replacing the SCSPTC
setting.

### MYMail

|                               |      |     |                             |     |
|-------------------------------|------|-----|-----------------------------|-----|
| **Default setting: MYCALL-8** |      |     |                             |     |
| Parameter:                    | CALL |     | Callsign of the PR mailbox. |     |

Identical to the **MYcall** command in the **pac:**-menu, however sets
the *Mycall* of the PTC-IIpro PR-mailbox (BBS-MYCALL). The BBS call is
set automatically to MYCALL-8, either at the first start (when the
*Flash-Call* in the BIOS has been defined), or when ones own
PACTOR-MYCALL has been set. If, for example, DL1ZAM is given as the
first PACTOR-MYCALL then the PR-mailbox can be connected with the call
DL1ZAM-8.

### PACLen

|                  |     |                                |
|------------------|-----|--------------------------------|
| Default setting: | 255 |                                |
| Parameter:       | X   | 1… 255, transmit packet length |

Sets the maximum PR transmit packet length, when the PTC is in Terminal
mode. (In hostmode is the **PAClen** value not used, as the hostmode
program itself defines the packet length). Packet lengths smaller than
255 are only useful if the link to the distant station has a lot of
errors. The PTC-IIpro sends in terminal-mode a packet immediately if a
\<CR> is received, which is the usual *sendpack-character*.

### PErsist

|                  |     |                        |
|------------------|-----|------------------------|
| Default setting: | 64  |                        |
| Parameter:       | X   | 0... 255, persistence. |

The persistence value sets the probability that a packet is transmitted,
after the radio channel is acknowledged as free.

Persistence on port 1 set to 32:

**pac:** **PE** 1:32 \<Return>

### Port

|                                                     |     |                      |     |
|-----------------------------------------------------|-----|----------------------|-----|
| **Default setting: depending on installed Modems.** |     |                      |     |
| Parameter:                                          | X   | 1... 2, defaut port. |     |

The default port is set here, the **Port** command has influence to the
following commands: **Baud**, **Connect**, **FSKFilter**, **FUlldup**,
**PErsist**, **SLottime** and **TXdelay**.

###  PRBox

|                        |     |                                   |     |
|------------------------|-----|-----------------------------------|-----|
| **Default setting: 1** |     |                                   |     |
| Parameter:             | 0   | PR mailbox switched off.          |     |
|                        | 1   | PR mailbox switched on.           |     |
|                        | 2   | PR mailbox, only private messages |     |

Enables the PR-mailbox to be switched on or off, or the mailbox to be
configured as a *maildrop*. (*Maildrop* means that only data addressed
to the PTC MYCALL will be accepted by the mailbox. This is a legal
requirement in many countries, as an open BBS may only be operated by
especially licensed stations). The function is similar to the **Box**
command of the PACTOR level (**cmd:**-prompt). The **Box** command
relates to PACTOR/AMTOR only. The **PRBox** command to Packet-Radio
only.

### Quit

Leaves the **pac:**-menu. The command prompt returns to its
*normal* form (**cmd:**).

### RESptime

|                  |     |                                  |
|------------------|-----|----------------------------------|
| Default setting: | 500 |                                  |
| Parameter:       | X   | 1... 30,000, response time delay |

Sets the value for the AX.25 timer-2 (T2) in milliseconds.

After receiving a packet the PTC-IIpro waits the time T2 to check if
another packets follow. If so, all packets can be confirmed with only
one control packet.

### REtry

|                  |     |                              |
|------------------|-----|------------------------------|
| Default setting: | 10  |                              |
| Parameter:       | X   | 0... 255, number of repeats. |

**REtry** sets the maximum number of repeats, and, if this value is
exceeded, then the PTC-IIpro gives out the message:

LINK FAILURE with \<call>

### Setchn

|                  |     |                   |
|------------------|-----|-------------------|
| Default setting: | 1   |                   |
| Parameter:       | X   | 0... 31, channel. |

Switches between the various channels.

The modem provides 32 logical channels to the user, numbered from 0
to 31. The `Setchn` command defines the channel to be written on. A
special status has the channel 0. Channel 0 is the channel to transmit
not protocolled messages, as CQ calls or beacon.

Connect attempts can be started from each channel between 1 to 31, as
long the channel is not occupied. Received connects will always be
assigned to the first free channel, provided that the number of maximal
permitted simultaneous connects (`USers` command) is not exceeded.

### SLottime

|                  |     |                                         |
|------------------|-----|-----------------------------------------|
| Default setting: | 100 |                                         |
| Parameter:       | X   | 1... 30,000, slot time in milliseconds. |

Sets the slot time for the transmitter control.

The modem can transmit at particular times only. `SLottime`
defines the period between these times.

### TRACE

|                          |     |                          |     |
|--------------------------|-----|--------------------------|-----|
| **Default setting: OFF** |     |                          |     |
| Parameter:               | OFF | Trace mode switched off. |     |
|                          | ON  | Trace mode switched on.  |     |

In the terminal mode the PTC-IIpro provides the so called Trace mode for
Packet-Radio. The **TRACE** command activates or deactivates a special
display mode for all frames shown in the monitor channel. The PTC-IIpro
sends the trace mode data as Hex-dump, as ASCII or as *shifted* ASCII in
three columns. Finally the normal monitor packet is displayed
additionally. As a horizontal separation between the frames a line out
of = characters is given. Primarily this function is used for testing.
In the WA8DED host mode this function is not available!

### TXdelay

|                  |     |                                       |
|------------------|-----|---------------------------------------|
| Default setting: | 100 |                                       |
| Parameter:       | X   | 0... 30,000, TxDelay in milliseconds. |

Sets the time between keying the PTT and the initial transmission of
data.

Setting TxDelay of Port 1 to 50 ms.

**pac:** **TXD** 1:50 \<Return>

Setting TxDelay of Port 2 to 200 ms.

**pac:** **TXD** 2:200 \<Return>

### TXLevel

|                  |              |                                                 |
|------------------|--------------|-------------------------------------------------|
| Default setting: | A 300, F 800 |                                                 |
| Parameter 1      | A            | Tx-level for AFSK = 300/1k2 Baud                |
|                  | F            | Tx-level for FSK = 9k6/19k2 Baud                |
| Parameter 2:     | X            | 20... 3000, Tx-level in millivolts (peak-peak). |

The audio output level of the **SCS**-DSP-PR-module is set with the
command **TXLevel** (certainly only when a DSP-PR-module is installed!).
The output level is set for the FSK (9600 and 19200 Baud) and AFSK modes
(300 and 1200 Baud) independently.

Setting TxLevel for 300 and 1200 Baud to 100 mV:

**pac:** **TXL** A 100 \<Return>

Setting TxLevel of the module on Port 2 to 500 mV:

**pac:** **TXL** 2:A 500 \<Return>

Setting TxLevel for 9600 and 19200 Baud to 500 mV:

**pac:** **TXL** F 100 \<Return>

Setting TxLevel of the module on Port 1 to 3000 mV (9600 and 19200
Baud):

**pac:** **TXL** 1:F 3000 \<Return>

Without entry of a second parameter the actual values can be read out.

Reading out the TxLevel for 300 and 1200 Baud:

**pac:** **TXL** A \<Return>

Reading out the TxLevel for 9600 and 19200 Baud:

**pac:** **TXL** F \<Return>

Certainly, also here the port can be specified.

**pac:** **TXL** 1:F \<Return>

**pac:** **TXL** 2:A \<Return>

Without any parameter given, the entry of **TXLevel** displays both
amplitude settings.

The baudrate values for ports with the **SCS** DSP-Modem are stored in the Flash-ROM and remain valid also after a **RESTart** or a firmware update.

### Unproto.

|                  |      |                      |
|------------------|------|----------------------|
| Default setting: | CQ   |                      |
| Parameter:       | Call | Callsign for Unproto |

**Unproto** sets the target callsign for the Unproto operation.

To start an Unproto transmission, just enter the Converse mode with
**K**, and, everything that is then typed, and ends with \<Return> is
transmitted by the PTC-IIpro.

\<Esc> returns the **pac:**-prompt, the entry of **K** then ending the
Converse mode.

### USers

|                  |    |                           |
|------------------|----|---------------------------|
| Default setting: | 4  |                           |
| Parameter:       | X  | 0... 31, number of users. |

Limits the number of channels available for remote users.

`USers` 5 limits the number of connects from outside to five, so if
the PTC is presently connected to by 5 stations, and a further station
attempts to connect, this connect request will be refused.

The `USers` command allows any incoming PR-connect to be transferred
to the PTC-IIpro PR-mailbox, but only if `USers` has to be set to 0.
This will allow for example, that on exiting the terminal program, (e.g.
automatic de-initialization with `Y0` in **GP**) the PTC-IIpro can be
brought to a condition where a connect using the *normal MYCALL* (i.e.
without the -8) will be transferred to the mailbox. This is useful, as
many potential users would use the *normal MYCALL* to connect to the
PTC-IIpro.

If the terminal is *off-line*, and the configuration is correct,
(`USers 0` or `Y0`) then all calls, irrespective of if they are the
*normal MYCALL*, the *MYALIAS*, or the *BBS-MYCALL*, will be transferred
to the PTC-mailbox.

The `USers`-command has no effect on self initiated connects, the
number of channels is not limited for the user. It is thus possible,
with `Users` = 0 to initiate up to 31 PR-connects in parallel!
