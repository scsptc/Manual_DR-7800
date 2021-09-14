# Commands

**In this and in the following chapters, only those commands are described which have a function in the P4dragon DR-7800. All other commands displayed with the [`Help`](#help) command were implemented purely for reasons of compatibility and are currently without any function.**

[[_TOC_]]

## ADECoder

### ADEC All
|                  |     |                  |
|------------------|-----|------------------|
| Default setting: | 1   |                  |
| Parameter:       | 0   | Auto decoder off |
|                  | 1   | Auto decoder on  |

Enables the general deactivation of the auto decoder, regardless of the mode-dependent parameters (`Navtex`, `Pactor`, `Rtty`). If the `ADEC All` parameter is set to 0, the auto decoder is completely switched off. If, on the other hand, the `ADEC All` parameter is set to 1, the mode-dependent parameters determine whether the respective auto decoder (e.g. for Navtex or RTTY or PACTOR) is active or inactive.

### ADEC Navtex

|                  |     |            |
|------------------|-----|------------|
| Default setting: | 1   |            |
| Parameter:       | 0   | Navtex off |
|                  | 1   | Navtex on  |

Determines whether the Auto Navtex decoder is switched on or off.

### ADEC Pactor

|                  |     |            |
|------------------|-----|------------|
| Default setting: | 1   |            |
| Parameter:       | 0   | PACTOR off |
|                  | 1   | PACTOR on  |

Determines whether the Auto PACTOR decoder is switched on or off.

### ADEC Rtty

|                  |     |          |
|------------------|-----|----------|
| Default setting: | 1   |          |
| Parameter:       | 0   | RTTY off |
|                  | 1   | RTTY on  |

Determines whether the Auto RTTY decoder is switched on or off.

### ADEC Buffer

|                  |      |             |
|------------------|------|-------------|
| Default setting: | 1000 |             |
| Parameter:       | X    | 0 to 20,000 |

The parameter value determines how many characters are to be read from the auto-decoder text buffer (into which all received data of the auto-decoder based on the FIFO principle with a FIFO length of 20000 bytes) should be read. So you can read out the last 2000 characters received by entering the command `ADEC B 2000`.

Without an argument, the last 1000 characters are always output. If fewer characters have been received since the last modem reset (power-on) than are to be output, the text received so far is output in full.

### ADEC Delay

|                  |     |                   |
|------------------|-----|-------------------|
| Default setting: | 30  | Seconds           |
| Parameter:       | X   | 10 to 300 seconds |

Determines the time in seconds until the display switches back to the previously selected display mode after the end of a reception process by the auto decoder (and automatic switchover to *Small Waterfall*).

Wenn z. B. der normale *große* Wasserfall als Display-Mode eingestellt ist, schaltet das Display bei Navtex-Empfang automatisch auf *Kleinen Wasserfall* um und gibt den Empfangstext in der unteren Hälfte des Displays wieder. Nach dem Ende des Navtex-Empfangs bleibt diese Darstellung per Voreinstellung noch 30 Sekunden erhalten (der Text kann gele sen werden), bis schließlich wieder auf *großen* Wasserfall (ohne Textbereich) umgeschaltet wird.

For example, if the normal *large* waterfall is set as display mode, the display automatically switches to *small waterfall* when receiving Navtex and shows the received text in the lower half of the display. After the end of the Navtex reception, this display is retained for 30 seconds by default (the text can be read), until it finally switches back to *large* waterfall (without text area).

Steht der Display-Mode auf dem Wert 2, hat der ADECoder Delay-Parameter keine Bedeutung.

If the display mode is set to 2, the ADECoder delay parameter has no meaning.


## Amtor

This command activates the AMTOR command prompt. 

The following system message is output for better differentiation:
```
AMTOR/DRAGON V.2.40 (C) 1994-2021 SCS GmbH & Co. KG
===================================================

**-A-** (SCSP):>
```
The system responds with the command prompt:

`**-A-** (SCSP):>`

The Navtex transmissions received by the auto-decoder are only output when the Amtor prompt is activated.

Otherwise the Amtor prompt has no function at the moment. The Amtor-ARQ operating mode is not implemented!

You can return to the **cmd:** prompt with the [`PT`](#pt) command.


## ANotch

|                  |     |                        |
|------------------|-----|------------------------|
| Default setting: | 1   |                        |
| Parameter:       | 0   | PACTOR-4 Autonotch off |
|                  | 1   | PACTOR-4 Autonotch on  |

This is a newly developed, minimal-phase, real 6-fold Autonotch filter that very effectively removes narrowband interference.


## AUdio

The `AUdio` command (without argument) activates the [Audio menu](Audio.md)
(**aud:**-menu). The command prompt takes the form **aud:**.

Within the **aud:**-menu the following commands are available:
```
AUXInput, CHannel, COpy, COPYGain, DD, Help, Level, Quit, Through, TOne
```
All other (*normal*) commands are not available!
You can leave the **aud:**-menu with the [`Quit`](Audio.md#quit) or [`DD`](Audio.md#dd) command.

The `AUdio` command can also be followed by an argument, namely a command
from the **aud:**-menu. In this case the PTC only executes this one Audio
command without switching to the **aud:**-menu.
The command is passed through, so to speak.

Directls set the [speaker audio output level](Audio.md#level) to 40:
```
cmd: AUdio Level 40<Return>
```
The [Audio commands](Audio.md) are described in detail in a [separate chapter](Audio.md).


## BAUdot

After **BAU**, the PTC answers with:

`>>> BAUDOT--RTTY RECEPTION ACTIVE -- SPEED: 45 BD <<<`

The RTTY transmissions received by the [auto decoder](#adecoder) are only output when the RTTY prompt is activated.

Otherwise the RTTY prompt has no function at the moment. The RTTY operating mode is not implemented!

You can return to the **cmd:** prompt with the command [`Quit`](#quit) or [`PT`](#pt).


## BKchr

|                  |             |                                                  |
|------------------|-------------|--------------------------------------------------|
| Default setting: | 25 (Ctrl-Y) |                                                  |
| Parameter:       | X           | 1... 127, ASCII code of the character (decimal). |

Defines the BREAKIN character used for PACTOR and AMTOR.

The BREAKIN character is a special command for a forced direction change
from RX to TX (BREAKIN). Because this command is used very often, the
PTC accepts the BREAKIN character only directly in the converse mode,
that means that the command can not be used after the **cmd:**-prompt.

The BREAKIN character may be changed to any other convenient character
with this command at any time.

\<Ctrl-B> as BREAKIN character is defined with the command: `BK 2`.

The following characters are not permitted: 8 (Backspace), 13 (CR), 32
(Space), 30 (IDLE), 17 (XON), 19 (XOFF), and other already specified
special characters.


## BRightn

|                  |     |                           |
|------------------|-----|---------------------------|
| Default setting: | 6   |                           |
| Parameter:       | X   | 1... 7, brightness value. |

This command was only retained to achieve the maximum possible compatibility with existing PC software.

The brightness of the OLED display on the P4dragon DR-7800 should be controlled using the [`DISPlay BRight`](#disp_bright) command.
However, the brightness values between `BRightn` and [`DISPlay BRight`](#disp_bright) are converted into one another.

## BT

The `BT` command (without argument) activates the [Bluetooth menu](Bluetooth.md)
(**bt:**-menu). The command prompt takes the form **bt:**.

Within the **bt:**-menu the following commands are available:
```
Help, ID, MAC, PASSKEY, Quit
```
All other (*normal*) commands are not available!
You can leave the **bt:**-menu with the [`Quit`](Bluetooth.md#quit) command.

The `BT` command can also be followed by an argument, namely a command
from the **bt:**-menu. In this case the PTC only executes this one Bluetooth
command without switching to the **bt:**-menu.
The command is passed through, so to speak.

Directly set the [Bluetooth passkey](Bluetooth.md#passkey) to 5678:
```
cmd: BT PASSKEY 5678<Return>
```
The [Bluetooth commands](Bluetooth.md) are described in detail in a [separate chapter](Bluetooth.md).


## CBdetector

|                        |     |                     |
|------------------------|-----|---------------------|
| Default setting:       | 0   |                     |
| Parameter:             | 0   | Normal.             |
|                        | 1   | Emphasizing PACTOR. |
|                        | 2   | PACTOR only.        |

The Channel Busy Detector is a very sensitive and selective way of detecting
the current channel occupation of a PACTOR channel. This prevents the channel
from being used twice, i.e. new call attempts on channels that are already in use.
This is e.g. very advantageous in the radio-only RMS project of the Winlink system.

There is a universal FFT detector that is sensitive for spectral peaks and there are special PACTOR selective P1/P2/P3/P4 detectors.

On `CB 0`, all detectors work in parallel, the FFT detector looks for spectral *anomalies* (channel occupancy) through the entire 300-2700 Hz frequency range.

On `CB 1`, the FFT detector only checks the frequency range 1500-1700 Hz in order to detect narrow bandwidth P1/P2 signals that could not yet be detected by the PACTOR sensitive detectors.

On `CB 2`, the FFT detector is completely switched off. The modem only looks for PACTOR signals.


## CHOchr

|                  |             |                                              |
|------------------|-------------|----------------------------------------------|
| Default setting: | 25 (Ctrl-Y) |                                              |
| Parameter:       | X           | 1... 127, decimal ASCII code of a character. |

Defines the CHANGEOVER character.

`CHOchr` defines the CHANGEOVER character which is a special command
for the change from TX to RX. Because this command is used very often,
the modem accepts this character only in the converse mode, and not after
the **cmd:**-prompt. The CHANGEOVER character is not part of the
transmitted data and will not be transmitted.

A CHANGEOVER initiated by the TX operator is not executed until all text
in the transmit buffer is transmitted.

The CHANGEOVER character can be changed at any time using the `CHOchr` command.

Using \<Ctrl-Z> (entering \<Ctrl> \<Z>) as a CHANGEOVER characters is
defined with the command `CHO 26`.

Illegal values are 13 (CR), 32 (Space), 30 (IDLE), 17 (XON), 19 (XOFF),
and other previously defined special characters.


## CLr

Deletes the transmit buffer. Everything that is contained in the
transmit buffer, which has not yet been transmitted, is deleted.


## CMsg

|                        |     |                   |
|------------------------|-----|-------------------|
| Default setting:       | 0   |                   |
| Parameter:             | 0   | Connect test off. |
|                        | 1   | Connect text on.  |

This command turns the [connect text](#ctext) on or off.


## CONIntegrity

|                        |     |                          |
|------------------------|-----|--------------------------|
| Default setting:       | 0   |                          |
| Parameter:             | 0   | Normal.                  |
|                        | 1   | Reduced error tolerance. |

If set to 1, the Robust Connect (SLAVE side) is searching for incoming calls
with less error tolerance. The required minimum SNR for establishing a PACTOR
connection increases by roughly 2 dB, but the (already very low) probability
of *false connects* is further reduced significantly.


##  Connect

|                  |                  |                                              |
|------------------|------------------|----------------------------------------------|
| Default setting: | previous address |                                              |
| Parameter:       | ADDR             | Callsign of the station you want to connect. |
|                  | !ADDR            | Starts a long path call                      |
|                  | %ADDR            | Starts a call using *Robust Connect*         |

Used to establish a PACTOR connection. The `Connect` command may be followed
by the argument being the callsign of a distant station. The callsign
length can vary between 2 and 8 characters. Too short arguments are
ignored. If the callsign is too long it will be truncated at the end.

If the argument is missing, the previous callsign (including Longpath or Robust flag) is used.

`Connect` can be repeated at any time with a new argument as long as there is no connection.

In the connected condition, the `Connect` command can
be used to display the callsign of the distant station.

If no response is received after the number of retries set by the
[`MAXErr`](#maxerr) command, the modem terminates the connect attempt automatically
with displaying an error message. A call can be stopped manually using
the [`Disconnect`](#disconnect) command.

### Longpath-connect

With an exclamation mark (!) or a semicolon (;) is set directly before
the callsign (example: `C !DL0WAA`) it is possible to call using sync
packets with long path options. The cycle time increases to 1.4 seconds
and the control delay becomes long enough for ARQ contacts to over
40,000 km (TRX-Delay 25 ms).

PTC1 systems (Z80-PTC) with a firmware version number \<1.3 are not able
to detect syncpackets with long path options and don’t react on long path
calls. During connections using the long path option the throughput decreases
to approximately 90% of the usual throughput.

### Robust-connect

The *Robust Connect* allows reliable link establishment even under extremely
poor and difficult signal conditions.

A *Robust Connect* can be started by prefixing the call sign (argument
of a connect command) of the distant system with a "%" sign, e.g.:

`cmd: C %DL1ZAM<Enter>`

This is also valid for WA8DED hostmode. In terminal mode the modem
will respond as following:

`*** NOW CALLING DL1ZAM (ROBUST CONNECT)`

The *Robust Connect* uses normal PACTOR timing. Longpath option and
*Robust Connect* **cannot** be combined! The call sign of the remote
station may only be prefixed by **%** OR **!**.

### Direct frequency entry

With starting a PACTOR connect, optional a frequency value (separated by
a comma) can be entered after the target callsign. This is valid for the
connect command in the terminal mode as well as in the hostmode.

`cmd: C dl1zam,3582.60<Return>`

In this example first of all the modem will send the frequency information
to the transceiver, the transceiver sets the VFO to 3582.600 kHz and starts calling (on
this frequency). To use this function the transceiver must be capable to
be remote-controlled using the TRX remote control option of the
P4dragon DR-7800. The remote control parameter have to be set correctly
using the [`TYpe`](TRXctrl.md#type) command of the [**trx:**-menu](TRXctrl.md).

This notation is very handy for simple callsign lists with the
corresponding frequency information. The list entries directly can be
entered as Connect arguments. Also the manual input of the frequencies
should be convient enough.


## CONType

|                        |     |                                |
|------------------------|-----|--------------------------------|
| Default setting:       | 3   |                                |
| Parameter:             | 0   | Accepts no connects            |
|                        | 1   | Accepts only *normal* connects |
|                        | 2   | Accepts only *robust* connects |
|                        | 3   | Accepts all connects           |

With `CONType` you determine which connect variants are accepted by
the P4dragon DR-7800 in the standby mode, i.e. lead to a connection being established.

## CSDelay

|                  |   |                               |
|------------------|---|-------------------------------|
| Default setting: | 5 |                               |
| Parameter:       | X | 1... 31, delay in X • 5 msec. |

Selection of time delay between the end of the RX packet, and start of
the first CS data bit. The time equals the value X multiplied by 5
milliseconds. The parameter influences the response time (controls) of
the RX at RX start. With a large value for `CSDelay`, even
transceivers that have slow transmit-receive switching can be used for
PACTOR. The maximum distance that can be covered is reduced due to the
time delay caused by the final speed of radio waves. DX is only possible
with fast transmit-receive switching.


## CTExt

|                  |   |                                            |
|------------------|---|--------------------------------------------|
| Default setting: |   | "Hello from P4dragon, Terminal offline..." |
| Parameter:       | X | String of max. 249 characters.             |

The connect text is transmitted when [`CMsg`](#cmsg) is set to 1 and the modem receives a connect.
In this case the modem immediately switches into TX mode and transfers the connect text to the calling station.

As the `CTExt` input happens using the command interpreter, one convention for the \<CR>- character
has to be followed: A \<CR> is represented in the `CTExt` string by a '#'.

Example:

to achieve the connect text
```
This is DL6MAA
The terminal is not active at the moment!

73 de Peter.
```
you have to enter the command
```
cmd: CTE This is DL6MAA#The terminal is not active at the moment!##73 de Peter.<Return>
```

## CTrlchr

|                  |             |                                              |
|------------------|-------------|----------------------------------------------|
| Default setting: | 22 (Ctrl-V) |                                              |
| Parameter:       | X           | 1... 127, decimal ASCII code of a character. |

Defines the Ctrl character.

If the Ctrl character is immediately followed by a-z (or A-Z), the PTC
will transmit a control code (ASCII 1-26) via HF channel. With this
simple convention, control characters that are used by your own terminal
can also be sent to the other station.

If CTRL-W should be transmitted to the other station, the following keys
have to be entered: \<Ctrl-V>\<W>

It is recommended to put all definable control characters in the control
block.

XON and XOFF (Ctrl-Q / Ctrl-S) can not be transmitted!

## CWid

|                          |     |                                                                |
|--------------------------|-----|----------------------------------------------------------------|
| Default setting:         | 1 0 |                                                                |
| Parameter 1:             | 0   | CW identification disabled.                                    |
|                          | 1   | CW identification enabled only for PACTOR ARQ.                 |
|                          | 2   | CW identification enabled for PACTOR ARQ and Unproto.          |
|                          | 3   | CW identification enabled for PACTOR ARQ, Unproto, AMTOR ARQ.  |
|                          | 4   | CW identification enabled only for PACTOR ARQ (refer to text). |
|                          | 5   | CW identification enabled for PACTOR ARQ, Unproto, AMTOR ARQ.  |
| Parameter 2:             | 0   | No delay.                                                      |
|                          | 4   | 6 second delay.                                                |

Automatic CW identification is given after a transmission of
approximately 7 minutes and after QRT. The CW identification is keyed
with the PTT line. The FSK output remains at the Mark frequency during
the CW Transmission. The AFSK signal amplitude is also keyed. The
frequency for AFSK is defined by the `Center` command in the Audio
menu (refer to chapter 7, page 119). The speed is set with the
`CWSpeed` command.

With `CWid` 1-3, the CW identification is only given at QRT if it is
self initiated. With `CWid*` 4 and 5, it does not matter which station
initiated the QRT procedure.

In this case the second parameter could be switched to Audio-Only CW
identification. That means that the PTT will be active during the whole
CW identification process and only the audio signal is switched on/off
in the rhythm of the CW signal. The CW identifications uses the Mark
tone.

For CW identification, one's own callsign (`MYCALL`) is always used.

The CWID amplitude is generally 3 dB lower than the FSKA level!


The second parameter in the `CWid` command is used for a 6-second delay of the CWID. If the parameter is set to 4, the CWID is delayed by 6 seconds after last PACTOR packet has been sent during link termination.


## DAte

|                  |          |               |
|------------------|----------|---------------|
| Default setting: |   none   |               |
| Parameter:       | DD.MM.YY | Desired date. |

`DAte` is used to set or read the PTC calendar. If `DAte` is entered
without a parameter, the modem displays the current date.

All positions have to be entered. Leading zeros must not be omitted. The
periods for separation are not necessary. Faulty inputs cause incorrect
programming of the clock!

From 01.01.1990 up to 31.12.2089, the day of the week is automatically
calculated from the date.

**Example**: set date to Sunday, March 24th 1999.

`cmd: DA 24.03.99<Return>`

Or in shortform

`cmd: DA 240399<Return>`


## DD

This command causes an immediate breaking off of the transmission
('**D**irty **D**isconnect'). An existing link is not correctly
terminated. Any text that remains in the transmit buffer is discarded.

`DD` leads, in all cases, back to the respective STBY level..


## Disconnect

An existing link (including Unproto) is closed down correctly. If any
text is still in the transmit buffer, this is first transmitted, then
the PTC starts the QRT sequence.


## DISPlay

The `DISPlay` command can be used to control all aspects of the P4dragon DR-7800's OLED display.
A brief overview of possible arguments can be obtained, as usual, with the command
`cmd: Help DISPlay<Return>`
or simply
`cmd: DISPlay<Return>`

### General

The middle of the frequency range is clearly marked by a specially thick (slightly arrow shaped) marker. This serves especially for 1200 and 2400 Hz bandwidth for easier adjustment (on the center frequency used of 1500 Hz)

Further there are small markers approx. ±100 Hz around the center frequency so the symmetrical setting of signals with 170 / 200 Hz shift is made easier.

A specialty in mode 1 (Spectrum) is that an AGC tries to place the spectral peaks at the upper end of the display range. This eases the correlation between the spectral peaks and frequency values, as the frequency scale is brought to the upper end of the spectrum. With very high [`DISP Smoothing`](#disp_smoothing) values for and with white noise for example, an almost smooth null line at the upper end of the spectrum display range.

### DISP Mode

|                  |     |                 |
|------------------|-----|-----------------|
| Default setting: | 0   | Waterfall       |
| Parameter:       | 0   | Watefall        |
|                  | 1   | Spectrum        |
|                  | 2   | Small Waterfall |

Switches between *Waterfall*, *Spectrum* and *Small Waterfall* Display. If the `Mode 2` (*Small Waterfall*) is used, the lower half of the display remains free for text output. Here, for instance, appears text that is generated by the [Auto-Decoder](#adecoder). `Mode 2` is especially useful if the output of the Auto-Decoder should permanently be displayed, i.e. when RTTY, Navtex and/or PACTOR-1 transmissions are monitored.

### DISP Autodimm

|                  |    |                           |
|------------------|----|---------------------------|
| Default setting: | 2  |                           |
| Parameter:       | X  | 0... 10, time in minutes. |

Controls the automatic display dimmer. The value 0 switches the dimmer off; the OLED display is never automatically dimmed. Values greater than 0 are interpreted as minutes. After this time, the OLED display is dimmed to its lowest brightness value. At every command input and every PACTOR link start, the brightness of the display is returned to the preset brightness value. The time to the automatic dimming is then set again.

`Autodimm` is mainly useful when the modem is in continuous operation. Very long operation of the OLED display with full brightness and always the same display can cause unwanted loss of brilliance (aging) of the pixels used (*burn-in* effect).

### DISP Bandwidth

|                  |       |                                   |
|------------------|-------|-----------------------------------|
| Default setting: | 2400  |                                   |
| Parameter:       | X     | 1200, 2400, 4800 bandwidth in Hz. |

Sets the frequency range for the Waterfall and Spectrum display.

| Bandwidth | Range |
|-----------|-------|
| 1200      | 1500 Hz ± 600 Hz |
| 2400      | 1500 Hz ± 1200 Hz |
| 4800      | 2400 Hz ± 2400 Hz |

### DISP BRight

|                  |    |                            |
|------------------|----|----------------------------|
| Default setting: | 15 |                            |
| Parameter:       | X  | 1... 15, brightness value. |

Sets the OLED brilliance. Corresponds with the normal [`Brightn` command](#brightness)
in **cmd:**-main menu. If the parameter (range 1 – 7) is changed in the main menu, then this relates also to the parameters in the DISP menu and vice-versa. `DISP BR` = (`BR` * 2) + 1.

### DISP COndisp

|                  |     |                               |
|------------------|-----|-------------------------------|
| Default setting: | 1   |                               |
| Parameter:       | 0   | Show only minimal link status |
|                  | 1   | Show detailed link status     |

Sets the operating mode of the display during a PACTOR link. The value 1 has
the effect that during a link, a detailed link status is displayed.
The value 0 however causes only a minimal link status display in the upper display line.
The display does however, even in this operating condition, show the waterfall or spectrum during a link.

### DISP DIMMOFF

|                  |     |                               |
|------------------|-----|-------------------------------|
| Default setting: | 0   |                               |
| Parameter:       | 0   | Display stays on              |
|                  | 1   | Display turned off after dimm |

This is usefull for 24/7 operating stations to preserve the display.
With `DIMMOFF` set to 1 the OLED display is turned off after the dimming sequence.
This prevents burn-in effects of the OLED display!

### DISP DIMMCON

|                  |     |                               |
|------------------|-----|-------------------------------|
| Default setting: | 1   |                               |
| Parameter:       | 0   | Do not dimm while connected   |
|                  | 1   | Dimm display while connectd   |

Determines whether the display should be dimmed or switched off during an existing connection.

### DISP Speed

|                  |   |                     |
|------------------|---|---------------------|
| Default setting: | 0 |                     |
| Parameter:       | X | 0.. 3, speed value. |

Sets the update speed (or the number of FFTs / second). Effects both modes.
The higher the speed, then the slower (naturally) is the resolution in the frequency
direction (only *washed out* spectral details can be seen). In the waterfall display (mode 0),
higher speed values give a higher waterfall *flow speed* (scroll speed). However, the resolution is less.
In the spectrum display (mode 1) a higher speed produces a poorer resolution (*round spectrum*):
the higher display change frequency however is only useful for signals with fast spectral changes and
additionally with a relative low setting of the `Smoothing` parameter.

### DISP SMoothing

|                  |    |                                   |
|------------------|----|-----------------------------------|
| Default setting: | 15 |                                   |
| Parameter:       | X  | 0.. 63, spectrum smoothing value. |

Functions only with spectrum display (mode 1). Sets the averaging effect in the time direction.
The larger the Smoothing value, the slower the spectrum changes – short time changes are increasingly
smoothed out with higher Smoothing values, and disappear. Only longer lasting spectral parts are displayed.
High smoothing values can thus serve to average the spectrum over a longer time frame, thus freeing it
from short term fluctuations. It is thus possible for instance to detect even a very weak sine wave signal under noise.

The smoothing parameter does not work linearly. A high Smoothing value gives increasingly greater averaging.
The value 63 works approximately double so strongly as the value 62. A number of values should be tried for optimum results.

### DISP SMAllfont

|                  |     |                |
|------------------|-----|----------------|
| Default setting: | 1   |                |
| Parameter:       | 0   | Use 6x8 font.  |
|                  | 1   | Use 4x6 font.  |

Configures whether the text on the display for monitor text (PR, RTTY, PACTOR, Navtex) in the lower half of the display outputs is shown in the normal 6x8 font or in the very small 4x6 font.

### DISP TYpe

|                  |     |               |
|------------------|-----|---------------|
| Default setting: | 1   |               |
| Parameter:       | 0   | No function.  |
|                  | 1   | No function.  |

Only implemented for compatibly reasons. Presently the function has no effect.


## EQualize

|                  |     |                                         |
|------------------|-----|-----------------------------------------|
| Default setting: | 0   |                                         |
| Parameter:       | 0   | No transmit equalizing.                 |
|                  | 1   | Moderate enhancement of the edge tones. |
|                  | 2   | Strong enhancement of the edge tones.   |

`EQualize` allows slight to moderate adjustment of the frequency
response of the PACTOR-3 transmit signal.

Some IF filters used in standard SSB transceivers already attenuate the
edges of only 2 kHz wide signals due to a poor frequency response. As a
countermeasure EQ allows to compensate for this effect. Please do only
use the EQ command if you really know the actual transmit frequency
response of your transceiver.


## ESCchr

|                  |             |                                              |
|------------------|-------------|----------------------------------------------|
| Default setting: | 27 (ESCAPE) |                                              |
| Parameter:       | X           | 1... 127, decimal ASCII code of a character. |

Defines the ESCAPE character.

When the PTC is in the converse mode (ARQ, FEC, CW terminal or RTTY) an
ESCAPE character is required in order to get a command prompt and input
a command.

**We recommend not to experiment with this character, since it is criticial to the control of the PTC.**


## FAX

The `FAX` command (without argument) activates the [FAX menu](FAX.md)
(**fax:**-menu). The command prompt takes the form **fax:**.

Within the **fax:**-menu the following commands are available:
```
Deviation, Fmfax, FResolut, Help, MBaud, Quit
```
All other (*normal*) commands are not available!
You can leave the **fax:**-menu with the [`Quit`](FAX.md#quit) command.

The `FAX` command can also be followed by an argument, namely a command
from the **fax:**-menu. In this case the PTC only executes this one FAX
command without switching to the **fax:**-menu.
The command is passed through, so to speak.

Directly set the [deviation of the FM-FAX demodulator](FAX.md#deviation) to 600 Hz:
```
cmd: FAX D 600<Return>
```
The [FAX commands](FAX.md) are described in detail in a [separate chapter](FAX.md).


## FSKAmpl

|                  |    |                                                     |
|------------------|----|-----------------------------------------------------|
| Default setting: | 60 |                                                     |
| Parameter:       | X  | 10... 9000, AF output voltage (peak to peak) in mV. |

Sets the Audio output (transmitted signal) of the
modem for all non PSK modes. Before this value is changed, the PSK
amplitude should have been correctly set with the [`PSKAmpl`](#pskampl) command.

After the PSK amplitude has been correctly set, the transceiver MIC gain control should **not** be further adjusted to attain the required power output for non PSK modes.

For this adjustment, (i.e. FSK/CW output power) exclusively use the
`FSKAmpl` command. The transceiver should be connected either to a
dummy load of appropriate power handling capacity, or a well matched
antenna. (please pay particular attention that the chosen frequency is
really free. Using `U 1<Return>` the Unproto mode 1 is started (100
Bd FSK). Now, using the `FSKAmpl` command, (use the ESCAPE character
to enter the command mode before each change) adjust the audio output
level of the modem until the required output power is reached (e.g.
`<ESC>FSKA 200<Return>`). It should be noted that the ALC level of
the transceiver must not exceed the prescribed level (exactly as with
PSK). To prevent possible damage to the average TRX, caused by
continuous transmission, we recommend that the FSK output power should
never exceed 50% of the maximum PEP power. In the case of the average
amateur transceiver of 100 watts, this represents the 50 watt level. The
internal impedance of the AF output stage of the modem is 330 Ohms
and resistive.


## Help

`Help` without parameters gives a list of all commands.

The PTC contains a short description of every command, so that the
manual does not need to be continually consulted. These descriptive
messages can be obtained by using `Help`, followed by the required
command.

`Help FSKAmpl` (or in shortened form `h fska`.)


## LAP

**L**oad **A**ll **P**arameters.  
Manually loads the parameters stored using [`SAP`](#sap).


## LFignore

|                  |     |                                      |
|------------------|-----|--------------------------------------|
| Default setting: | 1   |                                      |
| Parameter:       | 0   | no insertion of \<LF>.               |
|                  | 1   | insertion of \<LF> after each \<CR>. |

`LFignore` determines whether a \<LF> is automatically appended to
each \<CR> that is sent to the terminal. For `LFignore 0` the
characters are passed exactly as the PTC receives them.
For `LFignore 1` \<LF>'s sent to the PTC are ignored.


## LICENSE

|                  |      |              |
|------------------|------|--------------|
| Default setting: | none |              |
| Parameter:       | X    | License key. |

The `LICENSE` command is to enter or to readout (if already entered
previously) the License key which enables extended (professional)
firmware functions.

The following messages will be returned by the modem, depending on
licensing status:

If the license is invalid:

`LICENSE: NOT OK, XY TRIAL CONNECTS REMAINING`

Whereby XY is the number of remaining test connects.

If a valid serialnumber license is installed:

`LICENSE: SERIALNUMBERXYZO ABCDEFGHIJKL`


## Listen

|                  |      |                       |
|------------------|------|-----------------------|
| Default setting: | 1    |                       |
| Parameter:       | 0    | Listen mode disabled. |
|                  | 1    | Listen mode enabled.  |

The Listen mode is turned on with `Listen 1`, so that it is possible
to "Listen-in" to what is being sent in PACTOR QSO and to read Unproto
transmissions. Listen is only possible in the STBY condition. If the
Listen mode is active, Connect packets are also monitored and displayed:
`[CONNECT-FRAME: CALL]`, e.g. `[CONNECT-FRAME: DL6MAA]` means that a
station is trying to connect to DL6MAA. With poor signals it is possible
that the CALL is displayed only partially because it couldn´t be decoded
correctly.


## MARk

|                  |      |                               |
|------------------|------|-------------------------------|
| Default setting: | 1400 |                               |
| Parameter:       | X    | 300... 2700, frequency in Hz. |

Allows the adjustment of the mark frequency of the modem in 1 Hertz
steps. The frequency chosen is only used when the [`TOnes`](#tones) parameter is set to 2.


## MAXError

|                  |    |                                                 |
|------------------|----|-------------------------------------------------|
| Default setting: | 70 |                                                 |
| Parameter:       | X  | 30... 255, maximum number of retries or errors. |

`MAXError` defines the timeout value. When initially calling a station,
this value sets the maximum number of sync packets that the PTC sends
without a response from the other station (refer to [`Connect`](#connect) command).

When connected, `MAXError` determines how many consecutive faulty blocks
or controls are permitted before the connection is aborted
`***TIMEOUT: DISCONNECTED`. Request blocks or request controls are not
interpreted as errors, and reset the error counter to zero.

**The value 255 disables the timeout and causes endless traffic. Never use this setting for unmanned operation!**


## MOde

|                  |     |                                                                                                         |
|------------------|-----|---------------------------------------------------------------------------------------------------------|
| Default setting: | 2   |                                                                                                         |
| Parameter:       | 0   | ASCII mode with no compression                                                                          |
|                  | 1   | Huffman mode & Auto-ASCII, if necessary (Level I compression).                                          |
|                  | 2   | Full Level 2 compression with Huffman, Pseudo-Markow and run length coding and Auto ASCII if required. |

The 8 bit ASCII mode allows to transmit all characters from 0 to 255 (8
bit), inclusive the IBM special characters. Defined special characters
(e.g. Idle, CANGEOVER characters, etc). can be transmitted using the
[Ctrl-character](#ctrlchr).

In the Huffman mode only the ASCII characters 0... 127 (7 bit) can be
transmitted. To transfer certain IBM special characters (umlauts), the
PTC converts these characters according to the following table:

| **Umlaut** | **ASCII** | **Transmitted Character** |
|------------|-----------|---------------------------|
| ä          | 132       | 14                        |
| ö          | 148       | 15                        |
| ü          | 129       | 16                        |
| Ä          | 142       | 20                        |
| Ö          | 153       | 21                        |
| Ü          | 154       | 22                        |
| ß          | 225       | 23                        |

The Huffman data compression, which can improve speed up to 80%
(effective character length 4.5 to 5 bit) allows to reduce the middle
character length. The data compression of lowercase letters is better as
for uppercase letters. The ASCII mode will be useful only if the text
contains non ASCII characters, or many uppercase letters.

The PTC firmware scans through each packet determining whether HUFFMAN
or ASCII coding will be more efficient for transmission, and selects the
better one. Manually selecting the ASCII mode (`MOde 0`) makes the
controller transmit ASCII anyway. Doing this should only be necessary in
very special cases.

Automatic mode also works on characters exceeding 127 decimal. Therefore
7PLUS files may be transferred without any user intervention.

The parameter 2 is effective only with a PACTOR Level 2 link. With
Level 1 contacts, the system behaves as if the parameter 1 had been
chosen. The automatic compression used in PACTOR-2 has proved to be
very advantageous and reliable. Therefore, the `MOde` parameter should
only need to be changed in exceptional circumstances (e.g. measuring the
text throughput without compression) to a value \< 2. There are no
problems caused by leaving the Level 2 compression turned on, even when
transmitting binary files or graphics. No manual intervention by
the operator is required, as the modem will switch automatically to
uncompressed ASCII transmission for individual packets, if necessary.


## MYcall

|                  |          |                                        |
|------------------|----------|----------------------------------------|
| Default setting: | *SCSPTC* |                                        |
| Parameter:       | CALL     | Station's callsign, 2 to 8 characters. |

Defines the own Callsign. Whenever the callsign is received during STBY,
the PTC performs slave synchronization and responds with a control
signal attempting to establish the requested connect.

With an active AMTOR prompt `MYcall` sets one ´s own Selcall

Although there is a convention how to create a Selcall out of a callsign
this procedure isn´t always reasonable. Basicly an AMTOR selcall consits
of 4 letters. From a normal call usually the first and the last 3
letters are used to assemble the selcall e.g. DK5FH → DKFH, DL3FCJ →
DFCJ. If the call only contains 3 letters, the first one is used twice.

`MYcall` without argument returns the call or selcall as currently
set.

After power-on the firmware checks if there is a valid setting for the
PACTOR-MYCALL available. If it is the case (that means that the setting
is different to \*SCSPTC\*) it copies the PACTOR MYcall into all
Packet Radio channels which still contain SCSPTC and replaces it by the valid
MYCALL. The same procedure is performed if the `MYcall` command is
executed with a valid call as argument in the **cmd:**-menu. This
ensures that after a `RESTart` or after the first power-on all calls
are set to a valid value.


## MYLevel

|                  |   |                                                                                                            |
|------------------|---|------------------------------------------------------------------------------------------------------------|
| Default setting: | 3 |                                                                                                            |
| Parameter:       | 1 | The modem behaves as a Level 1 controller                                                                  |
|                  | 2 | The modem behaves as a Level 2 controller, and will switch to PACTOR-2 when the other station is so fitted |
|                  | 3 | The modem behaves as a Level 3 controller, and will switch to PACTOR-3 when the other station is so fitted |
|                  | 4 | The modem behaves as a Level 4 controller, and will switch to PACTOR-4 when the other station is so fitted |

This command serves to maintain the highest possible PACTOR level. The
parameter should only be set to 1 or 2 for test purposes. The default
value 3 leads to a very reliable and automatic level choice procedure
during the link initialization, so that the link always proceeds using
the highest possible level. There are no disadvantages incurred by using
this *auto negotiate* procedure.

`MYLevel` without argument leads to a 2 line output. The first line
displays the maximum possible link level (1…3, as set with `MYLevel`).
The second line displays the link level of the current or last link.
This may be useful if PC software wants to test in which link level
PACTOR links runs or ran.


## OFF

Switches off the P4dragon DR-7800.


## OFFMessage

|                  |            |                              |
|------------------|------------|------------------------------|
| Default setting: | Power Down |                              |
| Parameter:       | message    | String of max. 20 characters |

Sets the power-off message that is shown on the OLED display.
If your personal power-off message contains spaces, the message must be placed in quotation marks, e.g.: "This is the end".


## PACket

The `PACket` command (without argument) activates the [Packet Radio menu](Packet-Radio.md)
(**pac:**-menu). The command prompt takes the form **pac:**.

Within the **pac:**-menu the following commands are available:
```
Aprs, Baud, CHeck, Connect, CONStamp, CONVerse, CStatus, DIGIpeat,
Disconne, FRack, FUlldup, Help, JHOST, KISS, LAP, MAXframe, MCon,
Monitor, MONTimer, MStamp, MYAlias, MYcall, PErsist, PRPort, Quit,
RESptime, REtry, SAP, Setchn, SLottime, TXdelay, TXLevel, Unproto, USers, Version
```
All other (*normal*) commands are not available!
You can leave the **pac:**-menu with the [`Quit`](Packet-Radio.md##quit) command.

The `PACket` command can also be followed by an argument, namely a command
from the **pac:**-menu. In this case the PTC only executes this one Packet Radio
command without switching to the **pac:**-menu.
The command is passed through, so to speak.

Switch off the [Packet Radio listen](Packet-Radio.md#monitor):
```
cmd: PAC M 0<Return>
```
The [Packet Radio commands](Packet-Radio.md) are described in detail in a [separate chapter](Packet-Radio.md).


## PDTimer

|                  |     |                                                |
|------------------|-----|------------------------------------------------|
| Default setting: | 12  |                                                |
| Parameter:       | X   | 2... 30, PACTOR Duplex BREAKIN time in seconds |

Defines the PACTOR Duplex BREAKIN time. This is the minimum time the PTC
has to be in IRS state (data receiving), until a BREAKIN is sent
automatically in the case that own transmission data are available, and
*takes the keys*.

The `PDTimer` value is only valid in the PACTOR Duplex mode (`PDuplex` is set to 1).


## PDuplex

|                  |     |                            |
|------------------|-----|----------------------------|
| Default setting: | 0   |                            |
| Parameter:       | 0   | PACTOR Duplex switched off |
|                  | 1   | PACTOR Duplex switched on  |

PACTOR Duplex offers an intelligent CHANGEOVER automatic. For further
information about PACTOR Duplex refer to chapter 5.12, page 55.


## PMONitor

The PACTOR monitor is used for comprehensive observation and documentation
of all unencrypted PACTOR transmissions that have been possible to date.
The PACTOR monitor is configured using the `PMONitor` command. A brief overview
of the types of possible arguments can be obtained, as usual, with the command

`cmd: Help PMONitor<Return>`

Or simply

`cmd: PMONitor<Return>`

Via the OLED display it is also possible to switch between PACTOR-4 monitor,
PACTOR-1,2,3 monitor and normal auto decoder monitor (with PACTOR standby function)
by selecting the menu item *Monitor* in the sensor menu of the P4dragon DR-7800.
The three operating modes are run through cyclically.

### PMON Start

Starts the PACTOR monitor. Depending on the `PMON Mode` value the modem responds with different messages.

For mode 3:
````
PACTOR-1/2/3 Monitor started:
=============================
````

For mode 4:
```
PACTOR-4 Monitor started:
=========================
```


### PMON STop

Stops the PACTOR monitor. After this command, the modem works again in 
normal standby mode, so PACTOR connections can be accepted or established again.

The modem outputs the following message:
```
PACTOR Monitor stopped!
=======================
```

### PMON Mode

|                  |     |                                   |
|------------------|-----|-----------------------------------|
| Default setting: | 3   |                                   |
| Parameter:       | 3   | Monitor PACTOR levels 1,2 and 3.  |
|                  | 4   | Monitor PACTOR level 4.           |

Sets the PACTOR level to be detected. PACTOR-4 is read with the value 4. As the computing power required for this is very high, the other PACTOR levels cannot be read in parallel. PACTOR-1,2,3 are read in parallel with the value 3 but PACTOR-4 will not be detected then.

### PMON Packets

|                  |     |                                   |
|------------------|-----|-----------------------------------|
| Default setting: | 0   |                                   |
| Parameter:       | 0   | Only output TRAFFIC packets.      |
|                  | 1   | Output TRAFFIC & REQUEST packets. |

Defines which package variants to be output. With parameter 0, only TRAFFIC packets are output. These are packets with a correct CRC and a CRC that differs from the previous packet. With parameter 1, TRAFFIC packets and REQUEST packets (repetitions) are output.

### PMON Verbose

|                  |     |                                       |
|------------------|-----|---------------------------------------|
| Default setting: | 1   |                                       |
| Parameter:       | 0   | Show only the payload.                |
|                  | 1   | Output additional status information. |
|                  | 2   | Print a modulo-4 frame counter.       |
|                  | 3   | Print the packet CRC.                 |

The Verbose sub-command defines whether status information on the received packets (in addition to the actual payload) should be output.

With parameter 0 only the actual payload (user data) is output, otherwise no additional information.

With parameter 1 there is a formatted output beginning with status information, followed by the actual payload.

With parameter 2, an additional modulo-4 frame counter (“FRCNT”) is displayed.

With parameter 3, the packet CRC will be additionally displayed as 4-digit hex number ("CRC: XXXX").

The chapter [Firmware](Firmware.md) contains a [detailed description](Firmware.md#pmonitor) of the output format.

### PMON Hex

|                  |     |                                                     |
|------------------|-----|-----------------------------------------------------|
| Default setting: | 1   |                                                     |
| Parameter:       | 0   | No automatic Hex conversion.                        |
|                  | 1   | Automatic Hex conversion of unprintable characters. |
|                  | 2   | Allways output payload as Hex.                      |

If this parameter is set to 0, if `PMON Verbose 0` is set, the automatic hexadecimal conversion is never carried out for unprintable characters. This allows PACTOR broadcasts, e.g. unproto broadcasts, to be recorded unaltered, even if e.g. special characters in the range 128-255 (dec.) are used.

With parameter 2, the payload is generally output as a Hex dump, regardless of the content and the `PMON Verbose` parameter.
The chapter [Firmware](Firmware.md) contains a [detailed description](Firmware.md#pmonitor).

### PMON Autostart

|                  |     |                                     |
|------------------|-----|-------------------------------------|
| Default setting: | 0   |                                     |
| Parameter:       | 0   | Do not start `PMONitor` at power-on |
|                  | 1   | Start `PMONitor` at power-on        |

If this parameter is set to 1, the PMONitor starts automatically after booting / newstart of the DR-7X00.


## POSition

|                  |      |                         |
|------------------|------|-------------------------|
| Default setting: | none |                         |
| Parameter:       | NMEA | Requests NMEA raw-data. |

When a GPS receiver is connected to the modem, its possible to
readout the actual position using the `POSition` command. The
position information normally has the following format:
```
GPS POSITION REPORT
-------------------

Latitude: 50° 05.430' North
Longitude: 008° 45.980' East
Velocity: 0.0 Knots
Course: 360°

Recorded at: 13/12/00 19:25:48 UTC/GMT
```
The `POSition` command allows the argument NMEA.

`cmd: POS NMEA<Return>`

In this case the modem return the original NMEA compatible
position string ("sentence") - exactly as it was received from the GPS
receiver. NMEA compatible strings are *understood* by various
navigational programs, and can thus be almost universally used. The NMEA
compatible position string usually has the following format:
`$GPRMC,212234,A,5005.432,N,00845.974,E,000.0,360.0,190201,000.1,E\*7B`


## PSKAmpl

|                  |     |                                                             |
|------------------|-----|-------------------------------------------------------------|
| Default setting: | 140 |                                                             |
| Parameter:       | X   | 10... 9000, AF output voltage (peak to peak) in millivolts. |

Sets the AF output voltage (transmitted signal) of
the modem for the DPSK modes (PACTOR-2 and up).
The DPSK signal has a variable envelope, the average power
of which is approximately half the peak power. It is therefore necessary
to be able to adjust the PSK signal amplitude separately from the FSK
amplitude ([`FSKAmpl`](#fskampl) command), in
order that both forms of modulation should have the correct average
power level. (A simple automatic adjustment of the PSK amplitude by a
factor 1.45 does not give a satisfactory result, as the ALC control
characteristics are different from transmitter to transmitter).

The input sensitivity of most transceivers is adjusted for the output
level of an average dynamic microphone. With 200 mV (peak to peak)
therefore, most transmitters would be fully driven with the microphone
control only slightly open. It is not recommended to use a very high
`PSKAmpl` value, and then turn the MIC gain control right down, as the
first AF stage is normally before the gain control, and rather sensitive
to overdriving. We recommend that the `PSKAmpl` value of 140 (the
default setting) be left alone, and the PSK output to be increased with
the microphone gain control (if available). The transceiver should be
connected either to a dummy load of appropriate power handling
capacity, or a well matched antenna. (Please pay particular attention
that the chosen frequency is really free. PACTOR links operate even
when the signals are so weak as to be virtually *non existent*!). Use
`U 3<Return>` to start the Unproto mode 3 (100 Bd DBPSK). Now, using
the Mic gain control of the transceiver, the power is increased until
the ALC voltage has reached the desired value.

**Do not in any circumstances overdrive the transmitter, otherwise the signal will be made considerably wider due to intermodulation products!**

When correctly adjusted, the peak power should be approximately the same
as the PEP rated power output of the TRX. The effective average power is
then approximately half the maximum power, so that continuous operation
should pose no thermal problems. Note that many modern transmitters only
show the peak power and this must then be taken into consideration. If
the Mic gain control must be turned up over half way, then it is
recommended the `PSKAmpl` value be increased. (By for example `<Esc>PSKA 200<Return>`).
If there is no Mic gain adjustment available,
then naturally the PSK amplitude must be adjusted with the `PSKAmpl`
command alone. The internal resistance of the AF output level of the
modem is 330 ohm and real.


## PT

Returns to PACTOR from the AMTOR or RTTY modes. Activates the
PACTOR input prompt (**cmd:**).


## PTCComp

|                  |     |                                               |
|------------------|-----|-----------------------------------------------|
| Default setting: | 1   |                                               |     
| Parameter:       | 0   | P4dragon native mode.                         |
|                  | 1   | PTC-II compatibility mode level 1.            |
|                  | 2   | PTC-II compatibility mode level 2.            |

Activates the PTC-II compatibility mode. In mode 1 (default setting), the power-on message and the answer to the [`Version` command](#version) is given out in the appropriate form for the PTC-II. In mode 2, the answer to the [`Ver #` command](#Brief_overview_of_the_most_important_modem_properties) is also adjusted.

For software which has been written for the PTC-II modems, the `PTCC` parameter should be set to at least 1. This is for example particularly required for Airmail.

In compatibility mode 1 and 2, the argument “3” in the [`MYLevel` command](#mylevel) automatically changed to “4”. The command `MYLevel 3` thus results in a parameter value 4 for `MYLevel`. In order to set `MYLevel` to 3, the compatibility mode must be turned off (`PTCC 0`).


## PTChn

|                  |     |                                       |
|------------------|-----|---------------------------------------|
| Default setting: | 4   |                                       |
| Parameter:       | X   | 1... 31, hostmode channel for PACTOR. |

Defines the hostmode channel for PACTOR.
PACTOR can only be operated in a hostmode program on the channel defined here.


## Qrt

Identical to the [`Disconnect` command](#disconnect). 


## QRTChr

|                  |            |                                 |
|------------------|------------|---------------------------------|
| Default setting: | 4 (Ctrl-D) |                                 |
| Parameter:       | X          | 1... 127, ASCII-Code (decimal). |

Sets the QRT character, which causes the system to go QRT (close the
link). It can also be sent is the RX mode, which then becomes active at
the next TX phase. In UNPROTO it switches from
transmit to receive. It is an alternative to the [`Disconnect` command](#disconnect),
and can also be put at the end of a text to be transmitted, so that at
the end of the transmitted text, the link is closed down.


## Quit



## RESEt

Soft reset of the modem!

**This command may be used at any time and causes an uncontrolled disconnect while connected! The parameters entered are not cleared.**


## RESTart

Causes a complete re-initialization of the modem either to factory defaults or user preset (seved with `SAP`). The behaviour can be controlled with the `RESTPar` command.

**This command may be used at any time and causes an uncontrolled disconnect while connected! Customized parameters are replaced by the defaults.**


## RESTPar

|                  |     |                                      |
|------------------|-----|--------------------------------------|
| Default setting: | 0   |                                      |
| Parameter:       | 0   | Normal `RESTart` (factory defaults). |
|                  | 1   | `RESTart` loading user preset.       |

This command is available in the **cmd:**-menu and allows to configure des `RESTart` command.
If set to 0 a normal `RESTart` is performed, modem parameters will be loaded from the Flash ROM at system start.
If set to 1 the modem parameters will be loaded from the EEPROM, i.e. parameters stored by using SAP command will be utilized. (For that feature, the EEPROM parameter block must be available, i.e. at least stored once using the SAP command.)



## SAP

**S**ave **A**ll **P**arameters.  
This command saves all the presently set command parameters (e.g. your own callsign which has been set using [`MYcall`](#mycall)) in non volatile memory. Directly after switching on the modem, these parameters are read from the EEPROM and used as presets. The `SAP` command is especially useful when used with software which is not specially written for the P4dragon DR-7800 and thus does not set all required parameters correctly when started. In this case it is sensible that pre-set parameters (e.g. [`MYcall`](#mycall), [`PSKAmpl`](#pskampl), [`FSKAmpl`](#fskampl)) are used – so that they must not be newly configured after every new switch on of the modem. With `SAP` it is for example possible to set the modem permanently in [compatibility mode 2](#ptccomp).


## SPAce

|                  |      |                               |
|------------------|------|-------------------------------|
| Default setting: | 1200 |                               |
| Parameter:       | X    | 300... 2700, frequency in Hz. |

Allows the adjustment of the space frequency of the modem in 1 Hertz
steps. The frequency chosen is only used when the [`TOnes` parameter](#tones) is set to 2.


## STatus

|                  |     |                                |
|------------------|-----|--------------------------------|
| Default setting: | 1   |                                |
| Parameter:       | 0   | Status checking on (see text). |
|                  | 1   | Status checking on.            |
|                  | 2   | Automatic status output.       |

The status word polling in the P4dragon DR-7800 is permanently turned on.
The parameter 0 has only been retained for compatibility reasons.

This command facilitates polling of all operational states of the modem
via the serial interface. This is useful for mailbox systems, or more
luxurious terminal programs.

The status byte is called by the RS character (ASCII decimal 30). This
definition of the status request byte does not impose any restrictions
on data transparency. PACTOR uses ASCII 30 (decimal) as the *idle byte*
which can only be transmitted via a supervisor sequence.

The PTC's status reply always begins with an echo of the RS character
(ASCII decimal 30) to facilitate unique identification of the status
information following. The actual status byte follows this *header*.

This modular status level concept facilitates an expansion of the status
information in the future, i.e., in a higher status level, even several
bytes containing status information can be implemented. The status bytes
(incl. header) are sent in direct sequence.

During the transmission of status information new status requests are
ignored.

The status information is processed totally independent from the current
XON/XOFF state of the serial interface.

In status mode 2, the modem has an automatic status output. This
means that the status no longer needs to be regularly polled by the
terminal program. Instead, every status change causes the status
information automatically to be given. The status output is in the usual
format: 30, S (S = status-byte). In status mode 2, the status byte can
still be polled via the terminal as before, for instance directly after
the start of the terminal program.

Hints for programmers: Through the PACTOR software the status reply may
be delayed by 150 ms. After a system boot (power on, `RESTart`, or
`RESEt`), the status polling is ready after the first **cmd:**-prompt.
Construction of the status byte (status-level 1):

| **Bit** | **7** | **6** | **5** | **4** | **3** | **2**  | **1**  | **0**  |
|---------|-------|-------|-------|-------|-------|--------|--------|--------|
| Meaning | 1     | MODE  | MODE  | MODE  | D     | STATUS | STATUS | STATUS |

**Bit 7** always 1 to avoid control codes (XON/XOFF, etc).

**Bit 3** (DIRECTION bit) reflects the state of the SEND LED. This bit
is 1 when the PTC is the packet sender.

The fields mode and status have the following meaning:

| **Bit** |       |       |                 |                                                                                               |
|---------|-------|-------|-----------------|-----------------------------------------------------------------------------------------------|
| **2**   | **1** | **0** | **STATUS-Bits** | **Remark**                                                                                    |
| 0       | 0     | 0     | ERROR           |                                                                                               |
| 0       | 0     | 1     | REQUEST         |                                                                                               |
| 0       | 1     | 0     | TRAFFIC         |                                                                                               |
| 0       | 1     | 1     | IDLE            | Idle byte in packet, does not exclude traffic bytes in the packet!                            |
| 1       | 0     | 0     | OVER            | The system is busy with a CHANGEOVER. ERROR, REQUEST, TRAFFIC, and IDLE are ignored.          |
| 1       | 0     | 1     | PHASE           | AMTOR only.                                                                                   |
| 1       | 1     | 0     | SYNCH           | Active immediately after first half of a selcall or the first 4 decoded PACTOR address bytes. |
| 1       | 1     | 1     | IGNORE          | Status currently not defined (e.g. STBY).                                                     |


| **Bit** |       |       |               |                                                                                                                                                             |
|---------|-------|-------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **6**   | **5** | **4** | **MODE-Bits** | **Remark**                                                                                                                                                  |
| 0       | 0     | 0     | STANDBY       |                                                                                                                                                             |
| 0       | 0     | 1     | AMTOR-ARQ     |                                                                                                                                                             |
| 0       | 1     | 0     | PACTOR-ARQ    | Active no more than 20 ms after the end of the SYNC sequence in the received SYNC packet, or for a MASTER start no later than the begin of the data packet. |
| 0       | 1     | 1     | AMTOR-FEC     |                                                                                                                                                             |
| 1       | 0     | 0     | PACTOR-FEC    |                                                                                                                                                             |
| 1       | 0     | 1     | RTTY / CW     |                                                                                                                                                             |
| 1       | 1     | 0     | LISTEN        | AMTOR or PACTOR.                                                                                                                                            |
| 1       | 1     | 1     | Channel-Busy  | RF channel busy.                                                                                                                                            |


In STBY condition the modem analyzes the HF channel and differs
between *busy* and *free*.

A *busy* channel is defined as all signals that are audibly distinctly
different from noise, but, however, having a speed \< 250 Baud.
Packet-Radio (300 Baud) is virtually ignored. Furthermore, strong
carriers on the channel are not evaluated as *channel busy*. Even the
very hard to detect PACTOR-2 signals were recognized. The PTC-IIpro
reacts well even to short QPSK/BPSK sections, so that even the short
PACTOR-2 acknowledgement signal is sufficient for the channel to be
recognized as busy.

This function is essential for automatic stations, e.g. **WinLink**
systems.

An occupied HF channel is indicated by a status value of 247 (Channel
busy) being given over the serial interface. After the channel
busy status has been activated, it remains so for at least 3.5 seconds.
An optical output is also given, with the TRAFFIC LED lighting up when
the channel is busy.

The Channel busy status is only given in the STBY condition, and **not**
in Listen mode (L=1)!


## SYStest

The `SYStest` command (without argument) activates the [system test menu](SYStest.md)
(**sys:**-menu). The command prompt takes the form **sys:**.

Within the **sys:**-menu the following commands are available:
```
Beep, CHKBL, CHKFlash, Flash, GPSspeed, Help, HWInfo, Led, LOG, Ptt, Quit, SCANSTOP, SERNum, Trxtest, TUnit
```
All other (*normal*) commands are not available!
You can leave the **sys:**-menu with the [`Quit`](SYStest.md#quit) command.

The `SYStest` command can also be followed by an argument, namely a command
from the **sys:**-menu. In this case the PTC only executes this one system
test command without switching to the **sys:**-menu.
The command is passed through, so to speak.

This command for example would show the modem's [serial number](SYStest.md#sernum):
```
cmd: SYS SERNum<Return>
```
The [SYStest commands](SYStest.md) are described in detail in a [separate chapter](SYStest.md).


## Term

**Deprecated**

|                  |     |                                               |
|------------------|-----|-----------------------------------------------|
| Default setting: | 0   |                                               |     
| Parameter:       | 0   | Simple terminal mode.                         |
|                  | 1   | Terminal mode with delayed echo.              |
|                  | 2   | Split screen terminal mode.                   |
|                  | 3   | Enhanced split screen.                        |
|                  | 4   | Split screen with command prompt recognition. |
|                  | 5   | Split screen also for Packet-Radio.           |

With this command it is possible to make the PTC-IIpro support split
screen terminals.

In **simple terminal mode** text is not sent to the terminal when the
PTC receives commands from the user. The text stream is interrupted by
the first command given. At maximum 2000 characters are stored. The
terminal must have local echo (halfduplex).

**Terminal mode 1** is for use with simple split screen terminals. The
incoming text, and the text to be sent out, should be displayed in
separate windows on the screen. All transmitted characters are echoed by
the PTC, as soon as they are transmitted and correctly confirmed by the
station the PTC is connected to (delayed echo).

**In terminal mode 2** the PTC completely controls the switchover
between the windows on the screen. Therefore the screen is divided in
two areas. In the upper area the system information of the PTC and the
text to be transmitted appears. The lower window shows the received text
and the delayed echo-text. The PTC sends Ctrl-A as a changeover
character to the TX/information window and Ctrl-B as a changeover
character for RX/delayed echo window. The windows should be scrollable
independently.

**Terminal mode 3** arranges the delayed echo to be signaled by a
Ctrl-C, not a Ctrl-B as it is in terminal mode 2. The normal RX text is
still signaled by a Ctrl-B. This convention makes it possible to divide
the screen into three parts. The first window (Ctrl-A) for system
information and TX text, the second window (Ctrl-B) for RX text and the
third window (Ctrl –C) for delayed echo text.

**Terminal mode 4** differs from TERM 3 in that the PTC sends a Ctrl-D
before every command prompt. TERM 4 considerably eases the terminal
programming, in that the continuous search for prompts (**cmd:**,
**\*\*--A--\*\***, etc) is no longer required. Also, the PTC always
sends a pseudo prompt when the command interpreter is closed again (on
Connect, on switching to the CW or RTTY modes, etc.). This contains only
a \< Ctrl-D>, followed by a \<CR>, thus complete control over the
(command) input window is maintained, and there is no ambiguity
concerning the \<CR> sent from the PTC. It is recommended that the \<CR>
from the keyboard, signaling the end of a command, is not shown as local
echo in the input window, but just ignored. This minimizes unnecessary
empty lines in the input window.

**In terminal mode 5**, PR data, link status messages, monitor
information etc is always proceeded with a Ctrl-F. Only direct answer
messages for a command input do not fall under this convention. This
allows the comfortable administration of PR multi connects etc. using a
non hostmode terminal.

All PR received data is sent **at once** to the terminal program without
bothering about the **Setch** command (refer to chapter 9.7.35, page
165). **Setch** only has influence on the present transmit channel in
terminal mode. This means that one must set **Setch** to 2 if one wishes
to transmit data via channel 2. (If for instance an external link from
the PTC-IIpro has been automatically given channel 2 and one wanted to
write a text to that other station.) Terminal programs that fully
support Term 5 must therefore also automatically administrate the
**Setch** command.

After Ctrl-F, follows the channel number (binary, increased by 48) and
then the codebyte, as is defined in WA8DED hostmode:

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 79%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Code Byte</strong></th>
<th><blockquote>
<p><strong>Meaning</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>0</td>
<td><blockquote>
<p>Success, no text follows (Not used in Term 5)</p>
</blockquote></td>
</tr>
<tr class="even">
<td>1</td>
<td><blockquote>
<p>Success, text follows (Not used in Term 5)</p>
</blockquote></td>
</tr>
<tr class="odd">
<td>2</td>
<td><blockquote>
<p>Error, text follows (Not used in Term 5)</p>
</blockquote></td>
</tr>
<tr class="even">
<td>3</td>
<td><blockquote>
<p>Link status info follows (CONNECTED to... etc).</p>
</blockquote></td>
</tr>
<tr class="odd">
<td>4</td>
<td><blockquote>
<p>Monitor header follows / no monitor data</p>
</blockquote></td>
</tr>
<tr class="even">
<td>5</td>
<td><blockquote>
<p>Monitor header follows / monitor data available</p>
</blockquote></td>
</tr>
<tr class="odd">
<td>6</td>
<td><blockquote>
<p>Data from the monitor follows</p>
</blockquote></td>
</tr>
<tr class="even">
<td>7</td>
<td><blockquote>
<p>Data from the link follows</p>
</blockquote></td>
</tr>
</tbody>
</table>

The terminal mode 5 also extends the command prompt. Every command
prompt, as in terminal mode 4 is proceeded with a Ctrl-D. after every
Ctrl-D however, follows a byte with prompt information. Bits 5-7 contain
coded information about the prompt sort:

<table>
<colgroup>
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 18%" />
<col style="width: 59%" />
</colgroup>
<thead>
<tr class="header">
<th>Bit 7</th>
<th>Bit 6</th>
<th>Bit 5</th>
<th>Prompt</th>
<th><blockquote>
<p>Bits 0-4</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>0</td>
<td>0</td>
<td>0</td>
<td>Not allowed</td>
<td><blockquote>
<p>-</p>
</blockquote></td>
</tr>
<tr class="even">
<td>0</td>
<td>0</td>
<td>1</td>
<td>cmd:</td>
<td><blockquote>
<p>0=cmd, 1=AMTOR, 2=MONITOR, 3=RTTY, 4=CW, 5=PSK31</p>
</blockquote></td>
</tr>
<tr class="odd">
<td>0</td>
<td>1</td>
<td>0</td>
<td>trx:</td>
<td><blockquote>
<p>always 0</p>
</blockquote></td>
</tr>
<tr class="even">
<td>0</td>
<td>1</td>
<td>1</td>
<td>sys:</td>
<td><blockquote>
<p>always 0</p>
</blockquote></td>
</tr>
<tr class="odd">
<td>1</td>
<td>0</td>
<td>0</td>
<td>aud:</td>
<td><blockquote>
<p>always 0</p>
</blockquote></td>
</tr>
<tr class="even">
<td>1</td>
<td>0</td>
<td>1</td>
<td>pac:</td>
<td><blockquote>
<p>present input channel (0-31)</p>
</blockquote></td>
</tr>
<tr class="odd">
<td>1</td>
<td>1</td>
<td>0</td>
<td>rcu:</td>
<td><blockquote>
<p>always 0</p>
</blockquote></td>
</tr>
<tr class="even">
<td>1</td>
<td>1</td>
<td>1</td>
<td>fax:</td>
<td><blockquote>
<p>always 0</p>
</blockquote></td>
</tr>
</tbody>
</table>

The bits 0-4 contain additional information, depending on the actual
prompt. After the prompt codebyte it follows as usual the text prompt
information, ended with a Ctrl-A.

The **pac:**-prompt contains the channel number of the presently set
input channel (**Setchn**) as plain text information before the colon.
(Channel numbers of two digits are thus output by two ASCII number
characters.)

The prompt information of terminal mode 5 cannot be split. I.e. no other
information can be pushed through between bytes. The prompt always
begins with a Ctrl-D and always ends with a Ctrl-A.


## TIme

|                  |          |               |
|------------------|----------|---------------|
| Default setting: |  none    |               |
| Parameter:       | HH:MM:SS | Desired time. |

`TIme` is used to set or read the internal clock.

If `TIme` is entered without a parameter, the current time is
displayed.

When the clock is set, leading zeroes must not be omitted. The colons
can be omitted. Wrong entries cause a wrong programming of the clock
chip.

Setting the clock to 9 o’clock 56 ninutes and 5 seconds

`cmd: TI 09:56:05`

or

`cmd: TI 095605`.


## TOnes

|                  |     |                                                                 |
|------------------|-----|-----------------------------------------------------------------|
| Default setting: | 4   |                                                                 |
| Parameter:       | 0   | Low tones (1200/1400 Hz).                                       |
|                  | 1   | High tones (2300/2100 Hz).                                      |
|                  | 2   | Freely adjustable tones - definable with [`Mark`](#mark) - [`Space`](#space) commands. |
|                  | 3   | PACTOR-3/4 tones 1200/1400 Hz                                   |
|                  | 4   | Standard PACTOR-3/4 tones 1400/1600 Hz                          |
|                  | 5   | PACTOR-3/4 tones 1600/1800 Hz                                   |

The `TOnes` command allows to switch between various tone standards.

With PSK operation, care must be taken that the difference between the two tones is exactly 200 Hz, to remain compatible with the PT-II standard.

There is nothing, however, against experimenting with a chosen partner station with different shifts. It should be noted, however, that shifts greater than 200 Hz cannot be used with a narrow IF filter.

A PACTOR connection will only switch to PACTOR-3/4 during link
establishment if the TOnes parameter is greater than 2! We generally recommend to use TOnes 4 - also for PACTOR-1/2 connections. Furthermore we recommend to work PACTOR-3/4 only on the upper sideband (USB).

Please also note that the audio passband, i.e. the occupied audio
spectrum, of the PACTOR-3/4 signal always is fixed at 400-2600 Hz and INDEPENDENT of the TOnes setting. Regarding PACTOR-3/4, `TOnes` does ONLY define the (connect) tones used during link establishment, it does NOT define the relative location of the audio passband. If you want to adjust the audio passband, you can only do that by using the “passband tuning / IF shift” (or similar) at the radio!

Both systems participating in a PACTOR-3/4 connection MUST definitely use the same TOnes parameter - otherwise a link will not work properly! |

A description of the parameter follows:

0. Low tones  
  1400 Hz = Mark frequency.  
  1200 Hz = Space frequency.

1. High tones  
  2100 Hz = Mark frequency.  
  2300 Hz = Space frequency.

2. The freely definable [`MArk`](#mark) and [`SPAce`](#space) tones are used.

3. PACTOR-3/4  
  1200/1400 Hz  
  Call (dial) tones for PACTOR-3/4 link setup

4. PACTOR-3/4 (recommended setting)  
  1400/1600 Hz  
  Call (dial) tones for PACTOR-3/4 link setup

5. PACTOR-3/4  
  1600/1800 Hz  
  Call (dial) tones for PACTOR-3/4 link setup


## TRX

The `TRX` command (without argument) activates the [transceiver remote control menu](TRXctrl.md)
(**trx:**-menu). The command prompt takes the form **trx:**. 

Within the **trx:**-menu the following commands are available:
```
DD, DUmp, Frequency, Help, IType, KType, Offset, Parity, Quit, RTS, SAP, Transfer, TYpe, YType
```
All other (*normal*) commands are not available!
You can leave the **trx:**-menu with the [`Quit`](TRXctrl.md#quit) or [`DD`](TRXctrl.md#dd) command.

The `TRX` command can also be followed by an argument, namely a command
from the **trx:**-menu. In this case the PTC only executes this one transceiver control
command without switching to the **trx:**-menu.
The command is passed through, so to speak.

This command, for example, would [change the frequency](TRXctrl.md#frequency) of a connected transceiver directly to 14079.0 kHz:
```
cmd: TRX Frequency 14079.0<Return>
```
The [TRX commands](TRXctrl.md) are described in detail in a [separate chapter](TRXctrl.md).


## TXDelay

|                  |     |                                   |
|------------------|-----|-----------------------------------|
| Default setting: | 4   |                                   |
| Parameter:       | X   | 1... 31, PTT delay in X • 5 msec. |

Sets the TX keying delay (x times 5 ms). The TX keying delay (TXDelay)
is the time between activating the PTT and the sending of the first
data.


## Unproto

|                  |                               |                                          |
|------------------|-------------------------------|------------------------------------------|
| Default setting: | 1 \*2                         |                                          |
| Parameter:       | 1... 10, 30... 41, 401... 420 | Transmission mode for Unproto operation. |
|                  | \*1… 5                        | Number of packet repetitions.            |

This command allows the transmission of broadcasts (CQ calls etc). in
PACTOR without acknowledgment from the receiving station(s). An optional
parameter sets the baud rate, and the number of repetitions of packets,
in the transmission. This parameter can be set according to prevailing
conditions.

Set the number of packet repetitions to 3.

**cmd:** **U** \*3 \<Return>

Now, with the following command a 200 baud transmission can be started.

**cmd:** **U** 2 \<Return>

Unproto modes for PACTOR-1:

| **Parameter** | **Speedlevel** | **Packet definition**                  |
|--------------:|:---------------|:----------------------|
| 1:            | 100 Bd FSK     | (standard method for Level I CQ calls) |
| 2:            | 200 Bd FSK     |                                        |

Unproto modes for PACTOR-2:

| **Parameter** | **Speedlevel** | **Packet definition**                                     |
|--------------:|:---------------|:----------------------|
| 3:            | 100 Bd DPSK    | (short cycle) (standard method for *Level II only* calls) |
| 4:            | 200 Bd DPSK    | (short cycle)                                             |
| 5:            | 400 Bd DPSK    | (short cycle)                                             |
| 6:            | 800 Bd DPSK    | (short cycle)                                             |
| 7:            | 100 Bd DPSK    | (long cycle)                                              |
| 8:            | 200 Bd DPSK    | (long cycle)                                              |
| 9:            | 400 Bd DPSK    | (long cycle)                                              |
| 10:           | 800 Bd DPSK    | (long cycle)                                              |

Unproto modes for PACTOR-3:

| **Parameter** | **Speedlevel** | **Packet definition** |
|--------------:|:---------------|:----------------------|
| 30:           | 1              | short cycle           |
| 31:           | 2              | short cycle           |
| 32:           | 3              | short cycle           |
| 33:           | 4              | short cycle           |
| 34:           | 5              | short cycle           |
| 35:           | 6              | short cycle           |
| 36:           | 1              | long cycle            |
| 37:           | 2              | long cycle            |
| 38:           | 3              | long cycle            |
| 39:           | 4              | long cycle            |
| 40:           | 5              | long cycle            |
| 41:           | 6              | long cycle            |

Unproto modes for PACTOR-4:

| **Parameter** | **Speedlevel** | **Packet definition** |
|--------------:|:---------------|:----------------------|
| 401:          | 1              | short cycle           |
| 402:          | 2              | short cycle           |
| 403:          | 3              | short cycle           |
| 404:          | 4              | short cycle           |
| 405:          | 5              | short cycle           |
| 406:          | 6              | short cycle           |
| 407:          | 7              | short cycle           |
| 408:          | 8              | short cycle           |
| 409:          | 9              | short cycle           |
| 410:          | 10             | short cycle           |
| 411:          | 1              | long cycle            |
| 412:          | 2              | long cycle            |
| 413:          | 3              | long cycle            |
| 414:          | 4              | long cycle            |
| 415:          | 5              | long cycle            |
| 416:          | 6              | long cycle            |
| 417:          | 7              | long cycle            |
| 418:          | 8              | long cycle            |
| 419:          | 9              | long cycle            |
| 420:          | 10             | long cycle            |

The PACTOR-4 unproto modes 401-404 do not transfer any payload!

If no argument is given, then the modem uses the mode that was last
used, or the default setting. The actual mode is shown on the LED status
field.

The Unproto mode may be terminated with a [QRT character](#qrtchr), a
[`Disconnect`](#disconnet). It is always possible to abort a unproto transmission
using the [command `DD`](#dd).

A repetition rate of 3 does not mean that the text appears on the screen
of the receiving station 3 times. In this case, the PTC increases the
redundancy of the signal by repeating it. The transmission takes longer,
but there is a correspondingly greater chance of receiving it correctly.
At the receiving station, once a packet is correctly received, it will
not be received again. A data packet may be repeated 3 times, but will
only appear once at the receiving station(s). It is recommended that the
repetition rate should be adjusted according to propagation conditions.
A greater repetition rate, and lower baud rate, for poor conditions, and
conversely a lower repetition rate, and higher baud rate, for better
conditions.

**After approx. 4 minutes of pure idle transmission, automatic QRT takes place.**


## UPDATE

The `UPDATE` command renews the PACTOR firmware in the Flash ROM of
the modem. It should only be used together with the corresponding
program on the PC, which automaticly performs the update procedure with
all necessary handshake and control mechanisms.


## Version

Shows a short version and copyright message. The message depends on the setting of the [`PTCComp` command](#ptccomp).

With `PTCC 0` the message looks like this:
```
SCS P4dragon DR-7400 - Shortwave Communication Controller
Version 2.40.00
Copyright (C) SCS GmbH & Co. KG, Hanau, GERMANY 1994-2021

MiniBooter Version 1.12
  Built on 20150306

Bootloader Version 1.20
  Built on 20170424
```
With `PTCC 1` or `PTCC 2` the message looks like this:
```
PTC-IIpro - High Performance HF/VHF/UHF Communications Controller
PACTOR - Level-III - High Speed Data Transfer Protocol
 >>> Professional / Marine Firmware V.4.0  <<<
 (C) 1994-2021  SCS GmbH & Co. KG - Germany

BIOS: Version 2.08 detected

Packet Radio Port 1: SCS - DSP MULTI MODEM detected
Packet Radio Port 2: NO MODEM detected
```

### Brief overview of the most important modem properties

The parameter # leads to a short output of the most important modem properties
in a special format. This simplifies the automatic configuration of a terminal
program and is therefore of particular interest to software developers.

The ## parameter always outputs the correct P4dragon modem string, regardless of the [`PTCComp`](#ptccomp) value.

The output format is structured as follows:

Each output parameter begins with #. This is followed by the unique parameter
number (ASCII, decimal) and a colon (:). The actual parameter follows the colon,
terminated by the following # or \<CR> (as a terminator for the entire string).

As property-parameters are defined (Numbers always in ASCII, decimal):

| | |
|-|-|
| **#0:** | (Modem type) |
| | A = PTC-II |
| | B = PTC-IIpro |
| | C = PTC-IIe |
| | D = PTC-IIex |
| | E = PTC-IIusb |
| | F = PTC-IInet |
| | H = DR-7800 |
| | I = DR-7400 |
| | K = DR-7000 |
| | L = PTC-IIIusb |
| | T = PTC-IItrx |
| | X = undefined modem type |
| | |
| **#1:** | (Firmware version number) |
| | 3.7b (example) |
| | |
| **#2:** | (Bootloader version number) |
| | 1.90 (example) |
| | |
| **#3:** | (Firmware attribute) |
| | N = normal firmware |
| | T = *tiny* firmware (up to now only for the PTC-II, without Robust-PR) |
| | |
| **#4:** | (Packet-Radio modems) |
| | 5A0A (example) |
| | |
| **#5:** | (PACTOR-3 License) |
| | N = no permanent license installed |
| | V = permanent license installed |
