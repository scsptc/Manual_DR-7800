# Hostmode

The hostmode was developed from **WA8DED** in 1986 in as an alternative
firmware for TARP-TNC’s to enhance the communication between computer
(the host) and the connected TNC.

In the terminal mode the TNC is allowed to transfer data at any time to
the computer, but in the hostmode the TNC is only allowed to send data
if being polled by the computer. This has the advantage that the
computer definitely knows when the TNC sends data, i.e., the computer
controls the data transfer between computer and TNC. This ensures that
the data of each channel will be displayed in the correct window of the
hostmode program.

Because of this complete control of data exchange between computer and
TNC and because of the hostmode structure, a transfer of binary files is
possible without problems, and this on several channels at the same
time. Special encoders like UUENCODE, 7PLUS, YAPP are not necessary
anymore.

As there was no source code for the **WA8DED** firmware available, some
German radio amateur (from the NORD>\<LINK) decided to program an own
firmware. The ideal was the WA8DED firmware inclusive hostmode for best
compatibility to existing programs. So the NORD>\<LINK-**TheFimware**
was created, short form **TF**. Already from the beginning the source
code of **TheFirmware** was available for anyone, so that radio amateurs
could modify and improve it. Especially for new ideas like extended
hostmode and AX.25 protocol expansions like as DAMA **TheFirmware** was
and is the *basis for development*.

Because of these advantages, the wide distribution of **TF** and the
always more perfected hostmode programs, the hostmode became the
standard for TNC controlling.

But the disadvantages of the hostmode shall be mentioned too. The
hostmode progam has to poll the TNC continuously, if data is available
or not. That means the program has to poll in a turn each channel after
the other for data. This causes a delay until the data becomes displayed
on the monitor. But the polling is reduced using the extended hostmode
(refer to chapter 10.5, page 185). Another disadvantage is the high
*load* at the serial interface caused by multiple transfers of data,
i.e., if the monitor is switched on the receive-data are transmitted
once on the monitor channel and once on the receiving channel to the
computer. This disadvantage is visible especially when using high speed
packet (9k6 or higher).

## The P4dragon DR-7800 hostmode

The hostmode implemented in the P4dragon DR-7800 is largely compatible to the
WA8DED hostmode, as found in virtually all TNC´s, but is only used when
the modem is connected to a computer, and controlled by a special
hostmode program.

After starting the **WA8DED** hostmode the modem displays in the
monitor channel a short startup message with version number of the
firmware and Bootloader. Additionally all installed modems and
the baud rates being set are displayed:
```

************************************
* SCS P4dragon                     *
* Firmware Version 2.00    Level 4 *
* Bootloader Version 1.00          *
* (C) SCS GmbH & Co. KG 1999-2014  *
************************************

Port 1: SCS - DSP MULTI MODEM at 9600 baud.
Port 2: NO MODEM at 0 baud.

```

Please refer for more information to chapter 5.14, page 57 and the
explanations according to the **TNC** command, chapter 6.96, page 108.

## Modern Times

The settings of the time parameters are very important for proper
Packet-Radio operation! How long to wait for the confirmation (`F`).
How long is the time until it is checked if the other station is still
available (`@T3`), etc. The function and most of all the reliability
of a Packet-Radio connection depends on the time parameters.

Because of this, check the initialization files of programs you use in
advance and very carefully. Often the added examples are designed for a
TNC 2. But the TNC 2 expects the time inputs in 10 ms steps, e.g. for a
TxDelay of 100 ms the value 10 has to be given for a TNC 2! But the
P needs the value in milliseconds, that means 100.

If you use the initialization files without checking, it could happen,
that the very important timing data becomes 10 times too low.

The *most frequently* done mistakes according to wrong times are:

- At connect establishment all attempts of the PTC-IIpro are
  transmitted in very short distances.

- On a DAMA-Digi it could happen that suddenly the connection hangs.
  Digi and modem exchange RR frames only.

Please search for the following commands, `F`, `T`, `W`, `@T2`
and `@T3`, in the initialization file of your program and check the
settings. In any case you have to adjust the TX delay (command `T`)
due to your needs. It is possible to remove all other commands within
the initialization file or take the default settings.

## DAMA

The P4dragon DR-7800 in Packet-Radio is full compatible with the DAMA (Demand
Assigned Multiple Access) standard. You easily recognize a DAMA-Digi
with a look to your monitor. The expression \[DAMA\] is added to the
header of the monitored packets, if the packet is received by a
DAMA-Digi. The DAMA mode needs not be activated by the user. The
modem automatically notices if you are working with a DAMA-Digi or
not and behaves respectively.

## Commands

The commands available in the hostmode are totally different to the
commands in the terminal mode. Table 10.1 compares the commands between
the terminal mode and the hostmode.

| **Terminal Mode** | **Hostmode** |
|-------------------|--------------|
| Baud              | %B           |
| CHeck             | @T3          |
| CMsg              | U            |
| Connect           | C            |
| CONStamp          | K            |
| CText             | U            |
| Disconnect        | D            |
| FRack             | F            |
| FSKFilter         | %F           |
| FUlldup           | @D           |
| KISS              | @K           |
| MAXframe          | O            |
| MCon              | M            |
| Monitor           | M            |
| MStamp            | K            |
| MYcall            | I            |
| PErsist           | P            |
| Port              | %P           |
| RESptime          | @T2          |
| REtry             | N            |
| SLottime          | W            |
| TXdelay           | T            |
| Users             | Y            |


In the following chapters the hostmode commands are described:

### C

