Power
-----

The power input is located on the rear of the unit. The power supply
provided is a "desktop" type brick with a three-prong IEC input connector.
An AC power cord compatible with U.S. power outlets is optional. There is no
power switch; it is on when the power is applied.

Serial Console
--------------

The serial console port is located at the rear of the unit. It is an RJ-45
with a three-wire RS-232 level interface. The interface has the same pinout
as found on Cisco routers and switches. The baud rate factory default is
115200, 1 stop, no parity, 8 bits. The baud rate can be changed by software
command – see the [BAUD](#_BAUD) command in the Command Reference section.
Characters are echoed as they are typed (full duplex).

RJ-45 Connector:

| **Pin** | **Signal (DTE name)**    |
|---------|--------------------------|
| 1       | \*\*                     |
| 2       | \*\*                     |
| 3       | RS-232 data output (TxD) |
| 4       | Ground                   |
| 5       | Ground                   |
| 6       | RS-232 data input (RxD)  |
| 7       | \*\*                     |
| 8       | \*\*                     |

\*\* these signals are connected to each other

UUT Connections
-------------------

The RT-PoE5 has 24 test ports, configured as 12 pairs (1-2, 3-4, 5-6, etc.).
Each port can act as a PD load to the UUT. Also, each port pair can be
configured to pass data from one port to the other via internal
straight-through connections, allowing the loads to be applied while passing
traffic. All data path connections are made via signal relays and 100 ohm
differential pairs for data integrity.

Connect the port of the PoE supplying device under test to the UUT connector
via a standard straight-through Ethernet connector (see the [Ethernet
Cables](#_Ethernet_Cables) section for more information regarding cables).
There is an 802.3bt class transformer isolating the UUT ports in each port
pair so that power can be tapped from the UUT (see the [Data
Path](#_Data_path) section for more details).

Note that the devices connected to any given port pair cannot "see" the
power from the other port. In other words, the UUT ports in a port pair are
connected from a data perspective, and each UUT port connects to the RT-PoE5
active load from a power (PoE) perspective.

***NOTE: with high power loads, the DC balance of the patch cables used is
important to avoid DC saturation of the Ethernet transformers. DC Balance
(DC resistance per side of the power-carrying pair) should be within 3%. The
standard patch cable specifications of Cat 5, 5e, and 6 do not specify DC
balance.***