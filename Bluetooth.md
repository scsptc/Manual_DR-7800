# Bluetooth

The Bluetooth menu (**bt:**-menu) can be activated from the main menu of the P4dragon DR-7800 with the `BT` command.
The command prompt takes the form **bt:** and only the Bluetooth commands apply.

## Help

`Help` without parameters gives a list of all available commands.

The modem contains a short description of every command, so that the
manual does not need to be continually consulted. These descriptive
messages can be obtained by using `Help`, followed by the required
command, e.g. `Help PASSKEY`.


## ID

|                  |     |                        |
|------------------|-----|------------------------|
| Default setting: | 0   |                        |
| Parameter:       | 0   | Standard Bluetooth ID. |
|                  | 1   | Extended Bluetooth ID. |

Set the Bluetooth ID extension.

If set to 1 the Bluetooth ID get's extended by the last 4 digits of the
silicon serial number, e.g. **SCS DR-7800-X23A**.

**Not available with all Bluetooth modules!***


## MAC

Shows the MAC address of the Bluetooth module.


## PASSKEY

|                  |      |               |
|------------------|------|---------------|
| Default setting: | 0000 |               |
| Parameter:       | X    | 4..8 numbers. |

Change the Bluetooth passkey. The passkey may consist of 4 to 8 digits (0..9).

Example: `passkey 1234` set 1234 as the new passkey.


## Quit

Leaves the **bt:**-menu. The command prompt returns to its
*normal* form (**cmd:**).