**Default setting: none**  
Parameter: \<target call> \[\<Digi1> \<Digi2>…\]

Connect establishes a AX.25 link. The connect can take place over both
ports in the PTC-IIpro, the required port being given directly before
the target callsign:

**C** DL1ZAM - connects with DL1ZAM

If the link takes place via one or more digipeaters, then the list of
digipeaters should be given directly after the target callsign.

**C** DL6MAA DB0FKB - connects to DL6MAA via DB0KFB

A Connect command on channel 0 sets the path for the Unproto
transmission.

### D

Disconnects an AX.25 link.

If there is still data to be sent to the partner station, this data is
transmitted first, then the disconnect is carried out.

If the Disconnect command is given twice, one after the other, then the
link is broken immediately (corresponding to `DD` in PACTOR).

### F

|                  |       |                                 |
|------------------|-------|---------------------------------|
| Default setting: | 5,000 |                                 |
| Parameter:       | X     | 1… 15,000, time in milliseconds |

Frack-Timer (T1).

Frack sets the time in which a packet must be acknowledged. If the
modem sends a packet, and no acknowledgment is forthcoming within
the Frack time, the modem then queries whether the information has
arrived.

### G

`G` (Get) is a special hostmode command, and is used to get
information about the various hostmode channels.

This command is only used by the hostmode program.
The user cannot enter this command.

### I

|                  |        |                  |     |
|------------------|--------|------------------|-----|
| Default setting: | SCSPTC |                  |     |
| Parameter:       | CAll   | Station callsign |     |

Sets the station callsign, which can be individually set for each
channel. The callsign from channel 0 being used after a disconnect

###  JHOST

|                  |     |                             |
|------------------|-----|-----------------------------|
| Default setting: | 0   |                             |
| Parameter:       | 0   | Exit hostmode               |
|                  | 1   | Start hostmode              |
|                  | 4   | Start CRC hostmode          |
|                  | 5   | Start extended CRC hostmode |

Switches to the hostmode or exits.

This command is used by the hostmode software in order to switch to
hostmode. The command has no meaning for the *normal* operation in
terminal mode.

### K

|                  |     |                                                 |
|------------------|-----|-------------------------------------------------|
| Default setting: | 0   |                                                 |
| Parameter:       | 0   | Time stamp switched off.                        |
|                  | 1   | Time stamp for connect and disconnect messages. |
|                  | 2   | Time stamp also in monitor.                     |

Switches the time stamp display on and off.

### L

|                  |      |                |
|------------------|------|----------------|
| Default setting: | none |                |
| Parameter:       | X    | 0… 31, channel |

Requests the link-status, returns a list of the channel condition.

This command is only used by the hostmode program.
The user cannot enter this command.

### M

|                  |     |                              |
|------------------|-----|------------------------------|
| Default setting: | N   |                              |
| Parameter:       | N   | Monitor switched off.        |
|                  | I   | Info frames                  |
|                  | U   | Unproto transmissions.       |
|                  | S   | Control packets              |
|                  | C   | Monitor also while connected |

`M` sets which frame types will be displayed in the monitor.

###  N

|                  |     |                            |
|------------------|-----|----------------------------|
| Default setting: | 10  |                            |
| Parameter:       | X   | 0… 255, number of repeats. |

Sets the maximum number of repeats. If this value is exceeded
the modem gives out the message:

`LINK FAILURE with <call>`

### O

|                  |     |                                        |
|------------------|-----|----------------------------------------|
| Default setting: | 7   |                                        |
| Parameter:       | 1   | 1… 7, Number of unacknowledged packets |

Maximum number of unacknowledged info packets (I frames) in a link.
Maxframe also sets how many packets the PTC-IIpro transmits together.
The value should be reduced for bad links.

### P

|                  |     |                     |
|------------------|-----|---------------------|
| Default setting: | 64  |                     |
| Parameter:       | X   | 0… 255, persistance |

The persistence value sets the probability that a packet is transmitted,
after the radio channel is acknowledged as free.

### PS

