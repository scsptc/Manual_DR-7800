# SYStest

The system test is not normally required by the PTC user, but has been included here for the sake of completeness. **SYStest** is purely a tool to diagnose and rectify faults in defective PTC's. In normal operation this function is not needed. |

The command `SYStest` (without argument) activates the systemtest
menu. (**sys:**-menu). The command prompt takes the form **sys:**.

Within the **sys:**-menu, the following systemtest commands are allowed:
```
Beep, CHKBL, CHKFlash, Flash, GPSspeed, Help, HWInfo, Led, LOG, Ptt, Quit, SCANSTOP, SERNum, Trxtest, TUnit
```

All other (*normal)* commands are not available! You can leave the **sys:**-menu with [`Quit`](#quit) or [`DD`](#dd).

The `SYStest` command may also be followed by an argument, which
should be a command from the **sys:**-menu. In this case, the modem
carries out only that given systest command, without switching to the
**sys:**-menu.

This command for example would show the PTC-IIpro RAM expansion.

`cmd: SYS Beep<Return>`

The **sys:**-menu commands in detail:

## Beep

Activates the micro loudspeaker in the PTC-IIpro briefly. With correct
operation, a short signal tone should be heard.

## CHKBL

## CHKFlash

## Flash

## GPSspeed

## Help

Gives a short list of the **sys:**-menu commands. The `Help` command
may be followed by a command from the **sys:**-menu as argument, whereby a
description of that command is given.

Help to the `Beep` command

`sys: Help Beep<Return>`

## HWInfo

## Led

LED test.

## LOG

## Ptt

Activates the PTT test routine. The PTT switching transistor is toggled
on or off by means of \<Return>. The PTT test routine can be ended with
\<Q>.

## Quit

Leaves the **sys:**-menu. The command prompt returns to its *normal* form
(**cmd:**). Identical to the [`DD`](#dd) command of the **sys:**-menu.

## SCANSTOP

## SERNum

`SERNum` displays the serial number of the modem. This number alwas has 16 digits, e.g.
```
Serial number: 01000005A6E69C22
```

## Trxtest

Tests the transceiver control port. This command is only working
properly when using a special test adapter on the TRX-control connector.

## TUnit

