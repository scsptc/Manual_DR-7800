# PTC-Firmware

With the PTC-IIpro it is nearly possible to configure everything. In the
manual always the default settings are assumed! If you have changed
these settings you must keep this in mind while reading the manual. This
is very important in case of the control characters which can be freely
defined (CHANGEOVER character in chapter 6.19 on page 67, ESCAPE
character in chapter 6.39 on page 79, BREAKIN character in chapter 6.12
on page 64 and the QRT character in chapter 6.79 on page 98).

## General

The operation of the PACTOR-Controller (PTC) takes place using commands
which are sent over the serial interface. The data transfer format is:
**8 data bits, 1 stop bit, no parity and half-duplex**. The baudrate is
normally sensed automatically by the PTC. The PTC then acknowledges with
**cmd:** and waits for a command. All commands and command strings are
closed with \<CR> (ASCII 13). \<LF> (ASCII 10) is ignored during the
command input. Working on the computer means you have to enter
\<Return>. Corrections can be carried out with *Backspace* (ASCII 8),
above the \<Return> key.

When in Standby, the **cmd:**-prompt is available immediately after the
last command. The PTC is in the command mode. The command mode is
displayed with the system prompt **cmd:** or **pac:**.

During link set-up and while connected the PTC is in the converse mode.
Switching to RTTY or turning on the CW terminal also activates the
converse mode. Whereas in the so-called converse mode, characters from
the RS232 interface are placed in the transmit buffer and are sent over
the HF channel at the next opportunity.

In Converse mode, commands to the PTC must be preceded with an ESCAPE
character (initially set to \<ESC>, ASCII 27). After each ESC character,
only ONE command is accepted. After an invalid entry, however, the PTC
immediately allows a new input. (The ESCAPE character, as well as the
following command characters, DO NOT, of course, go into the transmit
buffer).

During an Unproto transmission the output amplitude shall be modified.

Start unproto transmission

**cmd:** **U 1** \<Return>

The PTC-IIpro starts the Unproto transmission and switches in the
converse mode.

Clicking on \<Esc> enables the command prompt **cmd:**. Now you can
enter the command to change the output amplitude.

**cmd:** **FSKA 100** \<Return>

Only this command is executed. The PTC switches immediately back to the
converse mode. Now you can stop the Unproto transmission entering the
QRT character.

\<Ctrl> + \<D>.

The PTC ends the Unproto transmission and changes to the command mode.

## Command structure

PTC commands are similar to the commands of a TNC with *TAPR* software
this makes it easy to learn and handle.

There are commands with and without arguments. If an argument is
possible the argument has to be separated from the command by at least
one space. A command's current argument setting is displayed if the
command is entered without an argument.

Nearly all commands can be used in abbreviated form to save keystrokes.
The shortest keyword of a command consists of the fewest number of
characters that uniquely identify it, e.g. you may type **C** instead of
**Connect**. All command inputs are internally converted to upper case,
so both character shifts may be used. All commands are listed below,
significant mnemonics are printed in capital letters. The short form of
the **SERBaud** command is **SERB**.

## Menus

The PTC-IIpro commands are combined into different function groups, so
called menus. The different menus are the following:

-   Packet-Radio

-   Audio functions

-   FAX/STTV

-   Transceiver controlling

-   System test

Last not least the *main* menu with the PACTOR/AMTOR/RTTY/CW/PSK31
commands.

The command prompt indicates the menu you have already selected. The
following table shows the prompts for the different modes.

| **Prompt** | **Menu**                |
|------------|-------------------------|
| cmd:       | Main menu               |
| pac:       | Packet-Radio            |
| aud:       | Audio functions         |
| fax:       | FAX/STTV                |
| trx:       | Transceiver controlling |
| sys:       | System test             |

Table 5.1: Command prompts

The separated function groups are for a better overview but this is not
their only reason. PACTOR for example has for the short wave port the
command **TXDelay** and for the Packet-Radio port also the **TXDelay**
command. The same is with the **Mycall** command for PACTOR and
Packet-Radio.

The grouping of the commands within the menus allows to choose the right
commands for the selected modes or functions.

## Simultaneous STBY mode

In the STBY condition, the PTC automatically knows if it is called in
AMTOR or PACTOR, answering in the respective mode. It is possible to use
the **ARX** command to suppress the AMTOR reaction (In ARQ as well as
FEC).

The **SCS**-PTC offers the possibility to receive AMTOR FEC and NAVTEX
transmissions from the STBY condition. For this, the **BC** parameter
must be set to 1. The reading of AMTOR FEC and NAVTEX can be inhibited
with the **ARX** command, independently from **BC**.

## Remote commands

Some PTC commands are also available for the distant station via the HF
link. There are two control possibilities.