When a GPS receiver is connected to the modem then with the `PS`
command the position data can be read out. In contrast to the
[`POSition`](#Commands.md#position) command in the **cmd:**-menu the output always has NMEA
format. The NMEA compatible string usually looks like:

`$GPRMC,212234,A,5005.432,N,00845.974,E,000.0,360.0,190201,000.1,E\*7B`

### T

|                  |     |                                       |
|------------------|-----|---------------------------------------|
| Default setting: | 100 |                                       |
| Parameter:       | X   | 0... 30,000, TxDelay in milliseconds. |

Sets the time between keying the PTT and the initial transmission of
data.

`T 50` sets the TxDelay to 50 ms

### U

|                  |     |                                                           |
|------------------|-----|-----------------------------------------------------------|
| Default setting: | 0   |                                                           |
| Parameter:       | 0   | Switch connect text off.                                  |
|                  | 1   | Switch connect text on.                                   |
|                  | 2   | Switch connect text on and analysis of special functions. |

Enable or disable the connect text.

**U** defines the connect text.

**U** 1 Here is the PTC-IIpro – The PTC-IIpro switches on the connect
text and the text will be “Here is the PTC-IIpro ”.

**U** 1 – asks for the connect text

**U** 0 – switches off the connect text

If **U** is set to 2, the sequences //B \<CR> and //Q\<CR> are accepted
additionally. The two sequences are recognized if they occur at the
beginning of a line and are closed directly with \<CR> or \<Return>.

//B initiates the sysop-bell (duration about 14 seconds). After
receiving //Q the PTC initiates a disconnect.

The sysop-bell is set using the **BEll** command of the **cmd:**-menu
(refer to chapter 6.11, page 64)

### V

Outputs a longer version string.

### W

|                  |     |                                         |
|------------------|-----|-----------------------------------------|
| Default setting: | 100 |                                         |
| Parameter:       | X   | 1... 30,000, slot time in milliseconds. |

Defines the slot time for the transmitter control.

The modem can transmit at particular times only. `W` (Slottime)
defines the period between these times.

### Y

|                  |     |                           |
|------------------|-----|---------------------------|
| Default setting: | 4   |                           |
| Parameter:       | X   | 0... 31, number of users. |

Limits the number of channels available for remote users.

`Y` 5 limits the number of connects from outside to five, so if the
PTC is presently connected to by 5 stations, and a further station
attempts to connect, this connect request will be refused.

The `Y` command allows any incoming PR-connect to be transferred to
the PTC-IIpro PR-mailbox, but only if `Y` has to be set to 0. This
will allow for example, that on exiting the terminal program, (e.g.
automatic de-initialization with **Y**0 in **GP**) the PTC-IIpro can be
brought to a condition where a connect using the *normal MYCALL* (i.e.
without the -8) will be transferred to the mailbox. This is useful, as
many potential users would use the *normal MYCALL* to connect to the
PTC-IIpro. If the terminal is *off-line*, and the configuration is
correct, (**Y**0) then all calls, irrespective of if they are the
*normal MYCALL*, the *MYALIAS*, or the *BBS-MYCALL*, will be transferred
to the PTC-mailbox.

The `Y`-command has no effect on self initiated connects, the number
of channels is not limited for the user. It is thus possible, with `Y`
= 0 to initiate up to 31 PR-connects in parallel!

### @B

Shows the free buffer available.

This command is virtually only used from the hostmode program to find
out how much memory is still free in the PTC-IIpro.

This command is only used by the hostmode program. The user cannot enter
this command.

### @D

**Default setting: 0**  
Parameter: 0 Full duplex disabled.
 1  Full duplex enabled.

Switches the port into full duplex operation, which allows the
simultaneous transmission and reception of data at a port.

**@D** 1:0 \<Return> Switches the full duplex on port 1 off

**@D** 2:1 \<Return> Switches the full duplex on port 2 on

**@D** 0 \<Return> Switches full duplex on the present port (default
port) off

### @F

The hostmode command @F allows to setup FAX reception under hostmode
control. Receveiving FAX images through the hostmode interface means
that the data transfer between modem and PC is highly buffered and
error-corrected (CRC hostmode). Thus “Skew” or“ “jumps” within FAX
images caused by data loss on the interface side (high PC operating
system latency, etc.) can be completely avoided. Besides that, the @F
command eases incorporating FAX reception to application software that
mainly builds on the hostmode.

|                  |      |                                                                                       |
|------------------|------|---------------------------------------------------------------------------------------|
| Default setting: | none |                                                                                       |
| Parameter:       | @F   | (no parameter) Clears the FAX data buffer, see below.                                 |
|                  | @F0  | Disables hostmode FAX reception and switches back to normal PACTOR Standby operation. |
|                  | @F1  | Activates hostmode FAX reception in FM-FAX, sampling rate = baudrate/32.              |
|                  | @F17 | Activates hostmode FAX reception in FM-FAX, sampling rate = baudrate/16.              |
|                  | @F2  | Activates hostmode FAX reception in AM-FAX, sampling rate = baudrate/32.              |
|                  | @F18 | Activates hostmode FAX reception in AM-FAX, sampling rate = baudrate/16.              |

If hostmode fax reception is activated, 8 bit per sample (grey scale)
FAX data is available on hostmode channel 252. The data field length of
the hostmode packets on channel 252 is always 256. The sampling rate
(number of 8 bit samples, i.e. pixels, per second) is calculated as
baudrate on the serial user interface (COM port) divided by 32 or 16.
The baudrate on the serial user interface of the modem should be chosen
as high as possible (higher than 57600 Bd) to achieve a good FAX
resolution. For example, 115200 Bd on the serial port yield a FAX
sampling rate of 3600 or 7200 pixel/sec, respectively. If the baudrate
is equal or less than 2400, the sampling rate is set to a constant value
of 75 samples/sec, however FAX reception at baudrates below 19200 Bd
generally does not make much sense because the image signal then suffers
from heavy undersampling.

The hostmode FAX demodulators (AM/FM) have the same properties as the
corresponding FAX demodulators in terminal mode (**fax:**-menu). All
parameters accessible through the **fax:**-menu which have an effect on
the FAX demodulator remain also valid for hostmode FAX reception. Any
change of the FAX parameters from the default settings should be
performed unter terminal mode control (fax: menu) prior to starting the
hostmode.

All FAX receive data is buffered through the 4096 samples long FAX data
buffer (see @F command without argument). If a buffer overrun occurs
(frequency of data polls by the PC program too low), the buffer is
automatically cleared again (4096 samples are lost). Besides that, the
FAX buffer is always cleared automatically when hostmode FAX reception
is activated.

When hostmode FAX reception is active, all PACTOR relevant
functions/tasks are blocked, i.e. PACTOR calls can neither be initiated
nor be accepted. (Not all corresponding commands are blocked. The user
itself must be aware of this if a PC application program does not
already limit the command set available during hostmode FAX operation.)

All other processes which do not access the HF port (UHF/VHF Packet
Radio, particularly the TRX control) are still availble during hostmode
FAX reception.

The “extended hostmode” logic (channel 255) includes channel 252.

### @K

The KISS-Mode is activated with the commands `KISS` or alternatively
`@K` out of the normal command mode. This usually happens
automatically by the KISS-PC-software or a KISS capable controller (e.
g. TNC3). The KISS-mode is terminated by a system reset (power off/on
cycle), but can also be terminated by software with sending the decimal
byte sequence 192, 255, 192. The termination by sending the byte
sequence is usually done automatically by the software as well, and may
just once be configured correctly in the setup of the program.

### @S

If hostmode FAX reception (refer to 10.4.21, Page 177) is activated, the
additional hostmode command @S is available. It allows access to the 16
bit wide audio samples from the A/D converter on the HF port. The @S
command does not require a parameter. The audio sampling rate is 9600
samples per second and cannot be changed. As soon as the modem
recognizes a `@S` command, it starts acquiring 1024 16 bit samples on the
HF port. The samples are directly (no filtering, no AGC) written to a
data buffer and can be retrieved from there on hostmode channel 251.
Thus the modem generates 8 hostmode data packets (with data field length
256) per @S command. Every 16 Bit sample is split into 2 bytes, the less
significant byte (lower half of the 16 bits) appears first.

The @S command can be used for displaying the frequency spectrum of the
input signal on the HF port.

The extended hostmode logic (channel 255) includes channel 251.

### @T2

|                  |     |                                  |
|------------------|-----|----------------------------------|
| Default setting: | 500 |                                  |
| Parameter:       | X   | 1... 30,000, response time delay |

Sets the value for the AX.25 timer 2 (T2) in milliseconds.

After receiving a packet the PTC-IIpro waits the time T2 to check if
another packets follow. If so, all packets can be confirmed with only
one control packet.

### @T3

|                  |         |                                       |
|------------------|---------|---------------------------------------|
| Default setting: | 300,000 |                                       |
| Parameter:       | X       | 0... 3,000,000, time in milliseconds. |

The `@T3` command sets the T3 or link activity timer. If nothing is
received from the distant station for the time T3, then the link status
is polled.

###  %B

|                  |      |                                  |
|------------------|------|----------------------------------|
| Default setting: | 1200 |                                  |
| Parameter:       | Rx   | Rx baud rate for the radio link. |
|                  | Tx   | Tx baud rate for the radio link. |

Setting / checking the radio link baud rate.

Without a parameter, the **%B** command shows the modem type and the
baud rate as set. If a valid baud rate is given as parameter it is set
in the Packet modem. Valid baud rates are:

-   For the **SCS** DSP-Modem: 300, 1200, 9600, 19200.

-   For the **SCS** AFSK-Modem: 1200 and 2400.

-   For the **SCS** FSK-Modem: 4800, 9600, 19200, 28800, 38400,
    57600, 115200.

Some digipeater work with higher baud rate in direction to the user than
at the *Upload* side, e.g. DigiUser 19k2 and User Digi 9k6.

The Baud command allows two arguments, e.g. **%B** 19200 9600

The first argument is the receiving baud rate, the second one is the
transmission baud rate.

If only one argument is set, the PTC-IIpro uses this value for both, TX
baud rate and RX baud rate, e.g. **%B** 9600 \<Return>

It is also possible to enter the port directly, e.g. **%B** 2:19200 9600
\<Return>

The baudrate values for ports with the **SCS** DSP-Modem are stored in the Flash-ROM and remain valid also after a **RESTart** or a firmware update. |

### %C

This is identical to the `CLr` command in the main menu of the
terminal-mode. It works only on the PACTOR-channel.

### %E

|                  |     |                           |
|------------------|-----|---------------------------|
| Default setting: | 6   |                           |
| Parameter:       | X   | 1... 7, brightness value. |

Identical to the `BRightn` command of the main menu in the terminal
mode. This serves to set the brightness of the LED display between 6%
and 100%. The parameter 1 is equivalent to 6% of the maximum brightness.
Parameter 7 represents 100%.

### %F

|                  |     |                                                      |
|------------------|-----|------------------------------------------------------|
| Default setting: | 0   |                                                      |
| Parameter:       | X   | 0... 15, Filter parameter for the **SCS** FSK modem. |

This command is only valid in connection with **SCS** FSK modem! |

The filter parameters provide a certain adaptation of the signal to the
frequency transfer characteristics of the transceiver. In most cases,
good results are already obtained using the default setting 0. If any
problems occur when connecting a certain digipeater, another value
should be tried.

### %I

Initiates a BREAKIN. Works only in the receiving condition (*IRS*) (SEND
bit in the status byte = 0).

### %L

|                  |     |                                  |
|------------------|-----|----------------------------------|
| Default setting: | 1   |                                  |
| Parameter:       | 0   | PACTOR listen mode switched off. |
|                  | 1   | PACTOR listen mode switched on.  |

Turns PACTOR listen mode on (1) or off (0).

### %M

|                  |     |                                  |
|------------------|-----|----------------------------------|
| Default setting: | 0   |                                  |
| Parameter:       | 0   | hostmode expansion switched off. |
|                  | 1   | hostmode expansion switched on.  |

The parameter of the `%M` command activates the respective hostmode
terminal expansion. At a hostmode start, it is always set to 0. (The
hostmode program must choose the respective amount of expansion it needs
for itself after the start. This greatly eases step by step software
expansion).

If a too high value is chosen, (that cannot be interpreted by the PTC
due perhaps to an older firmware version), the PTC answers with an error
message (code byte=2) which contains the maximum possible argument
value.

`%M0` - Switches the hostmode terminal expansion off.

(This command is normally not needed by the terminal program, as the
`%M` parameter is automatically set to 0 at hostmode start.)

`%M1`- *delayed echo* is output with Code-byte=8.

(With PR up until now, even with `%M1`, no *delayed-echo* has been
given, as this function is better done over the monitor channel data
stream which can even handle self sent packets.)

Note: Code byte 8 is not defined in **WA8DED**-hostmode, and is used to
define a special extension of the PTC-IIpro. Terminal programs which
wish to work with the *delayed echo* in hostmode, must logically be
appropriately extended to contain this feature, and choose the extension
required automatically. Manual switching of the hostmode expansion is
not to be recommended due to possible incompatibilities.

### %O

Performs a CHANGEOVER. This command can also be used in the receiving
condition (*IRS*). In this case, it leads to a BREAKIN.

During transmission (*ISS*), the `%O` will be executed when all
characters in the transmission buffer are completely sent and confirmed.

### %P

|                                                     |     |                       |     |
|-----------------------------------------------------|-----|-----------------------|-----|
| Default setting: depending on installed Modems.** |     |                       |     |
| Parameter:                                          | X   | 1... 2, default port. |     |

The default port is set here, the **%P** command has influence at the
following commands:

C, P, T, W, @D, %B and %F.

### %Q

`%Q` basically has the same function as %O (over command), i.e. it puts an
“over token” to the end of the PACTOR transmit buffer triggering and
“over” from ISS to IRS state after all transmit data has been sent. In
contrast to `%O`, the `%Q` command does not cause a “breakin” (“over” from
IRS to ISS state) if the PTC currently is in the receiving state (IRS).

### %T

Displays the total number of bytes that have been sent and confirmed in
PACTOR so far. The value is reset at the end of each connection. The
number can also be reset by giving an argument behind the `%T`
command. The format is identical with the standard decimal ASCII output
as used in the hostmode.

### %V

Displays a short ASCII string containing the actual version number of
the actual version number of the PTC-IIpro firmware and the actual
version number of the PTC-IIpro BIOS.

Format for example: 2.8 1.32

Characters left of the dot are the main version number of the firmware.
Characters after the first dot until the first blank character are the
sub-firmware version number. Letters may also appear here. At least one
blank separates the firmware version number and the BIOS version number.
The BIOS version string is built in the same way, the convention just
refers to the second dot this time.

### %W

**For synchronizing external scanners**

Possible arguments: 0 or 1 (ASCII).

All responses to the %W command are null-terminated ASCII strings.

The `%W` command enables synchronizing between the PTC and external
frequency scanners. Examples for external frequency scanners are AirMail
and WinLink2000. These PC programs subsequently search for incoming user
calls on some different channels, changing the actual frequency by its
own without the aid of the internal PTC scanner (trx:-menu). Thus there
exist a (small) risk that a frequency change occures when the internal
scanner would not allow/perform a frequency change or more generally
speaking when a frequency change is prohibited due to a special actual
state of the modem, e.g. when the modem has already detected the
beginning of a user access on the PACTOR HF port.

In principle this problem can already be solved by using the scan-stop
signal the PTC provides - but only if the external scanner immediately
recognizes the scan-stop signal. Unfortunately, so-called latency time
(Windows) is introduced in practise. Latency time delays the scan-stop
signal and thus can cause “prohibited” frequency changes. An example of
a typical szenario: A user calls on channel A. The PTC has already
detected that it is being called and asserts the scan-stop signal - but
unfortunately some time (latency) elapses until the external scanner
finally receives the scan-stop information. Therefore, it’s not unlikely
that the scanner still changes the frequency (during the latency period)
to channel B although the PTC has already indicated that the scanner
should stop operation. The result is catastrophic: The system responses
on channel B although the user called on channel A. The connection
fails.

The %W command fully resolves this problem with the aid of a special
mechanism, regardless of the amount of latency introduced.

**Usage of the %W command:**

Prior to every scheduled frequency change the external scanner must send
a %W\[0\] command to the PTC: (Parameter 0 is optional but should be
given in order to make sure upward compatibility.)

**%W\[0\]**

Possible response of the PTC: 0 or 1.

0: Scan-Stop! Currently the frequency MUST NOT be changed! (After that,
if the modem does not indicate a connection to a user within a few
seconds, the %W0 command should be resent to the modem, and so on.)

1: Currently the frequency can be changed, scanning need not to be
suspended because no link establishment is in progress. Response “1”
also indicates that the modem has entered the so-called WAIT state. If
the modem is in WAIT state, it does not accept user calls on the HF port
(it cannot be connected by a user) any more.

Now the external scanner can perform a frequency change. After that it
must release the modem from WAIT state by sending %W1 to it. After
receiving the %W1 command the modem again accepts user calls on its HF
PACTOR port.

**%W1**

Possible response of the PTC: none.

Release from WAIT state. The modem enters the normal “standby state”
again and waits for incoming user calls.

Note: WAIT state always automatically times out after 10 seconds.

**The following chapters are only applicable for software authors! If you do not want to write your own hostmode program you can skip the following chapters.**

## Extended hostmode

The P4dragon DR-7800 supports the so called *extended hostmode*. The extended
**WA8DED**-hostmode has established itself as a *de-facto standard* for
communication between TNC/PTC and PC-control programs.

The *extended hostmode* makes the polling of the channels much easier
and thus reduces the polling overhead.

In the *extended hostmode*, channel number 255 is dealed in a special
way. A G command to channel 255 leads to the output of "255,x,y,z,...,0"
from the TNC. x, y, x, etc. are the numbers (binary and increased by
one) of the channels that contain new information, which can be
requested with the G command. The string given by the TNC on a poll of
channel 255 always ends with "0".

If, for example, only the monitor channel contains new information, the
answer string of the TNC to a G-poll of channel 255 is 255,01,01,0. If
there is no new information to be received, the output is 255,01,0
(255,0 is also possible). If there is new information in channel 2 and
3, the string is 255,01,03,04,0. The channel numbers are usually given
in increasing order - at least the P4dragon DR-7800 follows this
recommendation.

With the *extended hostmode*, a continuous cyclic polling of every
single channel with the G command has thus become obsolete, just channel
255 needs to be polled regularly. If the result indicates that there is
information in any other channel, only the respective channel has to be
polled using the G command to get the data.

## Status output in hostmode

The usual status byte can be called in the hostmode by polling channel
no. 254. A G poll of this channel always outputs a string containing the
actual status information of the P4dragon DR-7800. The format is: 254,07,0,S.
(S = binary status byte). It is hence a *byte-count format*:

channel number, code, length minus one, information byte(s).

The code of the status information is 07. According to the **WA8DED**
standard, this would also relate to *information from a connection*,
which, however, is usually used as a byte count format on channel 254.

In future releases, the status information is planned to be expanded to
several bytes. Using the length information from the **WA8DED**
standard, a longer status information will not lead to any problems of
compatibility. The terminal program can utilize exactly that number of
bytes that are interpretable by the respective software. Newer
expansions can easily be ignored that way.

The G poll command on virtual hostmode channel 254 (“status channel”)
can be extended by a single parameter in ASCII format, valid range 0-3,
e.g. G1. The parmeter determines, how many status bytes are sent back to
the PTC as a response to the G poll. The number of bytes calculates as
paramater value plus 1. Thus the command G0 is compatible with the usual
G poll without argument because it yields exactly ONE status byte, the
old, “normal” status byte. Therefore, a maximum of 4 status bytes can be
requested by the application software.

The contents of the status bytes is as following:

Byte 1: „normal“ (old/usual) status

Byte 2: PACTOR connect level:

> 0: not connected,
> 1: PACTOR-1
> 2: PACTOR-2
> 3: PACTOR-3
> 4: PACTOR-4

Byte 3: *Speedlevel* (submode of a PACTOR level):

> 0-1 on PACTOR-1
> 0-3 on PACTOR-2
> 0-5 on PACTOR-3
> 0-10 on PACTOR-4

Byte 4: Signed, actual receive frequency offset. Value 128 (= -128 ) is
invalid and thus should be ignored by the application software. This
helps to avoid “glitches” because the frequency byte only gets valid
after the frequency detector has obtained a stable estimate of the
frequency offset.

*Auto status* is triggered by a change of the contents of byte 1 or byte
3.

### Auto status in Hostmode

If the status-format is set to 2 (please refer to the `STatus` command
chapter 6.92), the PTC provides an automatic status also in the
hostmode. This mode leads to an inclusion of channel 254 if a G poll is
performed to channel 255 in the *extended hostmode*, and any change of
the status has occurred in the meantime. The output could thus be:
"255,01,255,0". This means that new status information is available on
channel 254. The channel 254 in the G poll list of channel 255
(*extended hostmode)* is cleared after polling of channel 254. (When any
status change occurs, channel 254 is added to the list again).

The normal G-poll of channel 254 is always possible, independent from
new information in the status. Even is the auto status is active, the
actual value can always be obtained by a regular poll.

## TRX Control Channel on Hostmode

Virtual hostmode channel 253 serves as transparent data channel between
PC and TRX port. Arbitrary data can be exchanged between PC and
transceiver on channel 253. This enables, for example, direct
transceiver remote control from the PC side. There is one length
limitation: If more than 1000 bytes of data sent from the transceiver
are already buffered, the PTC does not accept more data until the buffer
is flushed (data fetched by the PC application).

## NMEA-Channel

On hostmode channel 249 the P4dragon DR-7800 provides **all** NMEA sentences of
a connected GPS receiver. Except the terminating \<CR> (ASCII13) the
data is exactly matching with the one the GPS receiver sends. The
P4dragon DR-7800 buffers 32 sets of NMEA data internally.

This NMEA channel is also included in the *extended hostmode* channel
255, which means that the usual poll on channel 255 is sufficient to
determine if there is new NMEA data available on channel 249.

## CRC Hostmode

The expanded **WA8DED** hostmode (*extended hostmode*) has established
itself as a de-facto standard for communication between TNC/PTC and PC
control programs.

Although containing a very well thought out structure, which
considerably eases compatibility of extensions, the **WA8DED** hostmode
has two basic weak points, which can cause serious problems with data
corruption or loss during operation:

1.  There is no reasonable possibility for a resynchronization of the
    hostmode operation if through any reason the synchronization is
    broken. (Even if a new synchronization does occur, it is highly
    probable that it will cause defective data transfer during the
    synchronization phase).

In the worst case, it only needs one destroyed bit in the data flow
between the PC and the TNC to cause a hostmode crash.

9.  Defective data cannot be uniquely identified, and it is not possible
    to request repetition of destroyed data. The data security in the
    link between the PC and the TNC has a weak point here. A correct
    transfer of sensitive data (such as program data in 7PLUS formator
    direct binary data) via an insecure **WA8DED**-hostmode cannot
    therefore be fully guaranteed.

10. Data transmission via multiple nodes (e.g. **WINLINK** forwarding)
    increases the potential for error due to corruption via the RS-232
    links.

Possible sources of error:

-   During active transmitter operation, HF can corrupt data.

-   Short spikes due to heavy loads being switched on or off on the AC
    power line, or through close lightning strikes etc. They can all
    cause error bursts, especially on longer RS-232 lines.

-   Slow or wrongly configured multitasking systems (WINDOWS) tend to
    *swallow* a character or even complete pieces of text, especially
    when the computer is heavily loaded. This is due to the overflow of
    (sometimes non-existant) buffers and also timing problems on the
    RS-232 interface itself.

-   The CRC-hostmode solves all these problems in that every hostmode
    data packet has a highly secure integrated CRC check sequence
    included. Errors can therefore be easily detected. The CRC-hostmode
    protocol also allows the request for and the automatic
    re-transmission of packets recognized as containing errors. Basic
    principles

### Extended CRC-hostmode

The command JHOST5 enables the extended CRC-Hostmode. This is compatible
to JHOST4, but allows data packets to be transferred with a lengh of max
1024 bytes on the FAX-channel 252 in the direction PTC to PC. The added
2 length bits are bit 4 and bit 5 of the code-byte.

JHOST5 especially enhances weather FAX receiption with the use of the
Bluetooth interface by compensating the probably occuring higher latency
time. Certainly, also with the use of the USB or RS232 interface the FAX
receiption timing becomes less critical with the use of JHOST5. (With
slower PC’s, the probability of “gaps“ in received pictures decreases.)

### Basic principles

The term *send packet* or *receive packet* has nothing to do with the
data actually transmitted or received via the HF link. They concern
themselves **only** with data present on the RS-232 interface. The #
character means *Binary byte*.

The protocol is based on the *extended hostmode*. A number of data
packets are built up according to this sub-protocol.

The HOST (PC) is, as in **WA8DED** mode, the MASTER. That means that
every action is initiated by the PC. The TNC/PTC (SLAVE) may never send
data with-out being first requested by the PC.

For every action by the MASTER, exactly one reaction from the SLAVE must
follow. The Master must wait for this reaction before it starts any
other new action. There is of course, a timeout allowed for this waiting
time (see below).

Every **WA8DED** data packet is expanded by a (unique) header,
consisting of #170 - #170.

Every **WA8DED** data packet is completed by the addition of two CRC
data-bytes (binary). The CRC is calculated exactly according to the
CCITT-CRC16, and is thus identical to that used for PR and PACTOR. The
CRC is calculated from the first byte after the #170 - #170 header
(channel number). (CRC see AX.25-protocol and example in the chapter
10.9.8, page 191).

Directly before the transmission, thus at the lowest sub-protocol level,
the data packet transmitter (MASTER and SLAVE) carries out so-called
Byte-Stuffing. This prevents the #170 - #170 sequence from appearing
within a packet.

The Byte-stuffing takes place directly after the 1st byte after the #170
- #170 header, and ends after the second CRC-byte. It therefore ranges
over the complete packet (excepting the header). Also, even when the
second CRC-byte has the value #170, this changes due to the stuffing.
Stuffing means that after every byte with the value #170, a further byte
with the value #0 is inserted. (The CRC calculation is only carried out
on the original packet, not on the stuffed packet.) The packet counter
concerns itself always with the original length of the packet (without
stuffing!).

