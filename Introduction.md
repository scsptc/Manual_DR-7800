# Introduction

## SCS-PTC, the Original

Thank you for having decided to purchase the **SCS**-P4dragon DR-7800. The **SCS**-P4dragon DR-7800 is the original, develped by those people that invented
PACTOR. Only from **SCS** you receive the best possible
support. The concentrated knowledge of the PACTOR-engineers is
available to you.

Mit dem P4dragon DR-7800 stellt SCS eine vollständig neuentwickelte Serie von PACTOR-4-fähigen Kurzwellen-Modems vor. P4dragon steht für ausgeklügelte nachrich- tentechnische Algorithmen und hohe Rechenleistung in PACTOR-Controllern der vierten Generation.

## Requirements

To operate PACTOR, a transceiver capable of switching between transmit
and receive within 20 ms is required. Therefore any transceiver capable
of AMTOR can also be used for PACTOR.



## About this manual

This manual contains information on the installation and operation of
your **SCS** PACTOR Controller P4dragon DR-7800. The shortform for PACTOR Controller is
PTC and is used in this manual alternatively.

The manual may be used as a reference manual for the PTC commands and as a hardware reference.

The section 3 shows how to *quick start* the PTC-IIpro. Section 16 gives basic introduction about PACTOR and PACTOR-II. Section 5 shows the command structure and operation of the PTC.

**You should additionally read sections** **6.42** and **6.74**. Here it is explained how the audio output signal from the PTC-IIpro is adjusted for FSK and PSK operation.

