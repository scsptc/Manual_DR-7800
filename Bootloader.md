# The Bootloader

The internal operating software of the P4dragon DR-7800 is divided into two major parts:

**Firmware:**  
Operating software available to the user, which supports,
for example, PACTOR, AMTOR, RTTY, etc, including the command interpreter and multitasking. and for which an update is occasionally available, to provide additional, and improve, current features. These updates are readily loaded into the PTC-IIpro using **UPDATE.EXE** or **PlusTerm**.

**Bootloader:**  
The BIOS allows some of the basic functions of the PTC system to be used and works totally independently from the presently loaded firmware. The BIOS has a very basic and essential task, and is thus is placed in a specially protected area of the FLASH memory.

Normally, the user does not need to worry about the existence of the
BIOS. However due to various unlucky or exceptional circumstances, it is possible that the PTC-IIpro will no longer load the PACTOR firmware. Under these conditions, it is only possible to access the PTC-IIpro via the BIOS.

If, for example, there is a power failure during a normal firmware
update, one part of the FLASH is programmed with the new version, while the other still contains a part of the old firmware. It is very unlikely that such a mixture will run, and the BIOS is then the only way that the update can be repeated.

The BIOS is automatically activated as soon as the PTC-IIpro detects an error on loading the PACTOR firmware, or the user wishes access to the BIOS.

## Bootloader and Firmware

What happens after powering on the modem?

The following lines explain the behavior of BIOS and fimware of the
PTC-IIpro to interested users.

First of all the BIOS controls the PTC-IIpro. After BIOS has been successfully started it initiates the LED´s, the serial interface, the RAM and the other peripherals. In the meantime the BIOS performs a light-show as a sign of life. Next of all it is checked if the user wants to activate the BIOS. In this case the command interpreter of the BIOS is activated and the commands described in the following chapters are available. The PTC-IIpro indicates **BIOS 1.58** in the display.

The BIOS checks if a firmware is loaded properly into the RAM by using a signature. If a firmware is detected a checksum is calculated over the program codes and checked for validity. If this test is positive then the firmware in the RAM is started directly.

If one of the two tests mentioned before is negative, the firmware has to be loaded from the Flash-ROM into the RAM. This procedure has two reasons. The first is that the firmware is contained by the Flash-ROM only in compressed form and the second is that Flash-ROM has only 8 bit data-bus width. Within the RAM 32 bit are available so that the firmware runs significantly faster.

The loading takes some time and is displayed within the LED display with **loading**. After unpacking and loading the firmware the BIOS has finished its job and now the firmware is responsible for controlling the PTC-IIpro.

## Activating the BIOS

As the PTC-IIpro has no switches to let the user express the intention to operate it with the BIOS a special procedure is used to activate the BIOS.

The PTC-IIpro performs a LED test when powered on. This test has 2 phases, first the LED´s are red and afterwards they appear green. When the PTC-IIpro is switched OFF again whilest performing the LED-test, then at next power up it will come with the BIOS. Being in the BIOS the PTC-IIpro indicates by indicating **BIOS 1.90** in the display.

The BIOS can be terminated by switching the unit OFF again. This can also be done with the OFF command of the BIOS (refer to 14.3.5 on page 219). At next power-on it will start the firmware again.

## Bootloader commands

### DAte

**Default setting: none**  
Parameter: DD.MM.YY - Desired date.

Identical to the `DAte` command in the PACTOR firmware.

**DAte** is used to set or read the PTC calendar. If **DAte** is entered
without a parameter, the PTC-IIpro displays the current date. All
positions have to be entered. Leading zeros must not be omitted. The
hyphen for separation are not necessary. Faulty inputs cause incorrect
programming of the clock chip!

From 01.01.1990 up to 31.12.2089, the day of the week is automatically
calculated from the date. Thus your PTC-IIpro is well equipped for the
future!

Required date Sunday 24th March 1991.

**cmd:** **DA** 24.03.91 \<Return>

Or in shortform

**cmd:** **DA** 240391 \<Return>

###  FCall

|                           |      |     |                                |
|---------------------------|------|-----|--------------------------------|
| **Default setting: none** |      |     |                                |
|                           |      |     |                                |
| Parameter:                | CALL |     | Flash call, max. 8 characters. |

Checking and setting of the flash call. By using the **FCall** command,
it is possible to store your own callsign permanently in FLASH ROM.

Stores the flash call DL3FCJ

**cmd:** **FC** DL3FCJ \<Return>

Checking the flash call.

**cmd:** **FC** \<Return>