Directly after the packet is received, and thus at the lowest
sub-protocol level, the packet receiver (MASTER and SLAVE) carries out a
so-called Byte-de-stuffing. This removes the #0 bytes inserted by the
packet transmitter. The byte-de-stuffing begins directly after the first
byte after the recognized #170 - #170 header. After every byte with the
value #170, one byte is erased, providing it is a #0 byte. (If the
following byte does not have a value of "#0", then error handling is
carried out, refer to chapter 10.9.5, page 190).

The MASTER uses a 1 bit packet-counter, using bit 7 of the
CMD/INF-bytes, that is incremented (= inverted) on sending a **new**
(not repeated) packet. This packet counter (and request flag) allows the
SLAVE to positively identify repeated MASTER packets.

The slave possesses the possibility to quickly inform the Master that
the last transmitted packet should be repeated, by inserting a short
request packet. The request packet has the format: "#170#170#170#85".

### MASTER protocol

Definition of the MASTER-condition

-   NACK-condition

> \- When no reaction is received from the SLAVE within 250 ms after the
> MASTER transmitted packet has ended.
>
> \- This is a minimum time. The modem answers within a few
> milliseconds. With very slow TNCs the waiting time can be changed in
> the MASTER program.

(Note: Timeout watchdog is stopped as soon as a packet-header is
received (i.e. the packet starts being read in). The maximum useable
data length of a *null-terminated* packet must not exceed 256).

