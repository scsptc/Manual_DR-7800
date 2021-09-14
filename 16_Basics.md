Chapter 16

# Basics

## Why PACTOR?

PACTOR (*Latin: the mediator*) is a modern radio teletype mode developed
in Germany by **DF4KV** and **DL6MAA** to improve on inefficient modes
such as AMTOR and PACKET-RADIO in weak short wave conditions.

The AX.25 PACKET protocol certainly has its advantages on VHF/UHF FM
channels, but gives a lot of problems on short wave:

-   The data rate of 300 baud combined with a large packet length used
    by many radio amateurs is very susceptible on fading or multipath
    conditions and QRM.

-   The large protocol overhead dramatically reduces the amount of
    information contained in a packet.

AMTOR had been developed specially for transferring text on an HF
channel. Even weak signals under distorted conditions, where a PACKET
connect would never be possible, could be copied. But AMTOR also has its
disadvantages:

-   Using 5 bit code makes it impossible to transfer the whole ASCII
    character set or binary data.

-   Detecting and correcting errors is insufficient for error free
    transmission of binary data.

-   The effective data rate is only 35 baud.

PACTOR offers a much better error correction system, and a considerably
higher data transfer rate, than AMTOR. The synchronous transmission
format, and the short packet lengths of AMTOR, have been retained. These
result in a protocol much more resistant to interference than
Packet-Radio under poor propagation conditions.

The PACTOR protocol, together with the **SCS**-PACTOR Controller, allows
a much higher throughput than AMTOR, with the efficient error correction
and data transparency of Packet-Radio.

One should not, however, be under the impression that PACTOR is just a
combination of Packet and AMTOR! Although essential parts of both
systems have been included, such as data integrity, by using a CRC from
Packet, and the synchronous transmission format and short block lengths
(compared to Packet) of AMTOR, a fully new concept has also been
included from the very beginning. For the first time in amateur radio,
online data compression is used to markedly increase the effective
transmission speed. Also the use of memory ARQ in PACTOR is a milestone,
although it has been known for a long time in the commercial sector.

Previously it has been very difficult, or impossible, to apply this
concept in amateur radio. The use of memory ARQ is the main reason that
PACTOR does not loose the link under bad conditions. With memory ARQ,
defectively received packets or blocks are not just simply thrown away.
They are stored and added to other defective packets, until enough data
is collected to reconstruct the original packet, and thus keep the link
during operation. The original **SCS**-PTC uses a real analogue memory
ARQ, whereby the received AF tone is not simply turned into 0 or 1 data,
but intermediate values are also stored. Therefore a more fine-tuned
analysis is possible than with so-called "digital memory ARQ".

## Why PACTOR-II ?

PACTOR Level I has established itself, in the last few years, as the new
standard for FSK radio teletype on HF links. With PACTOR-I it was
possible, for the first time, to utilize the possibilities of an almost
ideal combination of simple FSK modulation combined with an ARQ protocol
nearly perfect. Even now, PACTOR-I, with analogue memory ARQ, has shown
itself to be the most robust, narrow band radio teletype system
available using FSK modulation, though another relatively similar FSK
ARQ protocol has recently been developed.

In the meantime, the signal processor technology (DSP) has reached a
stage where the implementation of high performance modems with a
reasonable price to performance ratio is possible, and because of this
it becomes interesting for the radio amateurs and? now a requirement -
as with the development of the PACTOR-I protocol about 8 years ago - for
a radio teletype system which takes maximum advantage of the
possibilities offered by modern hardware, and which can be classed as
"state of the art".

The main question was, what could be improved in PACTOR-I. A bit of head
scratching provided the answer. First of all a significant improvement
has to be done to the working range, which requires greater
adaptability. In practice this means that even extremely weak or
disturbed signals should still allow a connection, even if they are so
bad that PACTOR-I can no longer transfer data. On the other hand,
observations have shown that PACTOR-I links often work at 200 baud,
virtually without repetitions, on the higher bands. In any case, the
effective information speed (when required, i.e. when data is really
available) should be increased, so that data is transferred as fast as
propagation will allow.

