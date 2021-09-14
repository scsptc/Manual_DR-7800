# Audio

The Audio-denoiser-menu (**aud:**-menu) is activated with the command
`AUdio`. The command prompt takes the form **aud:** .

The following commands are available in the **aud:**-menu:
```
AUXInput, CHannel, COpy, COPYGain, DD, Help, Level, Quit, Through, TOne
```
All other (*normal*) commands are not available in the **aud:**-menu!
`Quit` or `DD` exit the **aud:**-menu.

The commands of the **aud:**-menu in detail:

## AUXInput


## CHannel


## COpy


## COPYGain


## DD

Leaves the **aud:**-menu. The command prompt returns to its
*normal* form (**cmd:**). Identical to the [`Quit`](#quit) command in the **aud:**-menu.

## Help

Lists all available commands in the **aud:**-menu.

## Level

Default setting: 50  
Parameter: X 0... 100, output level of the audio-amplifier.

The `Level` command sets the volume of the internal audio amplifier
which supplies the speaker that can be connected to the PTC-IIpro.

## Quit

Leaves the **aud:**-menu. The command prompt returns to its
*normal* form (**cmd:**). Identical to the [`DD`](#dd) command in the **aud:**-menu.

## Through

Loops through the Audio signal direct, i.e. without filtering, from the
input (ADC) to the output (DAC).

## TOne

Default setting: 1000  
Parameter: X 1... 4000, frequency in Hz.  
           Y 1... 4000, frequency in Hz.

Starts the sine wave generator. The frequency required is given as an
argument for the command. The range covers 1 Hz to 4000 Hz with a
resolution of 1 Hz. The command without an argument delivers a tone of
1000 Hz.

The command can also be used to setup a dual tone generator. For this,
the second frequency is entered after the first one, separated by a
space. Both tones are generated simultaneously, which is well suited for
measurements of intermodulation distances of transmitters and power
amplifiers.

Example:
```
aud: TO 1000 2000<Return>
```

generates a two-tone signal of 1000 **and** 2000 Hz the same time.

The amplitude may be set using the `FSKAmpl` command from the main
menu (refer to chapter 6.42, page 80).