> \- If a packet-header is identified within 250 ms, a packet is read
> in, and a CRC error takes place.

\- If a request-packet is identified.

-   ACK-condition

\- If a data-packet with the correct CRC is received.

Reaction of the MASTER to various conditions

-   Reaction of the MASTER to an NACK condition.

\- Repetition (transmit) of the buffered last packet with the
request-bit unchanged.

-   Reaction of the MASTER to an ACK condition.

> \- A new packet can be sent to the slave, if available. The request
> flag is inverted before the transmission. (Note: this packet must also
> be buffered in case a repetition is requested.)

### SLAVE-protocol

Definition of the SLAVE-condition

-   NACK-condition

\- If a packet-header is identified, but a CRC error takes place.

-   ACK-condition

> \- If a packet is correctly received (CRC OK) and the request flag is
> different compared with the last correctly received packet.
>
> \- If bit 6 in the CMD/INF byte is set, then the condition of the
> request-flag in the last correctly received packet is ignored. Every
> correctly received packet with bit 6 in the CMD/INF byte causes an
> ACK-condition. A request condition is thus impossible here.

-   Request-condition

> \- If a packet is correctly received, and the request-flag is
> identical to the last correctly received packet. (Bit 6 of the
> CMD/INF-byte must be erased. Refer to the text above.

Reaction of the SLAVE to various conditions

-   Reaction of the SLAVE to the NACK-condition

> \- Transmission of the special request-packet #170 #170#170#85.
> (direct request for a repetition of the defective packet without
> waiting for the MASTER-timeout NACK condition).

-   Reaction of the SLAVE to the ACK-condition

> \- Transmission of the present (new) response-packet (e.g. data packet
> if a G-POLL). NOTE: This packet must be buffered in case of a later
> repetition)