All descriptions in this manual refer to the default settings of the PTC-IIpro. This is very importand especially with respect to the freely definable control characters (ESCAPE-character in section 6.39 on page 79, BREAKIN-character in section 6.12 on page 64 CHANGEOVER-character in section 6.19 on page 67 and QRT-character in section 6.79 on page 97. |

### Typography

Characters inside pointed brackets \<\> in the following text mean that the corresponding key or key combination should be pressed. \<ESC> means that the ESCAPE key should be pressed. \<RETURN> characterizes the
RETURN or ENTER key, and \<Ctrl-D> that the Ctrl key should be
pressed together with the 'D' key. All commands are closed with
\<RETURN>. Commands may be input either in upper or lower case letters, or a mixture of the two.

## HF-email

If you intend to use the PTC-IIpro for HF-email only and not for
amateur-radio purposes then 95% of this manual are not necessary for you
to read. HF-email is deeply associated with the email-client
(PC-programm) you use and your service provider. The email-client (e.g.
Airmail) automaticly does most of the configurations needed and lets you
successfully transfer email at a fraction of knowledge which this book
presents. So don´t feel bothered by the thickness of the book but have a
look into the documentation of your email-client, which will provide a
well tailored description of all you need for HF-email.

If you´re still looking for an email service provider then refer to our
homepage where you find actual links to the sites of many service
providers. When you have choosen a service provider then follow his
instructions on which software you need on your PC and how it needs to
be configured.

## The SCS CD-ROM

The **SCS** CD-ROM contains software to operate the PTC-IIpro in various modes.

### The programs

The PTC-IIpro offers many modes of operation of which most are related
to the exchange of text or data. In addition, picture modes like FAX and
SSTV are supported. To access and operate your PTC-IIpro you must run a
software program on your computer (PC). Although very simple terminal
software (i.e. Windows HyperTerminal) will control a PTC-IIpro, it is
much more convenient to use a program which has been specially created
to operate the **SCS** PTC-II series.

Many of the programs have been written on a voluntary base and are
available free of charge to all users and distributed via the Internet.
With the permission of the authors we have included the programs on our
**SCS** CD-ROM. Third party programs are **not** developed by **SCS**
and **SCS** cannot provide support for them. If you have problems or
questions concerning the programs, please contact the author directly.
Table 1.1 below gives you an overview on the software available for
specific applications.



-  We are frequently asked “What is the best program for the
    > PTC-IIpro?”. This question cannot be answered easily as it is
    > similar to someone asking “What is the best car?” or “What is the
    > best operating system?”. It’s a question of personal preference
    > and depends on the application.

> If **HF email** is your application for your PTC-IIpro, it may not be
> necessary to study Table 1. In most cases, your HF email service
> provider supplies or recommends the appropriate software for their
> particular service.

-   Transceiver control is possible with the PTC-IIpro only, not with
    > the PTC-IIe/ex.

-   Windows programs usually need Windows 98 or higher.

-   PlusTerm and EasyTransfer are the only programs that have been
    > developed by **SCS**.

-   The **SCS** CD-ROM is usually updated twice the year. Always check
    > if there is a newer version of your selected program available
    > from the Internet.

### Version numbering

Each (software) *component* has an own version number. The Bootloader, the firmware, the programs for the PC and the user manual. The different version numbers are necessary to distinguish between old and new versions.

### File types

Basicly the following file types (extentions) are used:

| Extension | Description                     |
|----------|---------------------------------|
| **.TXT** | Text english or german           |
| **.GER** | German text                     |
| **.ENG** | English text                    |
| **.DR7** | Firmware file for the P4dragon modems |

## Professional solutions

**SCS** has developed a Professional version of the firmware which
enables new modes for the PTC. The “Professional Firmware” meets many
special requirements for mobile and maritime users and services. It also
provides the high-speed **PACTOR-III** mode.

**The following overview shows the Professional Firmware features:**

-   PACTOR-III highspeed data transfer protocol.

-   Hayes compatible command interpreter, Hayes-mode (phone modem
    > compatibility).

-   PACTOR-IP-Bridge, direct “TCP/IP over PPP” via HF.

-   PACTOR-Free-Signal-Protocol, collisions-avoiding access system to HF
    > data services.

-   More robust protocol for the PACTOR link establishment
    > (“Robust-Connect”).

-   CCIR 491-Number-SelCalls (4- and 5 characters), as well as
    > WRU-identifier and Answerback for comfortable access to
    > SITOR-coast-stations.

|     |                                                                                                                                                                                                                                                                                                                                                                     |     |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----|
|     | For permanent usage of the extended firmware features you need a license key from **SCS.** Without this key you can test the extended features for 20 connects. Refer to **LICENSE** command chapter 6.47on page 82. For prices and detailed information (manual) about the Professional Firmware refer to our homepage: [www.scs-ptc.com](http://www.scs-ptc.com). |     |

### PACTOR-III

PACTOR-III is a third generation HF protocol building on latest
developments in 2-dimensional orthogonal pulse shaping, advanced error
control coding, and efficient source coding. Due to the advanced signal
processing methods applied, PACTOR-III provides outstanding performance
under poor and moderate signal conditions. As PACTOR-III also achieves
very high throughput rates under good signal conditions, it is
well-suited to HF channels with good SNR and low signal distortion as
well. During the development of PACTOR-III, high importance was attached
to compatibility with ordinary SSB transceivers (using standard 2.2-2.4
kHz wide IF-filters). Therefore, PACTOR-III can achieve its maximum
speed with using unmodified, common SSB transceivers. The occupied
bandwidth is around 2200 Hz.

Thus PACTOR-III is the ideal means of fast and reliable data
communication over (the sometimes difficult medium) HF-radio. The new
protocol is fully backwards compatible to existing PACTOR-I/II networks.

**The properties of the PACTOR-III protocol summarized:**

-   Under virtually all signal conditions, PACTOR-III is faster than
    > PACTOR-II. Under average signal conditions a speed gain by a
    > factor 3x to –4x is achieved, under very favourable conditions the
    > speed improvement can exceed 5x.

-   Maximum data throughput (without compression) greater than 2700
    > Bit/sec, around 5200 Bit/sec if PMC (online text compression) is
    > applied.

-   PACTOR III is at least as robust as PACTOR-II under extremely poor
    > signal conditions.

-   Maximum bandwidth only about 2200 Hz.

-   Low crestfactor (high mean output power).

-   High spectral efficiency – PACTOR-III makes very good use of the
    > bandwidth.

-   Fully backwards compatible to existing PACTOR-I/II networks.

### PACTOR-IP-Bridge

The PACTOR-IP-Bridge (PIB) is a new Network –Integration Protocol
developed by **SCS**. The dominant protocols of the Internet like
TCP/IP, as well as the Point-to-Point Protocol (PPP), which have become
standard for establishment of links between Internet applications, are
combined with the PACTOR modes. The result of this intelligent protocol
combination is a data transparent and relatively fast Internet access
via HF-radio using standardized user interfaces. The PTC appears to an
attached PC as if it were a Hayes compatible "telephone modem”. The PTC
locally takes over both the complete PPP and TCP/IP handling. Except for
a minimum fraction of protocol overhead, the physical PACTOR link only
carries useful data. The huge amount of overhead of the TCP/IP and PPP
protocols (which are designed for broad banded wired links) is reduced
to the absolute minimum required. By locally carrying out the PPP
protocol between the PC and the PTC a further decisive advantage arises:
Because of the very short timeouts, PPP used to be nearly impossible
over slow communication channels with relatively large delays. Timeout
problems are now solved by the PACTOR-IP-Bridge.

Summarizing the qualities of the PIB:

-   TCP/IP-transparent and relatively fast Internet access via HF-radio.

-   Internet-services accessible via PACTOR, e.g. E-Mail (SMTP/POP3),
    > FTP, HTTP, ...

-   Up to 4 Internet channels ("sockets") over one physical PACTOR link.

-   Extreme compression of the TCP/IP and PPP"overhead".

-   Full PPP compatibility: Use of common client/server-software, like
    > Netscape, Outlook, Eudora and others is possible.

-   Easy embedding and configuration under all common operating systems.

-   No "timeout"-problems on PPP and TCP/IP.

As host system for the PACTOR-IP-Bridge **SCS** has developed the
PTC-IInet.

A detailed manual for the *Professional Firmware* can be found on our
homepage <http://www.scs-ptc.com>.

### EasyTransfer

EasyTransfer is a program developed for binary transparent
file-transfers between two computers connected via PACTOR. The graphical
user interface is similar to some well known FTP clients, which are used
for file –transfers via the Internet. When viewing the software user
interface, the left side shows the contents of the local hard disk, on
the right are the contents of the enabled REMOTE directory of the PACTOR
connected server. Files can easily be moved between the two sides using
standard drag-and-drop actions. In addition to FTP, EasyTransfer has a
“chat” mode to exchange hand typed messages. With that, EasyTransfer is
the ideal tool to exchange computer data via HF and over unlimited
distances.

<img src=".//media/image1.wmf" style="width:6.01389in;height:2.11111in" alt="pro-box" />

Figure 1.1: The **SCS** PTC-IIpro