-   First Setting: **REMOTE** 1 and **BOX** 0. With this setting, all
    remote control commands via the radio link must begin with a //
    sequence, and end with a CHANGEOVER. (e.g. **//Date** \<Ctrl> + \<Y>
    or **//Dir** \<Ctrl> + \<Y>).

-   Second Setting: **BOX** 1, the BOX mode. With this setting, all
    remote control commands may be directly entered via the radio link,
    and terminated with a \<Return>. (e.g. **LOG** \<Return> or **Show**
    \<Return>)

The commands for the PTC mailbox and for the gateway mode also belong to
the remote commands.

Here is a list of all remote control commands:

| **Command** | **Short description**                           | **Reference** |
|-------------|-------------------------------------------------|---------------|
| BEll        | Call the Sysop.                                 | Chapter 6.11  |
| Check       | Lists actual mails                              | Chapter 6.17  |
| CLr         | Erase the transmit buffer.                      | Chapter 6.20  |
| Connect     | Packet-Radio Gateway (Flexnet Style).           | Chapter 6.22  |
| DAte        | Calls up the PTC date.                          | Chapter 6.33  |
| DELete      | Erase a file or files.                          | Chapter 6.35  |
| DIR         | Read the main directory.                        | Chapter 6.36  |
| Gate        | Packet-Radio gateway.                           | Chapter 6.43  |
| Help        | Help !!                                         | Chapter 6.45  |
| LIst        | Gives a list of files within a subdirectory.    | Chapter 6.49  |
| LOg         | Calls up the PTC log book.                      | Chapter 6.52  |
| LOGIn       | Log in for AMTOR.                               | Chapter 6.53  |
| Phase       | Calls up phase information.                     | Chapter 6.72  |
| POSition    | Requests GPS position                           | Chapter 6.73  |
| Qrt         | Starts QRT.                                     | Chapter 6.78  |
| Read        | Reads a particular file.                        | Chapter 6.80  |
| RESEt       | Resets the PTC (without loss of MBX data).      | Chapter 6.83  |
| Send        | Sends a particular file.                        | Chapter 6.108 |
| SHow        | Calls up QSO statistical data and PTC settings. | Chapter 6.89  |
| TIme        | Calls up the PTC clock time.                    | Chapter 6.95  |
| TRX         | Transceiver control.                            | Chapter 6.99  |
| USer        | Shows the current users.                        | Chapter 6.104 |
| Version     | Calls up the PTC software version.              | Chapter 6.107 |
| Write       | Writes a file into the PTC Mailbox.             | Chapter 6.108 |

Table 5.2: Remote commands

In addition, all remote control commands are identified with the word
<sub>Remote</sub> in the table of contens and command description in
this manual. (refer also to chapter 6.82, page 99).

## PTC-Mailbox

The PTC contains its own built-in mailbox. The mailbox files are stored
in static RAM and remain there even when the power supply is turned off.
The maximum allowable file length and the number of files in the mailbox
is only limited by the amount of free memory. The memory can be expanded
up to 2 MByte. Filenames may be a maximum of 10 characters long, and
should contain no special characters. The PTC truncates all over long
filenames after 10 characters, no difference being made between upper
and lower case letters.

Entering the Help command via PACTOR the mailbox of the PTC-IIpro
displays the following list.

\<pactor remote commands>

h(elp) q(rt) da(te) ti(me)

d(ir) w(rite) r(ead) del(ete)

sh(ow) v(ersion) p(hase) lo(g)

c(heck) c(onnect) cl(r) l(ist)

s(end) be(ll) trx g(ate)

rcu us(er) pos(ition)

characters within brackets are optional.

For more information type: h command (eg: help send).

next?

Display 5.6.1: PACTOR mailbox help

At Read and Send commands (on the terminal side) without a file number,
either the first file will be read, or, if more than one file is
present, the directory will be shown. When no argument is given, then
the present directory name (path) will be used by the file system.

BREAKIN during a remote text output (also while reading a file) will
erase the text output or ends the file read.

After a **Disconnect**, **RESEt** or **RESTart**, the current directory
is set to the **MYCALL** given value. With a connect from another
station (Slave connect), the current directory is set to the call of the
other station.

Valid **Write**-, **List**-, **Read**-, or **DELete** commands set the
path to the given directory. (The directory name must naturally be
explicit in the argument).

A list of the commands follows:

| **Command** |     | **Short description**                     |     | **Reference** |     |
|-------------|-----|-------------------------------------------|-----|---------------|-----|
| Help        |     | Help !!                                   |     | Chapter 6.45  |     |
| BEll        |     | Call the Sysop.                           |     | Chapter 6.11  |     |
| Dir         |     | Read the main directory OF THE MAILBOX.   |     | Chapter 6.36  |     |
| List        |     | Gives a list of files within a directory. |     | Chapter 6.49  |     |
| Check       |     | Lists actual mails                        |     | Chapter 6.17  |     |
| Read        |     | Reads a Mail.                             |     | Chapter 6.80  |     |
| Write       |     | Writes a mail into the PTC Mailbox.       |     | Chapter 6.108 |     |
| Send        |     | Sends a mail.                             |     | Chapter 6.86  |     |

| **Command** | **Short description**                        | **Reference** |
|-------------|----------------------------------------------|---------------|
| DELete      | Erase a mail.                                | Chapter 6.35  |
| USer        | Shows the current users.                     | Chapter 6.104 |
| LOg         | Calls up the log book.                       | Chapter 6.52  |
| Qrt         | Leaves mailbox, alternative the command BYe. | Chapter 6.78  |
| Gate        | Packet-Radio gateway.                        | Chapter 6.43  |
| Version     | Calls up the version.                        | Chapter 6.107 |
| CLr         | Erase the transmit buffer.                   | Chapter 6.20  |
| DAte        | Calls up the date.                           | Chapter 6.33  |
| TIme        | Calls up the clock time.                     | Chapter 6.95  |
| SHow        | Calls up QSO statistical data.               | Chapter 6.89  |
| Phase       | Calls up phase information.                  | Chapter 6.72  |
| POSition    | Requests GPS position                        | Chapter 6.73  |
| TRX         | Transceiver control.                         | Chapter 6.99  |

Table 5.3: PACTOR mailbox commands

Of course it is possible to enter mailbox commands on the console. With
the **DIR** and **LIst** command you can check the mailbox contents.
**Write** saves the mail, with **Read** you can read the mail and with
**DELete** you can delete the mail.

### Multiple file operations

All commands that contain a file number in the argument (e.g. **DELete**
or **Read**) allow batch access. File numbering is indicated in the
format start-end.

**DEL** test 1- entire directory named 'test' is erased  
**R** 2-4 read file numbers 2 to 4 of the present directory  
**Dir** 4- lists the files in the present directory from no. 4 till the
*last* *file*

### Special features when reading files

When a remote station is reading out a file in PACTOR the PTC checks if
the file has been written in AMTOR. Next of all it is checked if it only
contains capital letters. If yes, then the PTC converts the file
contents into lowercase letters, which can lead to almost doubling of
the transmission speed in PACTOR, due to more effective Huffman coding.

### The PTC mailbox for Packet-Radio

Up to four PR (Packet-Radio) users may be simultaneously connected in PR
to the PTC-mailbox. There they may read files, write files and delete
files. In addition, the PTC-IIpro allows a further user simultaneous
access to the internal mailbox via Pactor I/II or AMTOR. Virtually
unlimited access is thus allowed to the same *data pool* via
PACTOR/AMTOR and PR. This result in an increased data transparency at
the HF/VHF interface, allowing an easier direct transfer of data between
HF and VHF users. This property of the PTC-IIpro allows it’s use as a
powerful and flexible personal (private) *maildrop*. It is also possible
to use it in smaller general mailbox systems as a *stand-alone*
solution.

The PR mailbox in the PTC-IIpro can be viewed as a self contained *TNC
in the PTC*. This *virtual* mailbox TNC contains its own callsign, the
BBS-MYCALL. The user can reach the PR mailbox in the PTC-IIpro by
connecting to the BBS-MYCALL of the PTC-IIpro. The BBS callsign is set
automatically to MYCALL-8, either at the first start (when the
*Flash-Call* in the BIOS has been defined, or when ones own
PACTOR-MYCALL has been set.

If, for example, DL1ZAM is given as the first PACTOR-MYCALL then the
PR-mailbox can be connected to under the callsign DL1ZAM-8. The
BBS-MYCALL callsign of the PTC can be changed or checked thereafter at
any time with the **MYMail** command in the **pac:**-menu.

To change the setting of the PR-box characteristics, there are three
commands in the  
**pac:**-menu: **PRBox**, **MYMail** and **MText**.

### Practical operation using the PR mailbox

After a Help command, the PR mailbox of the PTC-IIpro displays the
following list:

PTC-IIpro Mailbox Help

----------------------

Bell Check Date Dir Erase Gate

Help List LOg POSition Quit Read

Send Time TRX User Version

Type “Help command” for detailed information.

Display 5.6.2: PR mailbox help

These are the commands available for PR. They behave, with few
exceptions, exactly as those for PACTOR. A few commands also allow an
alternative input, and so the command interpreter understands **Write**
instead of **Send**, **Bye** instead of **Quit** and **DELete** instead
of **Erase**.

There is a special small help text available for each command, which the
user can call up with **Help** followed by the appropriate command. E.g.
**Help Send** \<Return>.

| **Command** | **Short description**                             | **Reference** |
|-------------|---------------------------------------------------|---------------|
| Help        | Help !!                                           | Chapter       |
| BEll        | Call the Sysop.                                   | Chapter 6.45  |
| Dir         | Read the main directory OF THE MAILBOX.           | Chapter 6.36  |
| List        | Gives a list of files within a directory.         | Chapter 6.49  |
| Check       | Lists actual mails                                | Chapter 6.17  |
| Read        | Reads a Mail.                                     | Chapter 6.80  |
| Send        | Sends a mail, alternative the command **Write**.  | Chapter 6.108 |
| Erase       | Erase a mail, alternative the command **DELete**. | Chapter 6.35  |
| User        | Shows the current users.                          | Chapter 6.104 |
| LOg         | Calls up the log book.                            | Chapter 6.52  |
| Quit        | Leaves mailbox, alternative the command **BYe**.  |               |
| POSition    | Requests GPS position                             | Chapter 6.73  |
| Gate        | Packet-Radio gateway.                             | Chapter 5.11  |
| Version     | Calls up the version.                             | Chapter 6.107 |
| DAte        | Calls up the date.                                | Chapter 6.33  |
| TIme        | Calls up the clock time.                          | Chapter 6.95  |
| TRX         | Transceiver control.                              | Chapter 6.99  |

Table 5.4: Packet-Radio mailbox commands

Every text output from the PTC-IIpro PR mailbox is ended with a *Prompt*
which is identical in format to many mailbox systems (present directory
in brackets followed by the user callsign and mailbox callsign. E.g. :
**(TEST) DL6MAA de DL1ZAM>**.

The present directory is automatically changed with the usage of the
read-, write- and list- commands.

Mailbox *Batch* access, (e.g "**Read** 1-") is also available on PR.

7PLUS files can be read from, and written to, without problem.
AUTO-BIN-transfer or similar protocols are at present not supported by
the PR mailbox.

Uppercase and lowercase letters are not distinguished in the command
processing. All commands can be more or less abbreviated. The maximum
abbreviation possible can be found in the help text. Only the letters
written in capitals must be typed for the command to be correctly
understood.

PR mailbox links occupy as is *usual*, the lowest free channel of the
PTC-IIpro. The terminal program also displays the usual *connect
message* when a *mailbox connect* is made, with however, the addition
"(**BBS-Connect**)".

Local text input from the terminal to channels already occupied with BBS
connects are ignored. It is however, always possible for the Sysop to
disconnect an existing BBS connection by giving a disconnect command via
the local terminal.

Received text is displayed in hostmode terminal programs (e.g. **GP**)
exactly as usual and can be followed by the Sysop. The Sysop can hereby
notice which commands are given by the users. In terminal mode, the text
output from the BBS channels are completely suppressed to prevent that
the PTC-IIpro receives buffer filling and maybe overflowing.

### Passing PR connects to the mailbox

The **USers** command in the **pac:**-menu allows any incoming PR
connect to be passes over to the PTC-IIpro PR-mailbox. To do this
**USers** has to be set to 0. This will allow for example, that on
leaving the terminal program, (e.g. automatic de initialising with
**Y**0 in **GP**) the PTC-IIpro can be brought to a condition where a
connect using the *normal MYCALL* (i.e. without the -8) will be
transferred to the mailbox. This is useful, as many potential users
would use the *normal MYCALL* to connect to the PTC-IIpro.

If the terminal is *off-line*, and the configuration is correct,
(**USers** 0 or **Y**0) then all calls, irrespective they are the
*normal MYCALL*, the *MYALIAS*, or the *BBS-MYCALL*, will be transferred
to the PTC-mailbox.

### Properties of mailbox-commands

**Send**

Text input can either finished with \<Ctrl-Z> or with \*\*\*end, as well
known from other mailbox systems. The NNNN sequence has no effect in PR
!

Files that have been input via PR are signified in the status display
(ST), the **LIst**- and **CHeck**- outputs by being marked with an X
(AX.25), e.g: .... NX DL2FAK ...

The mail LED starts to blink when a file is written via PR whose
filename is the same as the MYCALL of the PTC-IIpro for channel 0.

**Read**

Even during a file read operation, it is possible to give further
commands to the PTC mailbox. These commands are stored in a buffer, and
only acted upon when the relevant file read operation is complete. An
empty input (only \<Return>), interrupts the file read operation.

**User**

Lists the presently active links, similar to the **CStatus** command in
the **pac:**-menu. A presently active PACTOR link is displayed in
channel 0 of the list and in addition marked with the comment PACTOR.
Every active link with the PTC mailbox is displayed with the callsign of
the connected station, together with the appropriate digipeater list.

PR links that are not connected to the PR-Box are displayed as a so
called *NON-BBS-CONNECT*, without however, the callsign of the opposite
station.

## The NAVTEX-Processor

### NAVTEX General

The NAVTEX service, introduced a number of years ago as part of the
GMDSS (Global Marine and Distress Safety System), is a maritime news
service, broadcasting weather, navigational and safety information to
shipping. This gives the impression that the system uses the most modern
technology. In fact, underneath the impressive sounding name, is nothing
other than a network of marine coast stations that

broadcast plain language messages using the SITOR-B system, at specific
times. This system is known to amateurs as AMTOR mode B or FEC. It uses
the usual 170 Hz FSK modulation system, which is also an old and wide
spread system in HF digital radio. For NAVTEX, only one MF channel on
the frequency of 512 kHz has been allocated. The transmission range is
approximately 800 km. A range limitation is an essential part of the
system so that reliable time sharing of the one frequency between the
various coast stations is possible. It is basically possible to decode
NAVTEX using any AMTOR modem, however, it has proved in practice, that
just reading the transmissions has a number of disadvantages, and is
therefore not of great value.

In the flood of messages sent, without pre-selection and a form of
buffer memory, it is very likely that the "interesting" messages will be
lost.

The messages are sent more than once, the newer ones at least every 4
hours, the older ones at longer intervals. As SITOR-B is very prone to
errors when signals are weak, the receiver should ensure that only the
best copy of the message to date is stored, and available for the Radio
Officer or Navigator. This is totally impossible by just "reading the
mail".

As NAVTEX works on long waves, the reception is generally better at
night than during the day. When sunny, the electrical energy
requirements of small ships can be met by solar panels. At night this is
not possible. The noise of a generator is also not exactly customised to
enhance the sleep of the crew. The power requirements at night should
thus be kept as low as possible. A continuously running laptop or other
computer is a relatively large load for the energy supply of a small
ship. A NAVTEX controller should therefore be able to operate without
any additional computer, and use little electrical energy itself.

The NAVTEX processor of the PTC-IIpro solves many of the disadvantages
mentioned above. It enables:

Automatic, selective reading of NAVTEX transmissions. Either the code
for the type of message or the regional code can be selected.

Automatic processing of transmissions received more than once. Only the
best copy is held. Old data is automatically deleted.

A fast check on the type of received messages.

A memory buffer is available without using an external computer, as the
NAVTEX processor uses the PTC-IIpro internal mailbox as a message store.
It automatically lays down, if not already there, a subdirectory called
NAVTEX in the PTC-box. Data written into the mailbox by the NAVTEX
processor can be accessed via PACTOR or Packet-Radio.

### The NAVTEX System in Detail

As mentioned above, NAVTEX messages are sent in plain language using
SITOR-B coding. To mark the beginning, end, and type of message, NAVTEX
uses a simple convention.

Every message begins with the characters ZCZC, followed by a space. Then
follows the four figure message identifier plus a carriage return. The
actual message now follows.

Every message finishes with NNNN. (If these end characters are
mutilated, the NAVTEX-processor finishes writing the message at the
latest after loss of receive synchronisation).

The message identifier is constructed as follows:

The first character is a letter, with a range of A to Z. This letter
sets the area code and is allocated to one transmitter in the reception
area. Which letter is allocated to which transmitting station can be
seen relatively fast, as the transmitting station is usually also
mentioned in the message itself.

The second letter describes the type of message. The following types are
presently defined:

|     |                          |
|-----|--------------------------|
| A:  | Navigational Warning     |
| B:  | Meteorological Warning   |
| C:  | Ice Report               |
| D:  | Search and Rescue Info   |
| F:  | Pilot Message            |
| G:  | DECCA Message            |
| H:  | LORAN-C Message          |
| I:  | OMEGA Message            |
| J:  | SATNAV Message           |
| K:  | Other NAV aid system Msg |
| L:  | Navigational Warning (2) |

The next two places in the message identifier contain the message
number. This number belongs to a message of a particular type and
remains unchanged when a message is transmitted more than once. The
numbers are consecutive. The number has a decimal format and comprises
00 to 99. If an overflow occurs, i.e. "started" again at 00, then
usually, the "old" 00 message is no longer active, and permission to
erase has been granted, or has already automatically been erased by the
NAVTEX processor. This is naturally valid for all numbers in consecutive
operation. An exception can occur in the very numerous "Navigational
Warning" messages. That is why there are two different message type
letters, A and L, which actually describe the same type of message. This
trick allows the possible number of active "Navigational Warning"
messages to reach 200.

### Operating the NAVTEX Processor

The NAVTEX processor has only a single new command in the **cmd:**-menu.
This is **NAVtex**. This command allows the complete configuration and
activation of the automatic NAVTEX processor. It operates in the
background, as a completely seperate process within the PTC-IIpro
multitasking environment.

When activated, the NAVTEX processor lays down a directory with the name
NAVTEX in the PTC-IIpro mailbox, and stores all incoming NAVTEX messages
there. The name of the message author is given as "AUTO-NAV". The NAVTEX
processor gives the complete four figure message header as well as the
plain language name of the type of message. E.g. "CA03 Navigational
Warning".

The PTC-IIpro displays the message **AUTO-NAV** on the green
alphanumeric display whilst message storage is taking place. If the
number of messages in the NAVTEX directory is exceeds the maximum
allowed, the NAVTEX processor deletes the oldest message it has
previously stored before starting to store a new message. (Messages from
other sources which may also be in the NAVTEX directory - such as
operating instructions - are NOT deleted!). For details on the
**NAVtex** command refer to chapter 6.66 on page 90.

### Notes about NAVTEX practice

The PTC-IIpro normally operates with 200 Hz shift for FSK operation.
Although NAVTEX uses 170 Hz shift, it is not necessary to change the
modem tone settings for NAVTEX reception. The loss due to the slightly
maladjusted shift being in the area of tenths of a dB, and can be
ignored for practical purposes.

When using the usual modem tones of 1400 Hz and 1200 Hz (Low-tones,
**TOnes** parameter 0), the receiver should be set to USB and a
frequency of 516.700 kHz to receive NAVTEX on a center frequency of 518
kHz. For LSB the frequency should be set to 519.300 kHz. Here, the
**TR** parameter should be set to 1 or 3 (See handbook).

Basically, the same conditions for NAVTEX reception are required as for
AMTOR-FEC. The parameters **BC** and **ARX** must both be set to 1.
(these are the default values. Refer to section 6.10 on page 64 and
section 6.6 on page 61).

### AMTEX

The American Radio Relay League (ARRL) has used one system (among
others) for its radio bulletins via HF radio for a number of years,
which closely resembles the maritime NAVTEX system, and follows the same
protocol rules. It is called AMTEX. This amateur radio NAVTEX differs
only in its special definition of possible message types, which have
been adjusted for amateur radio usage. The existing NAVTEX processor in
the PTC-IIpro is thus very suitable for fully automatic reception of
AMTEX transmissions, provided suitable adjustments are made. The
messages are transmitted (as with NAVTEX) in AMTOR FEC ("mode B")
normally from 1800 and 2100 American local time (i.e. 2300 and 0200 UTC
- or one hour earlier during summer time). The AMTEX transmissions take
place on the frequencies of 3625, 7095, 14095, 18102.5, 21095 and 28095
kHz (Mark). The following message types have been defined to date:

|     |                           |
|-----|---------------------------|
| E:  | DX News Bulletin          |
| G:  | General News Bulletin     |
| K:  | Keplerian Data Bulletin   |
| P:  | Propagation News Bulletin |
| S:  | Space Bulletin            |
| X:  | Special Bulletin          |

Table 5.5: AMTEX message types

Generally, "A" is used as the area code (Station ident). Exceptionally,
"S" has been used.

## GPS

The "Global Positioning System" (GPS) has very quickly become a standard
for all areas that require exact positional information e.g. shipping,
in-car navigation systems etc. Today, GPS receivers are cheaply
available and widely used. The PTC-IIpro offers the possibility to link
the GPS technology with PACTOR, and also to PR. It now becomes possible
for example to call up the present position of small ships or deep sea
yachts via shortwave, without requiring a PC to be running on the mobile
station and without a ships radio operator.

**SCS** offers a special Y-cable which which devides the wires from and
to the serial interface of the PTC-IIpro into two parts, so that 2
separate RS232/V24 connections with SUB-D sockets are created (refer to
chapter 17 on page 243). With the help of the Y-cable now both, computer
and GPS-receiver can be connected to the PTC-IIpro.

### Connecting the GPS receiver

The GPS receiver must be connected to the secondary serial port of the
PTC-IIpro. The input and output of the secondary port is brought out to
the normal SUB-D plug of the RS232 interface, and is available from
there.

The secondary port input is connected to pin 4 of the RS232 socket. The
secondary port output is connected to pin 9 of the RS232 socket. (Ground
is connected to pin 5. Do not forget the ground connection!)

SCS offers a special Y cable which splits the leads to and from the
RS232 socket on the PTC-IIpro so that two separate DIN-9 RS232 standard
sockets are available. By using the Y cable, it is possible to connect a
GPS receiver and a PC to the PTC-IIpro without needing a soldering iron.
Refer to chapters 16 page 231 and C4 on page 257 for details.

GPS receivers normally work at a speed of 4800 Bd from their serial NMEA
output. The PTC-IIpro normally operates automatically at 4800 Bd on its
secondary serial port.

If both PR sockets are occupied with a modem, then there is no free
baudrate generator available. In this case the PTC-IIpro uses the
baudrate of the TRX port for the secondary serial port. (Most
transceivers can be set to 4800 Bd for remote control. The typical 4800
Bd for the GPS receiver can be set using the TYpe command in the trx:-
menu, without having to sacrifice the TRX remote control ability.)

|     |                                                                                                                                                                                                  |
|-----|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | Some GPS receivers offer various protocolls for control via the serial port. The PTC-IIpro expects a NMEA compatible GPS receiver. The GPS equipment must therefore be set to "NMEA compatible"! |

### GPS position request

As soon as a GPS receiver is connected, the PTC-IIpro evaluates the
incoming data and saves the actual position with the corresponding (GPS)
time.

The PTC-IIpro accepts messages in formats GPRMC, GPGLL, IIRMC and IIGLL.
RMC has priority over GLL.

The user can call up this position data with the **POSition** command in
the **cmd:**- menu. The **POSition** command is also a remote control
command, and available for use via PACTOR and PR. It can also be called
up by users of the PTC-box.

Hostmode programs can use the channel 249 to directly access the NMEA
data of a connected GPS receiver (refer to chapter 10.8 on page 187).

## APRS[1]

APRS (Automatic Position Reporting System) was developed 1992 from Bob
Bruninga (WB4APR) as a special operating mode of Packet-Radio, as the
name implies, for automatic transfer of position data.

APRS is mainly used for tracking of mobile *objects*. For that the
actual position is read out from a GPS receiver (“GPS” operation). But
also without GPS receiver connected *fix* position data can be
transmitted (“FIX” operation). In this case the position needs to be
entered manually.

The PTC-IIpro operates this mode stand alone and without being connected
to a PC!

To setup the APRS features the command **APRS** in the **pac:** -menu is
available (refer to chapter 9.7.1 on page 152). Also here the parts of
the commands written in capital letters are necessary to enter to invoke
the command. The first argument following the **APRS** command usually
acts as a sub-command and selects a function. The final parametes are
defined with the arguments following this sub-command. If there is no
sub-command given and the nummeric parameter follows directly to the
**APRS** command, then this parameter defines the APRS main mode.

APRS digipeating is not supported directly, but the normal digipeating
features can be used for *simple* APRS digipeating as well. An universal
APRS digipeater can also be established using a free program like
UI-View.

APRS data is always transmitted using the modulation defined with the
command **Baud** (or **%B** in hostmode), (refer to chapter 9.7.2 page
155 and 10.4.26 page 180).

## Robust HF-Packet

Up till now Packet-Radio over shortwave has been basically a
non-starter, has even been heavily criticized because of the low
effective throughput and many repeats due to missing robustness. AX.25
is for shortwave not an ideal protocol, but with automatic **FRack**
setting and a small **MAXFrame** value the protocol should however
function much better on a shortwave channel than has previously been the
case generally.

One cannot of course expect an asynchrone protocol to reach the same
efficiency as a small synchrone ARQ protocol (e.g. PACTOR), but for some
applications a multi user service with very uncritical transmit/receive
switching, as well as almost zero power holding up a connection when no
data passing, brings a real advantage that outweighs the lower data
throughput.

What are the reasons then, that up until now HF-PR works so poorly, and
apart from “forwarding” is hardly ever used? There is a simple answer:
The current modulation type for HF-PR namely uncoded 300 baud FSK is
really unsuitable for normal HF channels. The symbols are much too small
even with moderate “multi path effect” (“delay spread”) to work.
Additionally because no sort of error correction code is used, even
short troughs or “statics” will destroy a many seconds long packet. Just
one missing bit leads to a repeat of the whole transmission.

To overcome this problem **SCS** has developed a new class of robust
modulation types especially for Packet-Radio. As a special feature for
all the variants of this “Robust-PR” a completely new synchronization
algorithm with tracking properties that were not possible before has
been realized. **Frequency deviations of ±250 Hz are immediately
recognized and compensated without any loss of sensitivity**, and this
also with signals that are buried deep in the noise. Because of this it
is possible to remove a tuning display. One can say with good conscience
this is “Plug and Play” for shortwave.

The 3.6 firmware makes available a small band (500 Hz) version of the
“Robust-PR”. A wide band variant (2 kHz) with similar characteristics
and 4 times the speed is in generally possible.

The current “Robust-PR” modulations schemes have the following
characteristics:

Bandwidth: 500 Hz @ -30dB.

Modulation: Pulse-Shaped OFDM (BPSK, QPSK); similar to Pactor-III

Average throughput: 200 or 600 Bits/s (Increase to 1200 Bit/s possible)

Crestfactor: 3.0 or 4.2 dB

Delay-Spread: to ±8 msec can be coped with

Coding: High performance error correction code, “full-frame
interleaved”,

> rate/2 or rate 3/4

## The PR PACTOR Gateway

The PTC-IIpro provides the outstanding featurwe to establish a PACTOR
connection on short wave using Packet-Radio(!) To utilize this feature
in a perfect way, the following requirements have to be fulfilled:

1.  The controller must be able to control the frequency of the HF radio
    independently, without the need of being supported by a PC for this
    purpose.

<!-- -->

1.  The controller must be able to determine by itself in a very
    reliable way if a HF channel is already occupied, to prevent mutual
    interference.

The PTC-IIpro fulfills both requirements: A TRX control port and a
special DSP algorithm for *channel busy* recognition.

To ensure a simple and safe operation of the gateway at link
establishment the PTC-IIpro uses the frequency data as well as other
information of the TRX frequency list. The gate parameter included in
the frequency list determines whether a defined channel is enabled or
disabled for PRPACTOR gateway operation.

This is a typical TRX frequency list:

> CHANNEL-LIST:
>
> =============
>
> Ch Frequency (kHz) Scan Gate Comment
>
> ----------------------------------------------------------
>
> 1: 3583.650 YES NO dl1zam channel 1
>
> 2: 3585.650 YES NO DL1ZAM channel 2
>
> 3: 3584.000 YES YES Test QRG DL1ZAM
>
> 4: 14079.000 NO YES DL2FAK CN2SM
>
> 5: 14076.540 NO NO EA5FIN’s summer QRG
>
> 6: 14075.600 NO YES LA2MV
>
> 7: 14080.000 NO YES 9K2EC special
>
> 8: 3587.000 YES YES SM3HUA QRG
>
> 9: 3595.400 NO YES DJ9YJ QRG
>
> 10: 3588.000 NO YES DKOMAV HB9AK
>
> 11: 14077.000 NO YES second ch d12fak
>
> \*\*\* WARNING: YOUR CALLSIGN WILL APPEAR ON HF/SHORT WAVE!
>
> \*\*\* PLEASE DO NOT USE THE HF-GATE WITHOUT HF-LICENSE!

Display 5.11.1: Typical frequency list

The list can be generated with the **Channel** command in the
**trx:**-menu, refer to chapter 13.1, page 201.

|     |                                                                                                                                                                                                                                                                                                                                                                      |
|-----|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | To access to the PRPACTOR gateway is only allowed for persons that own a valid license to operate on HF bands. The callsign of the gateway user is displayed without additional remarks on short wave! (An extension, e.g. DL2FAK-4, would cause trouble with most of the PACTOR mailbox systems). Access limits can be defined with the help of the Xuser command. |

### TRX command

The **TRX** command allows the standardization of the syntax in
comparison to the PACTOR port. After entering **TRX** List (List needs
not o be entered) a **TRX** frequency list is displayed, the same as on
the PACTOR port.

### Gate command

The **Gate** command is the fundamental command for the usage of the
PRPACTOR gateway. It provides several options:

Entered with no argument the PTC-IIpro displays the TRX frequncy list.

If the argument is a callsign, e.g. **G** DL2FAK \<Return>, the
PTC-IIpro attempts to establish a gateway connect to DL2FAK on
shortwave.

For this purpose the system browses through all comment fields with
enabled Gate parameter of the frequency list (starting with channel 1)
for the callsign (case insensitive). The end of a callsign in the
comment field can be marked with any *non-alphanumerical* special
character, e.g. with a space, comma or something else.

The search mechanism compares the number of characters entered as the
arguments of the **Gate** command. If e.g. **G** DL2FA is entered, the
length to be checked for is defined to be 5 characters. The callsign
*DL2FA* will not be found in the TRX list although DL2FAK is present in
two of the comment fields. The following character behind *DL2FA* in the
comment field is a *K*, which represents an alphanumerical character
(letter or number), so that the search algorithm *notices* that this
can’t be *DL2FA.* If, e.g. DJ9YJ/M is contained in one of the comment
fields, the search algorithm will detekt the right channel when entering
**G** DJ9YJ as well as when entering **G** DJ9YJ/P.

Back to the example of **G** DL2FAK – The PTC-IIpro first of all will
find this callsign in the comment field of channel 4. The appropriate
frequency is 14079 kHz. The system now sends this frequency formatted as
remote control command to the transceiver using the TRX port. It checks
every 5 seconds if the indicated frequency is already occupied and if
free it calls for DL2FAK in PACTOR mode. The maximum calling time is
limited on 1 minute for not to occupy the frequency more than
neccessary.

A typical sequence send for the procedure discussed above is:

> \*\*\* QRX – CHANNEL BUSY TEST ON: 14079.000 kHz
>
> \*\*\* LINK SETUP ON HF / PACTOR...
>
> \*\*\* CONNECTED TO DL2FAK

Display 5.11.2: PRPACTOR gateway message while building a connection

The connection can now be operated in the same manner as in PR, provided
that the PACTOR station performs the CHANGEOVER selfcontrolled after
having transmitted the text, but that’s usual for all mailbox systems as
well as for the PTC-IIpro PACTOR box (Problems with the CHANGEOVER of
the PRPACTOR will be discussed later on).

The connect will be terminated if either the gateway user disconnects
the PR connection or the connected PACTOR station disconnects the PACTOR
link, e.g. after the **Q** command is entered by the gateway user to
request the disconnect by the distant station. In this case the command
prompt of the PTC-PR box will be displayed, ready to accept new
commands, e.g. another gateway command.

|     |                                                                                                                                 |
|-----|---------------------------------------------------------------------------------------------------------------------------------|
|     | The PACTOR connection established by a gateway command will be terminated automatically if the link is inactive for 10 minutes. |

If the HF port is occupied when entering the **Gate** command the PTC
indicates this with displaying the following message:

> \*\*\* BUSY fm HF-GATE
>
> \*\*\* TRY AGAIN LATER...

Display 5.11.3: PRPACTOR gateway message if the HF port is occupied.

If the system notices at checking the HF channel that it is already
occupied, the following message is displayed:

> \*\*\* QRX – CHANNEL BUSY TEST ON: 14079.000 kHZ
>
> \*\*\* HF CHANNEL ALREADY OCCUPIED!

Display 5.11.4: PRPACTOR gateway message if the channel is occupied.

In this case the system automatically resumes browsing through the
comment fields, searching for the given callsign. In the example the
PTC-IIpro will find the callsign DL2FAK again in channel 11 and tries
again to establish a PACTOR connection if the channel is not occupied.

If the callsign does not appear anymore in the TRX list, the system
stops activity.

**Note:** If the longpath option shall be used, it is necessary to enter
an exclamation mark in in front of the callsign – same in the comment
field!

If as third argument after the callsign the channel number is entered,
no search for the callsign in the comment fields will be done, the
PTC-IIpro starts building up the PACTOR connection directly on the
entered channel as described in the last chapter.

Entering **G** !DL6MAA 7 in the TRX frequency list mentioned before
results in attempts of the system building up a longpath PACTOR link to
DL6MAA on 14080 kHz. The entered channel has to be enabled by setting
the Gate parameter in the TRX frequency list for gateway operation.

PRPACTOR gateway connections are indicated in the internal log of the
gateway PTC-IIpro with the preamble “G1:” or “G2:” depending on the
level of the corresponding PACTOR connection.

### CHANGEOVER problems

As explained in chapter “PACTOR Duplex” the PR needs in contrast to
PACTOR no special changeover characters, that means for example that no
\<CTLR-Y> is necessary to change the direction. If a PR link and a
PACTOR link are connected together, a principle conflict comes up: It is
unreasonable for the PR user to enter *blind* any change of direction
control character for the PACTOR link taken part of the connection.

As long as the PACTOR station connected to a PR user via the PRPACTOR
gate executes independently a BREAKIN before text to be send and
executes a CHANGEOVER after any text was send, the acting together with
the PR station works perfectly. That means that if a PACTOR station is
called as a mailbox the PRPACTOR gate works without problems.

But if a PACTOR station is called which doesn’t control automatically
the changeover, the PACTOR end user has to take over the whole over
control manually! That’s in case not possible, if the called PACTOR
station works without operator and isn’t configured as a mailbox.

Alternative for this handling we suggest to switch the PTC-IIpro gateway
in PACTOR Duplex mode (refer to chapter 6.71). But that’s not the
cure-all, because it might be possible that on the other hand some
PACTOR mailbox systems can’t work with the PACTOR Duplex mode without
problems (refer to chapter 5.12.2, “How to avoid incompatibility?”)

## PACTOR Duplex and PACTOR data transparency

To simplify the PACTOR operation mode, that means to ensure
*compatibility* to many mailbox and terminal programs made for
Packet-Radio (PR) while using PACTOR, the possibility of working without
the usage of special control key sequences (e.g. \<Ctrl> + \<Y>) had to
be created. Programs written for PR do not know the commands for
changeover used in the half-duplex mode on shortwave, because PR reacts
in the half-duplex mode on the user interface more or less like
full-duplex – a changeover does not exit for PR.

To avoid changeover commands using PACTOR the PTC-IIpro offers a
CHANGEOVER-automatism , the so called PACTOR Duplex.

The PACTOR duplex is activated with the new command **PDuplex** (refer
to chapter 6.71, page 95). The automatism works with the following
relatively simple algorithm:

1.  If the PTC-IIpro is the information sending station (ISS), that
    means controls the keys, the PTC-IIpro automatically executes a
    CHANGEOVER, if his transmission buffer is empty (that means no data
    to be sent are available).

<!-- -->

2.  If the PTC-IIpro is the information receiving station (IRS), the
    PTC-IIpro automatically executes a BREAKIN, if the transmission
    buffer is not empty, that means that data for transmission are
    available and the IRS state exists for at least 12 seconds.

This automatism causes a variety of conclusions during practical
operation that have to be mentioned, especially if the PTC-IIpro with
activated PACTOR Duplex has to work together with a *conventional*
PACTOR system.

The general usage of the PACTOR Duplex mode is not recommended at the
moment, because especially *old* PACTOR mailbox systems have problems
with the *unnecessarily* automatically executed changeover of the
PDuplex-PTC. The conventional operation control in the personal
*Chat-QSO* should only be switched to PACTOR Duplex mode, if the QSO
partner is familiar with what happens and will not be confused by the
change-overs of the PACTOR Duplex-PTC appearing accidentally.

The following distinctiveness exists for the PTC-IIpro itself when
switched to PACTOR Duplex:

1.  The CHANGEOVER bell is generally deactivated.

<!-- -->

3.  Open files for the PTC internal mailbox will not be closed by a
    CHANGEOVER any more.

4.  Mailbox access of users with PACTOR Duplex are executed correctly
    (the command interpretor will not be closed as usual by a
    CHANGEOVER, but generally by a *Carriage Return*).

### Application for PACTOR Duplex

1.  PDuplex can be used excellently to make mailbox programs for PR
    working with the WA8DED hostmode (**DPBox**, **DieBox**, **GP**,
    **WinGT**, etc). also usable for PACTOR. The terminal- and mailbox
    program does not notice on the WA8DED hostmode side any difference
    between a PACTOR– or PR-link, if PDuplex is activated. No
    transmission control character has to be send by the PC.

    The great advantage of these technique:

> The PR program used by a mailbox is compatible to **all** PACTOR
> users, independently if they use PACTOR Duplex or not. ( It also
> doesn’t matter if a user accesses to the mailbox with PACTOR-I or
> PACTOR-II).

5.  In combination with binary data transparency binary files can now be
    transmitted directly - e.g. in the Autobin mode via PACTOR – without
    the detour using 7PLUS or other coding mechanisms. If a file shall
    be transmitted to a friend using the PTC-IIpro too, both PTC-IIpro
    are switched to PACTOR Duplex. Using a WA8DED hostmode program all
    features available for PR can be used on the PACTOR channel (usually
    channel 4) as well– certainly also the AUTOBIN transfer!

6.  Very convient operation with partners using PACTOR Duplex too. In
    this case the QSO can be made in the same way as in PR – regardless
    of the actual *transmission state* of the connected PTCs. CHANGEOVER
    or BREAKIN aren’t necessary anymore.  
    We want to point out that the selection of the QSO style is a matter
    of taste. The usual operation with manual control of the
    transmission direction is useful furthermore.

### How to avoid incompatibility?

PACTOR Duplex allows to experiment a lot, especially using PC software
intended for Packet-Radio. Unfortunately side effects arise from using
the duplex simulation together with *old* PACTOR systems.

|     |                                                                                                                                                                                     |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | In general the PACTOR Duplex should be switched off before using a PACTOR mailbox - if it is not definitely clarified that the mailbox is able to operate with PACTOR Duplex users. |

Also the internal mailbox of the PTC-IIpro reacts incorrect (if the
PTC-IIpro isn’t switched to PACTOR Duplex), if a CHANGEOVER is executed
while entering commands – e.g. when the user operates PACTOR Duplex but
enters the command very slowly.

**It would be desirable if all of the mailbox programs for PACTOR could
be modified in the way that they could also operate with PACTOR Duplex
users without problems.**

### PACTOR data transparency

The PACTOR Duplex mechanism and the data transparency structure of the
WA8DED hostmode make it useful for other applications to fulfil the
demand (already mentioned from many users) for data transparency for
PACTOR. As already mentioned the transparency in combination with PR
programs allows the usage of binary transfer protocols via PACTOR.

Using the WA8DED hostmode the PTC-IIpro sends and receives data in
PACTOR absolutely binary data transparent.

|     |                                                                                                              |
|-----|--------------------------------------------------------------------------------------------------------------|
|     | Data transparency is only achieved if both sides use the PTC-IIpro with the firmware version 2.4 and higher. |

The data transparency certainly includes all characters being attached
to special functions in the terminal mode. The consequence is:

Using the hostmode the CHANGEOVER character or the BREAKIN character
does **not** cause any change of direction at the PACTOR connection
anymore. (Keyboard macros, e.g. in **GP**, which generate these special
characters are ineffective!). In the hostmode for changeovers the
commands **%O** or **%I** have to be used.

## Audio Functions

For special processing and filtering of Audio signals (Audio from the
Transceiver) the PTC-IIpro presents its own submenu - the so called
Audio-Denoiser menu, **aud:**-menu. The PTC-IIpro is thus also suitable
for SSB operation (automatic notch filter) and for CW listening
(Automatic peak-filter, CW-filter) and has very useful options. The
Audio is presented to the PTC as usual via PIN 4 of the 8 PIN HF radio
connector, so that no changes compared with normal RTTY/PACTOR operation
are required. The processed or filtered signal is presented at PIN 1 of
the HF radio connector, and at PIN 11 of the 13 pin DIN-connector
(TRX-REMOTE-CONTROL).

The very high computing capacity of the PTC-IIpro is shown to be very
advantageous for the Audio processing algorithm. In comparison to the
usual simpler and cheaper Audio Denoiser units, several times as much
computing power can be used to optimize the result.

All functions of the **aud:**-menu that process the AF input signal use
a 4-stage signal level matching (22 dB adapting range) for the 16-Bit
A/D converter in order to keep the quantization effect low and to
provide a large effective dynamic range. The PTC-IIpro therefore adjusts
itself in stages automatically to the average signal level delivered
from the transceiver. A complete description of the **AUdio** commands
set is given in section Audio (refer to chapter 7, page 119)

## The hostmode

The PTC-IIpro supports the **WA8DED** hostmode and an **SCS** specific
extension, the CRC hostmode. For detailed information about the hostmode
and the hostmode commands refer to chapter 5.14, page 57. Pay attention
to the explanations concerning the **TNC** command (refer to chapter
6.96, page 108).

Here you find some important details for the hostmode and PACTOR
cooperation.

To make PACTOR accessable from the hostmode, one of the hostmode
channels can be reserved for PACTOR operation. On this reserved channel
a connect or disconnect command of the hostmode program is effective on
the short wave port of the PTC-IIpro and establishes a PACTOR connection
or terminates it. If the PACTOR listen mode is activated, incoming text
will also be displayed in this channel and not in the monitor-screen of
the hostmode program.

With the **PTChn** command the hostmode channel for PACTOR can be set.
Default setting is channel 4. If more than one channel is enabled in the
hostmode program, it is usual to take the last channel.

If your hostmode program has 8 channels enabled, the command

**cmd:** **PTChn** 8 \<Return>

reserves channel 8 for PACTOR.

As the example shows it is only possible in the terminal mode, e.g. in
**PlusTerm**, to enter the **PTChn** command.

As mentioned in the chapters about PACTOR Duplex and the PRPACTOR
gateway the hostmode programs naturally have problems with the usual
special characters for the changeover in PACTOR (CHANGEOVER and
BREAKIN). Because of this there are special hostmode command which allow
the changeover for PACTOR in the hostmode: **%O** causes a CHANGEOVER
and **%I** causes a BREAKIN.

Another comfortable way to initiate a CHANGEOVER in the hostmode is to
use the command **HCr** (refer to chapter 6.44, page 81). If **HCr** is
1 the PTC-IIpro executes a CHANGEOVER for each line feed at a blank
line. That’s convient for direct QSOs.

The PACTOR listen mode can be switched on and off with the hostmode
command **%L**.

|     |                                                                                                                                                                                                                           |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | The **JHOST** command is not allowed in the initialization file of the hostmode program! Only the commands mentioned for hostmode (refer to chapter 10) should be used in the initialization and de-initialization files! |

|                                                                                                                                                                                                |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| If you want to use the PTC-IIpro after power-on directly with a hostmode program, you should set the baudrate with the **SERBaud** (refer to chapter 6.87, page 100) command to a fixed value. |