The flash call is used as default callsign by the PACTOR firmware after
a **RESTart**.

### FSelcall

|                           |         |     |                                  |
|---------------------------|---------|-----|----------------------------------|
| **Default setting: none** |         |     |                                  |
|                           |         |     |                                  |
| Parameter:                | SELCALL |     | Flash-Selcall, max. 4 characters |

Checking and setting of the flash selcall. By using the **FSelcall**
command, it is possible to store your own selcall permanently in FLASH
ROM.

Stores the flash selcall DFCJ

**cmd:** **FS** DFCJ \<Return>

Checking the flash selcall.

**cmd:** **FS** \<Return>

The flash selcall is used as default selcall by the PACTOR firmware
after a **RESTart**.

### Help

Displays all useable commands. It is also possible to obtain further
helpon a command whilst in BIOS with Help \<CMD>.

More details to the **SERbaud** command

**cmd:** Help **SERBaud** \<Return>

or shortened to:

**cmd:** H **SERB** \<Return>

### OFF

Switches off the PTC-IIpro. With signals on the RS232 link the (e.g. one
or more \<return>) it switches on again.

In *off-by-command* condition the PTT-LED of the packet-radio port 2 is
blinking.

### SERBaud

|                           |          |                                                                          |     |
|---------------------------|----------|--------------------------------------------------------------------------|-----|
| **Default setting: auto** |          |                                                                          |     |
|                           |          |                                                                          |     |
| Parameter:                | baudrate | The serial interface of the PTC-IIpro is pre-set to the given baud rate. |     |
|                           | auto     | Automatic baud rate recognition.                                         |     |

Identical to the **SERBaud** command in the PACTOR firmware.

Sometimes it is obvious to avoid the automatically baud rate recognition
of the PTC-IIpro. This is for example is the case if the PTC-IIpro (the
whole station) is switched on and off by a timer. Also if you want to
react the PTC-IIpro on a hostmode program after switching on you have to
set the baudrate to a fixed value.

The **SERBaud** command allows the PTC-IIpro to be set to a certain baud
rate and to avoid the automatic baud rate recognition after switching on
the PTC-IIpro. The PTC-IIpro doesn’t display AUTOBAUD / press CR, but
will start directly!

To set the baud rate to 9600, just enter the following command:

**cmd:** **SERB** 9600 \<Return>

Switching on the PTC-IIpro the next time 9600 baud will be displayed!

To activate the automatic baud rate recognition again enter the
following command:

**cmd:** **SERB** auto \<Return>

Switching on the PTC-IIpro the next time the automatic baud rate
recognition will work.

Without entering arguments the **SERBaud** command shows the actual baud
rate. The message “auto” will be added if the automatic baud rate
recognition is turned on.

### SYStest

Switches to the **SYStest** commands. The command prompt changes from
**cmd:** to **sys:**.

### Time

|                           |          |               |     |
|---------------------------|----------|---------------|-----|
| **Default setting: none** |          |               |     |
|                           |          |               |     |
| Parameter:                | HH:MM:SS | Desired time. |     |

Identical to the **TIme** command in the PACTOR firmware

Arguments are ignored during remote control.

**TIme** is used to set or read the internal clock.

If **TIme** is entered without a parameter, the current time is
displayed.

When the clock is set, leading zeroes must not be omitted. The colons
can be omitted. Wrong entries cause a wrong programming of the clock
component.

**cmd:** **TI** 09:56:05 \<Return>

or

**cmd:** **TI** 095605 \<Return>

### UPDATE

Identical to the **UPDATE** command in the PACTOR firmware.

This command renews the PACTOR firmware in the Flash ROM of the
PTC-IIpro. It should only be used together with the corresponding
program on the PC.

### Version

Displays the version number of the BIOS.

## BIOS SYStest commands


### Beep

Produces a short beep tone.

### CFg

Configurations register readout and display in hexadecimal form.

### CHKFlash

Check Flash-ROM for valid PACTOR firmware.



### Help

Displays all useable commands. It is also possible to obtain further
help on a command whilst in BIOS with Help \<CMD>.

More details to the RUN command

**sys:** **Help** RUN \<Return>

### Led

Checks the LED´s. The PTC-IIpro tests the whole lighting console.

### Quit

End the SYStest.

### RUN

Start the PACTOR firmware.

### SERNum

**SERNum** displays the serial number of the PTC-IIpro. This number alwas has 16 digits. **SERNum** answers as follows:

Serial number: 01000005A6E69C22

### Trxtest

Tests the transceiver control port. Only works in conjunction with the appropriate test adapter!