-   Reaction of the SLAVE to the request-condition

> \- Repetition of the last (buffered) packet. Information of the
> present received packet is not used, it is thrown away/erased.

### Stuffing errors or unexpected header sequences

- The sequence #170#0 during a header search is interpreted as an ERROR, and the header search carried on.

- Sequences between #170#1-#169 and #170#171-#255 during the header search AND during the packet read-in are interpreted as an ERROR and cause a *newstart,* i.e. the header search is started afresh.

- #170#170 ALWAYS leads to a *start of packet* condition, under all situations. The next byte is then appropriately interpreted as the channel number. (However after a start of packet is recognized, two #170 in a row must follow so that this *exception* can work again. This would be in the case #170#170#170...)

### Start of the CRC-hostmode

- The command that switches a TNC/PTC into hostmode is
    \<ESC>JHOST4\<CR>.

- After the start of the CRC-hostmode, the internal REQUEST-bit in the SLAVE (PTC) should be set to *not defined* so that either 1 or 0 are valid as REQUEST-BIT in the first transmit packet from the MASTER.

  Thus when the CRC is correct at the SLAVE, an ACK-condition follows.

  Independent of the above, it is recommended that the first transmit packet from the MASTER, after a hostmode start, or program start, should have bit 6 set, to ensure that a correctly received packet at the SLAVE always leads to an ACK-condition. (This allows the MASTER to start the protocol without having to know the condition of the (old) buffered RQ-flags at the SLAVE.)