For a new protocol the following conditions of compatibility should be
observed:

15. All advantages of the *old* protocol should be obtained.

-   Step synchronous ARQ protocol.

<!-- -->

-   Simple half-duplex operation with short packets during a direct QSO
    > (high *spontaneity*)

-   Full data transparency (binary, ASCII, Huffman, Markow, etc.).

-   Full support of analogue memory ARQ.

-   Should be able to connect under poor S/N ratio conditions, and with
    > a short phasing time. (no requirement for a valid CRC to connect,
    > therefore short pause times for scanning BBS).

-   Independence from sideband selection (no mark/space convention or
    > similar limitations).

-   Free choice for the center frequency of the audio signal in a range
    > between 400 Hz and 2600 Hz.

-   Longpath option (ARQ links over the long path possible).

-   Reliable QRT acknowledgment from both sides (not just a simple
    > time-out).

-   Fast and reliable change of data direction.

-   High performance *read* function without additional software.

-   Capable of running as a *stand-alone* controller i.e. independence
    > from IBM compa­tible PC’s.

16. Full compatibility with the *older* protocol.

-   Automatic switching between Level-I and Level-II at contact
    > initialization. (The user should be able to use the usual command
    > syntax **C** CALLSIGN to start a PACTOR contact, without having to
    > worry about the other station's system level).

17. A bandwidth of less than 500 Hz at -50 dB, so that operation within
    500 Hz channels is possible.

18. Constant bandwidth, irrespective of the actual effective
    transmission speed.

19. The acknowledgment signal (CS) should be equally as robust, or even
    more so, than the actual data signal.

All the above points are fulfilled with PACTOR-II, and not only those.
PACTOR-II uses an extended and better on-line data compression system
known as Markow coding. A reliable and automatic frequency correction,
adaptive cycle length, and many other useful features are also
incorporated.

## Basics of the PACTOR-II protocol

### General

The PACTOR-II protocol (PT-II) is essentially based on the Level-I
standard, consisting of a synchronous half-duplex ARQ protocol. New,
however, is the ability to choose four different speed steps, so that a
greatly improved adaptability is obtained. The modulation system used
for PT-II is based on DPSK (differential phase shift keying - see
below). which leads to a very narrow spectrum, practically independent
of the data rate. The robustness of the DPSK modulation qualifies itself
noticeably higher at lower information speeds in comparison to FSK. In
order to effect a further step towards robustness, PT-II uses high
performance convolutional coding, that is evaluated with a real Viterbi
decoder in the data receiver (see below). The high correction capability
of the decoder allows not only links with extremely weak or noisy
signals, but also, with more normal signals, enables short error bursts,
or fadeouts, to be entirely ignored, and a repetition of that packet is
not required. This is especially important with PT-II, as the new
protocol allows switching to a triple cycle length if there is enough
data in the transmit buffer. The relatively long resultant data packet
would be very prone to impulse errors from clicks or atmospherics (QRN),
if not for the highly effective error correction designed.

### The modulation system

As with the previous FSK standard, PACTOR-II also uses two tones (or
carriers). These are, however, not just sent alternately to transmit the
data, they are both sent together as continuous tones. The data is
contained in the phase of each tone, or, to be more exact, in the phase
difference between two consecutive information states or steps. The
keyword *step* should be more exactly explained, so that an essential
part of the PT-II modulation system, the pulse shaping, can be
understood. The FSK system uses rectangular keying (or steps)
throughout. With 100 Baud operation for example, a high (mark) tone of
exactly 10 ms is transmitted if a logical 1 is sent, or a 10 ms low
(space) tone if logic 0. Every step at 100 baud takes exactly 10 ms and
starts and stops very abruptly, i.e. a square wave. This abrupt keying
produces a relatively wide frequency spectrum. That the two tone FSK
keying bandwidth remains tolerable is only due to the fact that no phase
shift takes place during the tone keying (providing a correctly adjusted
modulator may achieve this). Phase modulation on the other hand, has, by
its very nature, a phase jump between each step. A square wave modulated
PSK signal has therefore a very wide frequency spectrum, and should
never be used on the (in any case much too narrow) HF amateur bands. The
number of steps (or changes) per second is called the *symbol rate*, or
(a little less correctly) baud rate.

Harry Nyquist, one of the most well known of the earlier communications
experimenters, developed, as early as the twenties, a mathematical model
that described exactly the relationship between bandwidth and the
maximum step speed, which finally led to his sampling theory. Stemming
from his work, a special step or impulse waveform was found that
contained the ideal characteristics for data transmission over an
electrical circuit.

A special version of this waveform, with even better characteristics,
led to the so-called "raised-cosine" waveform. (For insiders: the form
of the spectrum is equal to the squared cosine function, or the cosine
function plus one). The special properties of the "raised cosine pulse"
are as follows:

1.  The spectral bandwidth of a carrier modulated with the RC pulse is
    ideally only double the symbol rate (in hertz) - without any
    spillover or nearby spurious responses. In practice it is possible
    to reach a spurious attenuation of around -50 dB.

2.  At the sampling points (e.g. every 10 ms for a step speed of
    100/sec) the RC pulse presents a "zero crossing" to all except the
    *correct* sample point. This means that the impulse can be
    completely overlapped at the sampling distance, although the pulse
    itself may exhibit a multiple of the computed step length. This
    leads to a very high information density. To clarify this point,
    Fig. 3.1 shows the sampling points of a 100 baud RC pulse.

3.  Even the complete signal, comprising numerous overlapping RC pulses,
    always shows a "zero crossing" between the sampling points. This
    "zero crossing" enables any timing errors to be measured, and thus
    the PT-II system to be kept in synchronization.

It is obvious to use two RC modulated signals, with a spacing of 200 Hz
(*Shift*) in parallel. The complete signal then shows a spectrum 450 Hz
wide at minus 50 dB. PACTOR-II utilizes exactly this modulation scheme,
using two tones, and a modulation rate of 100/sec. This is a relatively
low value, and is a good compromise between robustness in noise, and
resistance to multipath effects. As the two tones work in parallel, the
PT-II system reaches a total modulation rate of 200/sec. The reason why
differential PSK is used on HF links is that signals are much too
unstable and noisy (or with too large a frequency error) to be used
effectively by "normal" coherent PSK detectors.

<img src=".//media/image26.wmf" style="width:4.84722in;height:2.43056in" />

Figure 16.1: Raised-Cosine-Pulse, Sampling points marked X.

<img src=".//media/image27.wmf" style="width:4.54167in;height:2.80556in" />

Figure 16.2: PACTOR-II spectrum 300 Bd FSK (200 Hz Shift)

For arguments sake, if there are only two possible phase changes between
the steps it’s called differential binary phase shift keying (DBPSK).
Every step contains exactly one bit of information. If four different
phase changes are allowed, then the modulation is called "differential
quadrature phase shift keying" (DQPSK). Every step of course then
carries two bits of information. With eight or sixteen allowable phase
changes, the modulation is called 8-DPSK or 16-DPSK, each step
containing three or four bits of information respectively. The required
signal to noise ratio, however, climbs rapidly, as the number of
allowable phase changes increases. Table 1 shows the total bit rates for
the PT-II modulation scheme (without data compression).

| **Modulation Scheme** |     | **Total bit rates (Bit/s)** |     |
|-----------------------|-----|-----------------------------|-----|
| DBPSK                 |     | 200                         |     |
| DQPSK                 |     | 400                         |     |
| 8-DPSK                |     | 600                         |     |
| 16-DPSK               |     | 800                         |     |

Table 16.1: Total Bit Rate

|     |                                                                                                                                                                                                                                                                                     |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | The complex PT-II modulation scheme is totally different to the simple FSK. Therefore it is IMPOSSIBLE to use the FSK modulators found in some transceivers to generate the signal. The PT-II signal must always go via the indirect route, by using SSB to generate the HF signal. |

This has actually no disadvantages, providing the transceiver is not
overdriven (see below).

A further very essential difference between the *older* FSK modulation
and the multi-tone DPSK modulation has to be mentioned. With FSK
modulation the output power of the transmitter remains constant during
the entire transmission because alternating square wave pulses of each
tone are transmitted, and mathematically the total amplitude adds up to
a constant function. This could be called a *constant envelope*.

As the amplitude remains the same, non-linear amplifiers, or even class
C power amplifiers, can be used without problems. Speaking about a
complex modulation method, e.g. used in PT-II, a more or less *variable
envelope* must be considered. This means, in practice, the following two
points have to be observed:

|     |                                                                                                                                                                                                                                          |
|-----|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | In all modulation methods using a changing amplitude HF signal (e.g. PACTOR-II, SSB-speech modulation, AM etc)., it is NEVER allowed to overdrive the transmitter because intermodulation products will be generated broaden the signal. |

How to adjust the maximum transmitter power will be described in the
PSKAmpl command (refer to chapter 6.74 on page 96). It always has to be
taken in consideration that, with a variable amplitude modulation
system, the effective average power is lower than the peak power. With
PACTOR-II this ratio between peak power and average power is almost
exactly 2. (For insiders: the square root of this ratio is called the
crest factor, and with PT-II has a value of around 1.45). This value is
considerably lower than with other multi-tone systems, and has shown
itself to be very well matched to the usual SSB transmitter. If one sets
a peak power of 100 watts, then the PT-II signal produces an average
output of about 50 watts. The full PEP output of an SSB power amplifier
can be thus used without great fear of overload, conditions being
similar to those existing during normal SSB speech transmission.

### Error control coding

The basic idea behind error correcting codes is that extra checking
information is transmitted along with the required data, so that the
*redundancy* of the signal is increased. The greater the efficiency of
the redundancy employed the better the code, and the greater its error
correcting abilities. The ratio of useful information to total
information (=useful information plus redundancy) is called the *code
rate*. A very simple code, the (7,4) Hamming code for example has a
*code* *rate* of 4/7, as for every four useful bits of information,
three redundancy bits are added. It can correct exactly one bit error
per block of seven bits. If however two or more bits have their polarity
changed in transmission, then this simple code fails.

The coding theory distinguishes between two main classes of codes: The
block codes and the convolutional codes. In block codes (e.g. Hamming
codes, the Golay code or Reed Solomon codes), the data stream is chopped
into relatively small pieces called blocks. The coding rules or
algorithm is then carried out on these blocks. Block codes were the
first to be developed due to their simplicity. Unfortunately, in
practice they have all proved to be rather weak, as only a very few bits
per block can be corrected. The (24,12) Golay code for example can only
correct a maximum of three bits in a block of 24, even though there is a
redundancy of twelve bits contained in each block. The coding rate is
therefore classed as 1/2. (for insiders: The problem with block codes is
mainly that they do not adhere to one of Shannon’s theorems. According
to Shannon, good codes should be as long as possible, and as
unsystematic as possible).

At the beginning of the sixties, the convolutional codes began to slowly
gain importance. In this form of coding, a message (or a data packet) is
coded as a complete entity. The actual encoder consists of a tapped
shift register, and carries out an algorithm which strongly resembles
the mathematical convolution integral - hence the name. The length of
the shift register is called the *constraint length*, and sets a limit
to the correction capacity that can be achieved. To decode convolutional
codes, a number of different methods can be employed. The optimum
decoder, that really can achieve the maximum possible gain from the
code, is called a Viterbi decoder. Unfortunately, there is an
exponential relation­ship between constraint length and the computing
time required by a Viterbi decoder. This is why the use of the Viterbi
decoder for real time tasks has been limited to a maxi­mum constraint
length of six for many years. The present day generation of DSP’s in the
meantime, allow use to constraint length nine or in special cases, even
more. As opposed to block codes, convolutional codes with a Viterbi
decoder easily allow the fine analogue resolution of the received signal
to be included in the decoding process, and hence even more gain to be
obtained. This method is called *soft decision*, and, depending on the
form of interference present, can give several dB additional gain
compared to *hard decision*.

Another point, which occurs often in connection with coding, is
so-called interleaving. This is nothing more than a shuffling of the
data. All codes, irrespective of whether block codes or convolutional
codes, when developed for maximum gain in noise, react more or less over
sensitively to short error bursts. On HF channels, the error burst (QRN,
clicks, short *fadeouts* etc). is about the most prevalent form of error
found. In any optimized error correction method for shortwave use, it is
obligatory to use interleaving. Usually the transmitted data is
dismembered into short blocks (e.g. 16 bit long strings) that are
stacked one over another in a memory. The data is then transmitted, not
in the original sequence, but in vertical rows. At the receiver, exactly
the reverse operation occurs. If during transmission, an error burst
takes place, this is cut into relatively widely spaced single bit errors
by the interleaving / de-interleaving process. These bit errors resemble
noise during the de­ coding, which the decoder is designed to handle
easily.

PACTOR-II is based on a convolutional code, with a constraint length of
9 and a Viterbi decoder with soft decision. The coding rate varies
between 1/2 and 7/8. The four possible speeds are shown in Table 16.2

<table>
<colgroup>
<col style="width: 27%" />
<col style="width: 17%" />
<col style="width: 54%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Modulation</strong></th>
<th><blockquote>
<p><strong>Coderate</strong></p>
</blockquote></th>
<th><strong>Net absolute throughput (bit/sec)</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>DBPSK</td>
<td><blockquote>
<p>1/2</p>
</blockquote></td>
<td>100</td>
</tr>
<tr class="even">
<td>DQPSK</td>
<td><blockquote>
<p>1/2</p>
</blockquote></td>
<td>200</td>
</tr>
<tr class="odd">
<td>8-DPSK</td>
<td><blockquote>
<p>2/3</p>
</blockquote></td>
<td>400</td>
</tr>
<tr class="even">
<td>16-DPSK</td>
<td><blockquote>
<p>7/8</p>
</blockquote></td>
<td>700</td>
</tr>
</tbody>
</table>

Table 16.2: The four speed settings and coding.

### Online data compression

As with the Level-I protocol, PACTOR-II uses Huffman coding for text
compression on a packet by packet basis. As an alternative, PACTOR-II
can also use pseudo Markov coding (PMC) as a compression method. PMC has
been developed by **SCS**, and in­creases the throughput of plain text
by a factor of 1.3 compared to Huffman coding. The PTC-IIpro examines
each packet individually to see if it would be faster to send it using
Huffman, PMC, or normal ASCII transmission. There are thus no
disadvantages incurred by using PMC. As a further selection criterion,
the PT-II protocol supports separate German and English coding tables
for PMC, as well as a capitals mode for Huffman coding and PMC. There is
a total of 6 different compression variations available for use. The
PTC-IIpro checks each packet automatically, and then very reliably
chooses the best compression method for transmitting the data.
Additionally, PT-II uses "run length coding", so that sequences of
repeated characters, e.g. underlining, or columns in graphics, may be
transmitted very efficiently. With "run length coding", the system does
not transmit each character individually, instead an sample character is
sent, followed by the required number of same.

A few words on how PMC functions would not be out of place here. Normal
Huffman compression makes use of the statistical frequency distribution
of characters in plain language text. The characters most used (e.g. ‘e’
and ‘n’ ) are coded with only two or three bits. Rare characters such as
‘Y’ can conversely be up to 15 bits long. On an average, one obtains a
symbol length of around 4.7 bits, which is a considerable compression
factor compared to 7 bit ASCII of constant length. The Markov coding, to
put it very sloppily, is like a *doubled* Huffman compression. Here it
is not just the simple frequency distribution of characters which plays
a role. Instead, the interest is in the frequency distribution of the
*leading’*or initial letter of any two byte sequence. Let us take our
example of an ‘e’. It is very probable that an ‘n’, an ‘r’ or a ‘t’ may
follow. On the other hand, it is extremely unlikely that an ‘X’ would be
the next character. The resultant frequency distribution is more
accurate than the simple frequency distribution of the characters in a
text, and therefore allows a better compression. Every *leading*
character should allow, in principle, its own Huffman code for the
following character to be built up. Every *leading* character therefore
lays down its own Huffman table for the following characters.

Unfortunately, although very convincing in theory, this system has two
very obvious weak points. Firstly, the coding table would be
impracticably large, as there would have to be a Huffman table for every
character. Secondly, the least common characters in particular, show a
very unstable (context dependent) resultant probability, and it must be
reckoned that particularly these characters would lead to a decrease in
the effective transmission speed with (non-adaptive) Markov compression.

The **SCS** team, in developing PT-II, came up with a simple and clever
answer to these problems. The Markov compression would be limited to the
16 most common *leading* characters. All other characters result in
normal Huffman compression. We have thus a hybrid of Markov and Huffman
coding, that we have named "pseudo Markov coding. The coding table
remains reasonably small, and the uncommon characters can no longer
cause trouble due to their unstable probability results. In practice it
has been shown that PMC almost always produces a greater benefit
compared to normal Huffman compression.

## PACTOR-II in practice

### General points

Those experienced users of PACTOR-I should have no trouble changing to
PACTOR-II, particularly if they know the usual commands of the **SCS**
controller for PACTOR operation. Before the first try-out on the air a
check should be made, using the **MYcall** command (refer to chapter
6.63, page 89), to see that one's own callsign has been correctly loaded
into the PTC-IIpro from the terminal program. If this should not be the
case, then put in the callsign manually using the **MYcall** command.
Other than this, it is essential that the AF output level, together with
the maximum output power in FSK and DPSK are correctly set. For this,
see the information contained in the description of the two commands
**FSKAmpl** (refer to chapter 6.42, page 80) and **PSKAmpl** (refer to
chapter 6.74, page 96). Once that has been done, then one is ready to
start. The transceiver can be tuned to say 3583.7 kHz or 14079.0 kHz,
and DL2FAK called (providing the frequency is clear). If there is PT
traffic on the chosen frequency, irrespective whether PT-I or PT-II, the
PTC-IIpro will automatically copy it, providing the Listen mode is
turned on (refer to chapter 6.50, page 83). As with previous PTCs', a
connect is started with

**cmd:** **C** CALLSIGN \<Return>

At the very start of a link, the two controllers automatically agree to
use the highest common level. This functions with all known PACTOR-I
equipment, as these all contain a correct implementation of the Level-1
protocol for the initial link. At present, we know of no PT-I
implementation which does not work correctly with the automatic level
setting during the initial link-up. The user knows virtually nothing of
the auto level setting procedure and does not have to concern himself
with it. In the case where a Level-II link is set up, the LED display
jumps from PT1: to PT2: and the appearance of the tuning indicator
changes drastically in comparison to the usual FSK tuning help.

### The tuning indicator and tuning behavior

The tuning indicator consists of 15 dual color LED’s, which, during
Level-II operation, not only show the quality of the received signal,
but also its frequency offset. Unlike with FSK operation, these two
operations are practically independent of each other. With an error free
received DPSK signal, only the two outer LED’s should flicker. If the
signal contains noise or other interference, then some of the middle
LED’s will flicker, more or less brightly, depending on interference.

The frequency offset is shown separately with one of the 13 inner tuning
indicator LED’s. If the tuning is exactly correct, then the centered LED
is permanently lit. An offset of between ten and sixty Hz causes a
shifting of this LED to the left or right by approximately one position
per 10 Hz. A shift to the right means the frequency of the partner
station is too high. A shift to the left means it is too low. If the
difference is greater than ± 60 Hz, then the next to the last tuning LED
blinks.

|     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|-----|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | The DPSK demodulator can only operate correctly when it knows the receive frequency accurately to within a few hertz. Decisions of this accuracy require time. Manually tuning the VFO or using the RIT control on the transceiver **must** therefore cause a number of defective packets to be received, leading to repetition requests. The highly robust and reliable automatic frequency compensation, built into the PTC-IIpro, needs a few seconds to be sure that a sudden frequency change has in fact occurred. |

Manual intervention to the tuning does not normally need to be
undertaken, providing the automatic frequency parameter (**AQrg**)
(refer to chapter 6.5, page 61) is set to ‘1’. The PTC then adjusts
itself automatically to the optimum receive frequency. The QRG display
LED can be seen to slowly but surely slide into the center position
within a few minutes. (If this should not be the case, then check the
AQrg command is set to ‘1’, see AQrg command).

The tuning indicator functions also when using the ‘Listen mode’,
copying PT-II signals within ±50 Hz of the correct frequency, exactly as
per the connected condition. Here however, the operator should undertake
the frequency correction manually, as the PTC-IIpro does not operate
with auto QRG in the Listen mode.

### Speed and robustness

When compared to good old PACTOR-I, PACTOR-II achieves an effective text
throughput of around 3 times that of PT-I under average to poor
conditions. With very weak signals, or signals with heavy interference,
PT-II still works when PACTOR-I will not allow any more data to be
passed. Naturally however, the speed of transfer, even with PT-II, drops
accordingly. One must get used to the fact, that, with practically
inaudible signals, one must wait 20 or 30 seconds for a new line to
appear on the computer screen. It has NOT proved to be a disadvantage to
continue working with longer packets when signals are weak or under
heavy interference. The transmit buffer naturally rapidly fills up under
these conditions, causing the PTC-IIpro to switch automatically to
longer packets. Only the waiting time until a new line of text appears
on the screen increases with the longer packet length, under extremely
unfavorable conditions. The effective throughput, however, remains
considerably higher than when using shorter DBPSK packets. If the link
threatens to break, then the MAXError parameter (time-out) can be
increased to 255, and the Memory ARQ parameter (MAXSum) may be increased
to 60 during the contact. **NEVER tune the VFO by hand with very weak or
inaudible signals!** With very weak or noisy signals, the PTC-IIpro
adjusts its tuning very slowly to minimize tuning error. With good, to
very good, propagation conditions, PT-II has shown itself to be 4 to 6
times faster than PACTOR-I. A maximum speed of 140 characters per second
can be achieved. This is approximately 30 times the effective AMTOR
speed.

Switching between speeds occurs automatically. The operator can
influence this a little by using the MAXUp and MAXDown parameter, as
with Level-I PACTOR. The PTC-IIpro not only uses the packet statistics
as a switching criterion, but also measures the average phase offset
from the correct value for every packet, and thereby obtains a very
reliable measure of the optimum speed required.

**Important:** The PTC-IIpro only switches to a higher speed if there is
more data available to be transmitted, than the actual speed could
transmit.

### CQ calls and broadcasts

As with PACTOR-I, a CQ call or broadcast is normally carried out with
100 Bd FSK UNPROTO mode (see the **Unproto** command (refer to chapter
6.102, page 112). Such transmissions can be read by all PACTOR users.
If, however, only those users with Level-II systems should be addressed,
then a DPSK-Unproto transmission can be chosen. We recommend the
Unproto-3 mode for a DPSK CQ call. This is DBPSK with short packets, and
has proved to be the most robust broadcast mode under normal conditions.