### Recommended baudrate

Due to the considerably higher overhead in the CRC-hostmode, it is recommended that the RS-232 data rate not be set lower than 19200 Bit/sec. There is otherwise the risk that the response time could be too long, and the effective data throughput, especially when multitasking with Packet-Radio, would be to slow for useful working.

### Example source code for CCITT CRC16 (HDLC)

Example program in Turbo PASCAL:
```
/*
  unsigned short = 16 bit Datentyp
*/

unsigned short crc_table[256]; /* wird dynamisch aufgebaut */
unsigned short crc;

void CALC_CRC_CCITT (unsigned char b)
{
  crc = ((crc >> 8) & 0xff) ^ crc_table[(crc ^ b) & 0xff];
}

void InitCRC (void)
{
  unsigned short index;
  unsigned short j, accu, Data;

  for (index = 0; index < 256; index++)
  {
    accu = 0;
    Data = index;
    for (j = 0; j < 8; j++)
    {
      if ((Data ^ accu) & 0x01)
      {
        accu = (accu >> 1) ^ 0x8408;
      }
      else
      {
        accu = (accu >> 1);
      }
      Data = Data >> 1;
    }
    crc_table[index] = accu;
  }
}

void CCITT_CRC (void)
{
  InitCRC();            /* Baue CRC-Tabelle auf */

  crc = 0xffff;         /* Start-Wert des CRC-Registers */

  /* Berechnung des CRC folgt - fuer jedes Input-Byte muss
     CALC_CRC_CCITT einmal aufgerufen werden. */

  CALC_CRC_CCITT(0x04);
  CALC_CRC_CCITT(0x01);
  CALC_CRC_CCITT(0x01);
  CALC_CRC_CCITT(0x47);
  CALC_CRC_CCITT(0x47);

  /* und so weiter.... */

  crc = ~crc;       /* CRC wird am Schluss invertiert laut HDLC-Protokoll */

  /*
     In der Variablen crc steht der CRC-Wert. Wenn alle Bytes, die in den CRC
     einfliessen sollen, abgearbeitet sind, haengt man zuerst das
     Low-Byte vom WORD CRC und schliesslich das High-Byte an den
     Block als "CRC" an. Bei den obigen 5 eingerechneten Beispiel-Bytes
     sollte sich ein CRC-Wert von LOWBYTE=0xD5, HIGHBYTE=0x99 ergeben.

     Beim Ueberpruefen des CRC ("Empfang") rechnet man auch die beiden
     uebertragenen CRC-Bytes noch in den CRC-Wert mit ein. Der dadurch
     erhaltene neue CRC-Wert muss dem Wert 0xF0B8 entsprechen, falls
     der Block korrekt angekommen ist.
     Alternativ dazu kann man den CRC auch nur über die Datenbytes rechnen
     ohne die eigentlichen CRC-Prüfbytes einzubeziehen. Invertiert man die
     beiden so errechneten Bytes, muss das Ergebnis mit den beiden empfan-
     genen CRC-Bytes übereinstimmen.
  */
}
```
