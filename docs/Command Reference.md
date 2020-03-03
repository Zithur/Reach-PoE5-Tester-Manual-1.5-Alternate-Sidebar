Command Reference
=================

>   This section describes the commands available. For typical command
>   sequences, see [Appendix B](#_B.1_Overview).

>   When the unit is ready for a command, it issues the default prompt
>   "RT-PoE5\>". The prompt may be changed via the "hostname" command so that a
>   unit can be identified by its prompt. Command buffering is not supported;
>   you must wait for the prompt before sending a command. The default baud rate
>   is 115200. This can be changed via the "baud" command and is preserved
>   across power cycles.

>   All commands are terminated by a \<return\> which is the HEX character 0x0D
>   (decimal 13).

>   Most commands have a short form version. The optional characters of a
>   command are indicated by the [ ] brackets.

>   Parameters shown within the \<\> characters are required parameters.

>   All commands that take "on" or "off" arguments can also take "1" and "0" as
>   arguments.

>   All commands that work with the pairs can use one of two different forms.
>   The first form, such as “conn 1” tells the PoE5 to connect both the main and
>   the alt pairs.

>   The second form lets the user specify values for each pair. A command such
>   as “conn 1,0” tells the PoE5 to connect just the main pair. Using the
>   command “conn 0,1” tells the PoE5 to connect the alt pair only. Using the
>   command “conn 1,1” is the same as using “conn 1”.

>   Responses from the unit that include variable data, such as the port number,
>   are shown as 'C'-language printf style strings, so the script writer knows
>   exactly what to expect as a response.

EEPROM Warning
--------------

>   **NOTE: The non-volatile memory used for EEPROM storage has a write cycle
>   limit of about 1,000,000 cycles. To prevent future issues, the user should
>   not include commands that write to EEPROM in repetitive scripts.**

<br>ECHO
--------

>   Description: Used to test the communication between the host and this unit.
>   This is useful at higher baud rates to validate a baud can be used without
>   error. A script can repeat the echo command continuously and verify that no
>   communication errors are present.

>   Command: echo \<string\>

>   \<string\> = any ASCII string. May contain spaces.

>   Example: echo this is a test

>   Response: "this is a test"

ERROR CHECK
-----------

>   Description: The unit maintains an error flag that is set if any error
>   messages are generated. This command reports the error flag value and then
>   clears the error flag. A test script can run an entire sequence of commands
>   and check at the end to make sure there were no errors instead of having to
>   check on a command-by-command basis.

>   Command: err[ors]

>   Result: "1 - one or more errors have occurred; error flag reset"  
>   - or -  
>   "0 - no errors have occurred"

HELP
----

>   Description Displays a list of available commands.

>   Command: he[lp]

>   Command: ?

>   Example: help

VERSION
-------

>   Description Displays software and hardware version

>   Command: vers[ion] [0\|1]

>   Result: "Reach PoE Tester Model RT-PoE5/24

>   PN 53-0005-11 Rev A 0/1, SW 1.04, Jul 19 2019

>   Copyright (C) 2019 by Reach Technology, a Novanta Company"

>   An error is generated if the line card versions are inconsistent; that is,
>   if the three 8-port line cards have different firmware. Use vers 1 to get a
>   verbose listing of version information with errors flagged.

BAUD
----

>   Description: Used to change the unit's baud rate. This will not take effect
>   until the unit power is cycled or the \*boot command is issued. This is done
>   to make sure the baud change is acceptable.  
>     
>   See [EEPROM Warning](#eeprom-warning).

>   Command: \*baud \<baudrate\>

>   \<baudrate\> = 9600, 19200, 38400, 57600, or 115200

>   Example: \*baud 19200

>   Response: "Console baud set to 19200. Cycle power or issue \*boot to effect
>   change."

BOOT
----

>   Description Resets the system to the power-on state. This is the same as if
>   the unit has its power cycled.

>   Command \*boot

HOSTNAME
--------

>   Description: Used to change the unit's prompt. This is useful in a
>   production system because it allows the user to know with which physical
>   unit it is communicating. Name must be equal or less than 31 characters
>   long.  
>     
>   See [EEPROM Warning](#eeprom-warning).

>   Command: \*host[name] \<string\>

>   Example: \*hostname myTester

>   This makes the unit's prompt "myTester\>"

SHOW ALL
--------

>   Description Shows the current (last-sent) state of all commands on each
>   port. Note that there is no ‘port’ or ‘group’ syntax for ‘show all’.

>   Command: sh[ow] all

>   Response: [See example below]

Example: show all

Example response: (table truncated for brevity)

|     | class | det   | cap | conn | set        | pwr    | ext | short | single | mps | inrush |
|-----|-------|-------|-----|------|------------|--------|-----|-------|--------|-----|--------|
| p1: | 3L,3L | OK,OK | 0,0 | 0,0  | 1000,1000  | \-SET- | 1   | 0,0   | 0      | 0,0 | 85     |
| …   | …     | …     | …   | …    | …          |        | …   | …     | …      | …   | …      |
| P8: | 4D,4D | LO,LO | 0,0 | 1,1  | \---PWR--- | 50,50  | 1   | 0,0   | 0      | 1,1 | 85     |

CLEAR 
------

>   Description Clear user settings in EEPROM. Note that there is no ‘port’ or
>   ‘group’ syntax for ‘\*clear’.  
>     
>   See [EEPROM Warning](#eeprom-warning).

>   Command: \*clear

>   Response: EEPROM clearing settings copy 1  
>   EEPROM clearing settings copy 1  
>   EEPROM settings cleared

LOAD 
-----

>   Description Load user settings from EEPROM. Note that there is no ‘port’ or
>   ‘group’ syntax for ‘\*load’.

>   Command: \*load

>   Response: EEPROM restoring user settings  
>   :p1 restored  
>   :p2 restored  
>   …  
>   :p24 restored

SAVE 
-----

>   Description Save current user settings to EEPROM. Note that there is no
>   ‘port’ or ‘group’ syntax for ‘save’.  
>     
>   See [EEPROM Warning](#eeprom-warning).

>   Command: \*save

>   Response: EEPROM saving configuration  
>   EEPROM user settings saved

PORT / GROUP PREFIX
-------------------

>   Description For all port-specific commands, a port or group prefix will
>   restrict the command to a specific port or port group. The prefix must be
>   followed by a space before the port command. If no prefix is used, the
>   command will be applied to all 24 ports.

>   Port Prefix: pN

>   This specified port N where N is from 1 to 24.

>   Group Prefix: gN

>   This specifies group N where N is from 1 to 3.

>   group 1 = ports 1-8

>   group 2 = ports 9-16

>   group 3 = ports 17-24

CAP
---

| Description | Controls the 10uF capacitor across the full-wave bridge. This represents either a legacy capacitive signature or an AC load. Using two values separated with a comma allows the main and alt pairs to be set differently, or a single value will be applied to both pairs. The default state is off for both pairs. |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|             |                                                                                                                                                                                                                                                                                                                     |
| Command:    | cap \<on\|off\|0,0\|0,1\|1,0\|1,1\>                                                                                                                                                                                                                                                                                 |
|             |                                                                                                                                                                                                                                                                                                                     |
| Response:   | printf(":p%d cap %d\\r\\n", port, state);                                                                                                                                                                                                                                                                           |
|             | - or -                                                                                                                                                                                                                                                                                                              |
|             | printf(":p%d cap %d,%d\\r\\n",port,stateM,stateA); state = 1 or 0 for on and off respectively.                                                                                                                                                                                                                      |

CLASS – Single Signature
------------------------

| Description | Sets the IEEE load class while in single signature mode. See IEEE 802.3af, 802.3at, and 802.3bt specifications (external documents). The default setting is 0. |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
|             |                                                                                                                                                                |
| Command:    | cl[ass] \<0\|1\|2\|3\|4\|5\|6\|7\|8\>                                                                                                                          |
|             |                                                                                                                                                                |
| Argument:   | class value                                                                                                                                                    |
|             |                                                                                                                                                                |
| Response:   | printf(":p%d class %d\\r\\n", port, class);                                                                                                                    |
| Example:    | sin 1                                                                                                                                                          |
|             | p9 cl 6                                                                                                                                                        |
| Response:   | :p9 class 6\<CR\>\<LF\>                                                                                                                                        |
|             | This sets port 9 IEEE "class" to 6.                                                                                                                            |

CLASS – Dual Signature
----------------------

| Description | Sets the IEEE load class while in dual signature mode. The command supports both the Type 1/2 “Legacy” class settings and the Type 3/4 “Compliant” class settings. See IEEE 802.3af, 802.3at, and 802.3bt specification (external documents). Using two values separated with a comma allows the main and alt pairs to be set differently, or a single value will be applied to both pairs. Use a capital ‘L’ after the class number to specify the dual signature legacy class. If left off, the compliant class setting is used. The default setting is 0 for both pairs. |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Command:    | cl[ass] \<0\|1\|2\|3\|4\|5\>[, 0\|1\|2\|3\|4\|5]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|             | - or -                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|             | cl[ass] \<0\|1L\|2L\|3L\|4L\>[, 0\|1L\|2L\|3L\|4L]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Argument:   | class value (append a capital ‘L’ for type 1/2 legacy class settings)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Response:   | printf(":p%d class %d\\r\\n", port, class);                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|             | - or -                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|             | printf(":p%d class %d,%d\\r\\n",port,clsM,clsA);                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Example:    | sin 0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|             | p9 cl 3                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Response:   | :p9 class 3D\<CR\>\<LF\>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|             | This sets port 9 IEEE "class" to compliant class 3 on both pairs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Example:    | sin 0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|             | p1 cl 1L,2L                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Response:   | :p1 class 1L,2L\<CR\>\<LF\>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|             | This sets port 1 IEEE "class" to legacy class 1 on the main pair and legacy class 2 on the alt pair.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

CLASS – Autoclass
-----------------

| Description | Used to enable support for autoclass. Using two values separated with a comma allows the main and alt pairs to be set differently, or a single value will be applied to both pairs.                                                                                                                                                                                               |
|             |                                                                                                                                                                                                                                                                                                                                                                                   |
|             | Note that autoclass is an addition to the current number class setting, and when enabled, is indicated with an ‘A’ after the number class setting. The default setting is aoff for both pairs.                                                                                                                                                                                    |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|             |                                                                                                                                                                                                                                                                                                                                                                                   |
| Command:    | cl[ass] \<aon\|aoff\>                                                                                                                                                                                                                                                                                                                                                             |
|             |                                                                                                                                                                                                                                                                                                                                                                                   |
| Argument:   | “aon” for autoclass on, or “aoff” for autoclass off                                                                                                                                                                                                                                                                                                                               |
|             |                                                                                                                                                                                                                                                                                                                                                                                   |
| Response:   | printf(":p%d class %d%c\\r\\n",port,class,acls);                                                                                                                                                                                                                                                                                                                                  |
|             | - or -                                                                                                                                                                                                                                                                                                                                                                            |
|             | printf(":p%d class %d%c,%d%c\\r\\n", port,clsM,clsA,aclsM,aclsA);                                                                                                                                                                                                                                                                                                                 |
|             |                                                                                                                                                                                                                                                                                                                                                                                   |
| Example:    | p9 cl 3                                                                                                                                                                                                                                                                                                                                                                           |
|             | p9 cl aon                                                                                                                                                                                                                                                                                                                                                                         |
| Response:   | :p9 class 3A\<CR\>\<LF\>                                                                                                                                                                                                                                                                                                                                                          |
|             | This sets port 9 IEEE "class" to 3 on both pairs, with autoclass on.                                                                                                                                                                                                                                                                                                              |
| Example:    | p1 cl 1,2                                                                                                                                                                                                                                                                                                                                                                         |
|             | p1 cl aof                                                                                                                                                                                                                                                                                                                                                                         |
| Response:   | :p1 class 1,2\<CR\>\<LF\>                                                                                                                                                                                                                                                                                                                                                         |
|             | This sets port 1 IEEE "class" to 1 on the main pair and 2 on the alt pair, with autoclass off on both pairs.                                                                                                                                                                                                                                                                      |

CONNECT 
--------

>   Description Controls the relays that connect the power load circuitry to the
>   UUT port via the GbE transformer. From a power perspective, this is
>   equivalent to plugging in the RJ45 from the UUT. See the [Operational
>   Overview](#_Operational_Overview) section for more details. Connect must be
>   ‘on’ for the UUT to see an IEEE 802.3af/at/bt PoE load. The connect command
>   can also be used to select the main, alternate, or both power pairs. If a
>   comma is present, the command assumes the user is specifying the connect
>   status of each pair individually. The first value is the connect status of
>   the main pair and the second is the alternate pair (e.g. when “connect 0,1”
>   is entered, only the alternate pair will be connected to the load).

>   Command: conn[ect] \<on\|off\|0\|1\|0,0\|0,1\|1,0\|1,1\>

>   Response: printf(":p%d Connect %d\\n", port, state);  
>   - or -  
>   printf(":p%d Connect %d,%d\\r\\n",port,stM,stA);

>   state = 1 or 0 for on and off respectively.

DETECT
------

>   Description Sets the IEEE 802.3af/at/bt detect signature. Using two values
>   separated with a comma allows the main and alt pairs to be set differently,
>   or a single value will be applied to both pairs.  
>     
>   The default setting is ok for both pairs.

>   Command: det[ect] \<ok\|lo\|ok,ok\|ok,lo\|lo,ok\|ok,ok\>

Arguments: ok signature resistance 24.9K ohms  
lo signature resistance 13K ohms

>   Response: printf(":p%d det %s\\n", port, arg);  
>   - or -  
>   printf(":p%d det %d,%d\\r\\n",port,argM,argA);

EXT 
----

>   Description Controls the connection of the data path from one test port to
>   another. The data path is connected between adjacent ports: 1-2, 3-4, etc.
>   when the ext command is set on for both ports. This is necessary for the
>   ports to send data to each other. When ext is off, the data path is open.  
>     
>   The default state is on.

>   Command: ext[ernal] \<on\|off\>

Response: printf(":p%d Ext Ref %d\\n", port, state);

>   state = 1 or 0 for on and off respectively.

<br>GETI 
---------

>   Description Measures the load current being drawn from the UUT on the main
>   and alt pairs individually, and as a total for both pairs. Current readings
>   are in milliamps.

>   Command: geti

>   Response: printf(":p%d %dmA, %dmA, %dmA\\r\\n",port,val, val_alt,
>   val_total);

Example: p1 geti

Example response: :p1 501mA, 500mA, 1001mA\<CR\>\<LF\>

GETP 
-----

>   Description Measures the load power being drawn from the UUT on the main and
>   alt pairs individually, and as a total for both pairs. Power readings are in
>   watts.

>   Command: getp

>   Response: printf(":p%d %dW, %dW, %dW\\r\\n",port,val, val_alt, val_total);

Example: p1 getp

Example response: :p1 50W, 50W, 100W\<CR\>\<LF\>

GETV 
-----

>   Description Measures the voltages from the UUT (center taps of GbE
>   magnetics) of both pairs. Reports the voltage as either positive or negative
>   depending on the polarity of the pair. The “Cisco” standard 1,2 = negative,
>   3,6 = positive is reported as a positive voltage (main pair). Alt pairs with
>   4,5 = positive, and 7,8 = negative is reported as a positive voltage.

>   Command: getv

>   Response: printf(":p%d %.1fV, %.1fV\\r\\n",port,fvalM,fvalA);

>   The result will be between -60.0 and 60.0

Example: p1 getv

Example response: :p1 50.5V, 0.0V\<CR\>\<LF\>

<br>INR
-------

>   Description Sets the time period (in milliseconds) of the inrush timer. The
>   default time period is 85ms, and the maximum time period is 255ms. The same
>   inrush time period is set for both pairs. The inrush timer controls the
>   application of the full ‘set’ command current, with a minimum current of
>   about 100ma being allowed during the inrush period. The inrush timer starts
>   when the input voltage goes above UVLO (38v typical). See [Appendix
>   A.3](#_A.3_Inrush_Example) for an example waveform of the inrush current.

>   Command: inr[ush] \<value\>

>   Response: printf(":p%d inrush delay %d ms\\r\\n", port, val);

Example: p1 inr 100

Example response: :p1 inrush delay 100 ms\<CR\>\<LF\>

MPS
---

| Description       | Turns the minimum power signature feature in the PD controller on or off. Using two values separated with a comma allows the main and alt pairs to be set differently, or a single value will be applied to both pairs. When MPS is on, the power signature will be 18.5mA, and will have a 26% duty cycle for PSE types 1 and 2, and a 5.4% duty cycle for PSE types 3 and 4. The default state is off for both pairs. |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                   |                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Command:          | mps \<on\|off\|0,0\|0,1\|1,0\|1,1\>                                                                                                                                                                                                                                                                                                                                                                                     |
|                   |                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Response:         | printf(":p%d mps %d\\r\\n", port, val);                                                                                                                                                                                                                                                                                                                                                                                 |
|                   | - or -                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                   | printf(":p%d mps %d,%d\\r\\n",port,valM,valA);                                                                                                                                                                                                                                                                                                                                                                          |
| Example:          | p1 mps 1                                                                                                                                                                                                                                                                                                                                                                                                                |
| Example response: | :p1 mps 1\<CR\>\<LF\>                                                                                                                                                                                                                                                                                                                                                                                                   |

PSE 
----

>   Description Returns the state of the TPH, TPL and status bits from the TI
>   TP2372 PD controllers of both pairs. A “-“ indicates that the specified bit
>   is not set. These status bits are specific to the PD controller, and cam be
>   interpreted using the tables below (data from TI TP2372 spec).

>   Command: pse

>   Response: printf(":p%d MAIN: %s, %s, %s, ALT: %s, %s, %s\\r\\n", port, val);

Example: p1 pse

Example response: :p1 MAIN: TPH, - , - , ALT: TPH, - , - \<CR\>\<LF\>

Table 1 - TPH, TPL, BT and Allocated Power Truth Table

| PSE Type | PD Class | Number of Class Cycles | PSE Allocated Power at PD (W) | TPH  | TPL  |      |
|----------|----------|------------------------|-------------------------------|------|------|------|
| 1-2      | 0        | 1                      | 12.95                         | HIGH | HIGH | HIGH |
| 1-2      | 1        | 1                      | 3.84                          | HIGH | HIGH | HIGH |
| 1-2      | 2        | 1                      | 6.49                          | HIGH | HIGH | HIGH |
| 1-2      | 3        | 1                      | 12.95                         | HIGH | HIGH | HIGH |
| 2        | 4        | 2                      | 25.5                          | HIGH | LOW  | HIGH |
| 3-4      | 0        | 1                      | 12.95                         | HIGH | HIGH | LOW  |
| 3-4      | 1        | 1                      | 3.84                          | HIGH | HIGH | LOW  |
| 3-4      | 2        | 1                      | 6.49                          | HIGH | HIGH | LOW  |
| 3-4      | 3        | 1                      | 12.95                         | HIGH | HIGH | LOW  |
| 3-4      | 4        | 2-3                    | 25.5                          | HIGH | LOW  | LOW  |
| 3-4      | 5        | 4                      | 40                            | LOW  | HIGH | LOW  |
| 3-4      | 6        | 4                      | 51                            | LOW  | HIGH | LOW  |
| 4        | 7        | 5                      | 62                            | LOW  | LOW  | LOW  |
| 4        | 8        | 5                      | 71                            | LOW  | LOW  | LOW  |

Table 2 - Power Demotion Cases

| PSE Type | PD Class | Number of Class Cycles | PSE Allocated Power at PD (W) | TPH  | TPL  |     |
|----------|----------|------------------------|-------------------------------|------|------|-----|
| 3-4      | 4-8      | 1                      | 12.95                         | HIGH | HIGH | LOW |
| 3-4      | 5-8      | 2,3                    | 25.5                          | HIGH | LOW  | LOW |
| 3-4      | 7-8      | 4                      | 51                            | LOW  | HIGH | LOW |

POWER
-----

| Description       | Sets load control to ‘power’ mode, and sets load value in watts. If set above 100W (or 50W per pair) an error will occur. If a single value is used, it is divided in half, and each pair will draw half the specified amount. Using two values separated with a comma allows the main and alt pairs to be set differently. Single, odd, input values will be rounded down. |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                   |                                                                                                                                                                                                                                                                                                                                                                             |
| Command:          | pwr \<value\>                                                                                                                                                                                                                                                                                                                                                               |
|                   | - or -                                                                                                                                                                                                                                                                                                                                                                      |
|                   | pwr \<value main\>,\<value alt\>                                                                                                                                                                                                                                                                                                                                            |
|                   |                                                                                                                                                                                                                                                                                                                                                                             |
| Response:         | printf(":p%d pwr %d, %d (%d) W\\r\\n", port, mVal, aVal, totalW);                                                                                                                                                                                                                                                                                                           |
| Example:          | p1 pwr 100                                                                                                                                                                                                                                                                                                                                                                  |
| Example response: | :p1 50, 50 (100) W\<CR\>\<LF\>                                                                                                                                                                                                                                                                                                                                              |

RESET 
------

>   Description Resets port(s) to fully disconnected state.

>   Command: res[et]

>   Response: printf(":p%d reset\\n", port);

SET
---

>   Description Sets load control to ‘current’ mode, and sets load value in
>   milliamps. If set too low, the minimum value will be set; if above 2000mA
>   (or 1000mA per pair) an error will occur. If a single value is used, it is
>   divided in half, and each pair will draw half the specified amount. Using
>   two values separated with a comma allows the main and alt pairs to be set
>   differently.

>   Command: set \<value\>  
>   set \<value main\>,\<value alt\>

>   Response: printf(":p%d %d, %dmA\\r\\n",port,valM,valA);  
>   - or -  
>   printf(":p%d %d, %dmA (min)\\r\\n",port,valM,valA);

Example: p1 set 350, 450

Example response: :p1 350, 450 mA\<CR\>\<LF\>

Example: g2 set 350

>   Example response: :p9 350 mA\<CR\>\<LF\>  
>   ….  
>   :p16 350 mA\<CR\>\<LF\>

SHORT
-----

>   Description Controls a relay that can short the UUT power before the full
>   wave bridge. Using two values separated with a comma allows the main and alt
>   pairs to be set differently, or a single value will be applied to both
>   pairs. *WARNING - SHORTING AT FULL POWER CAN DAMAGE UUT.*  
>     
>   The default state is off for both pairs.

>   Command: short \<on\|off\|0,0\|0,1\|1,0\|1,1\>

>   Response: printf(":p%d short %d\\r\\n", port, val);

Example: p1 short 1

Example response: :p1 short 1\<CR\>\<LF\>

SHOW
----

| Description       | Shows the current (last-sent) state of a specific command. For the ‘set’ and ‘pwr’ values, will also indicate which control mode (set/current or pwr/power) is in effect for each port. |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                   |                                                                                                                                                                                         |
| Command:          | show \<cl\|det\|cap\|conn\|set\|pwr\|ext\|shor\|sin\|mps\|inr\>                                                                                                                         |
|                   |                                                                                                                                                                                         |
| Response:         | Depends on selected command, but is the same as the response of that command.                                                                                                           |
| Example:          | p1 sh cl                                                                                                                                                                                |
| Example response: | :p1 class 0,1\<CR\>\<LF\>                                                                                                                                                               |
| Example:          | p1 set 1000 p1 sh pwr                                                                                                                                                                   |
| Example response: | :p1 in SET control mode                                                                                                                                                                 |
| Example:          | p1 pwr 100 p1 sh set                                                                                                                                                                    |
| Example response: | :p1 in PWR control mode                                                                                                                                                                 |

SINGLE
------

>   Description Turns the single signature feature on or off. Setting the single
>   signature feature off reverts to the default dual signature mode.  
>     
>   The default state is off.

>   Command: sin[gle] \<on\|off\>

>   Response: printf(":p%d Single Signature\\r\\n");  
>   - or -  
>   printf(":p%d Dual Signature\\r\\n");

Example: p1 sin 1

Example response: :p1 Single Signature\<CR\>\<LF\>

Example: p1 sin 0

Example response: :p1 Dual Signature\<CR\>\<LF\>

STATUS 
-------

>   Description Returns the "Power Good" status of the IEEE load controllers.
>   The power status is active when the IEEE controller is receiving power above
>   the UVLO value (38v typical) and the load capacitor is charged. Also reports
>   if an over-temperature condition occurred that caused the port to be shut
>   down.

>   Command: st[atus]

>   Response: printf(":p%d PWR %d, %d\\n",port,state1,state2);

>   state = 1 or 0 for on and off respectively.

Example: p1 st

Example response: :p1 PWR 1, 1\<CR\>\<LF\>

TEMPERATURE
-----------

>   Description Reports the temperature of the drain pins of the MOSFET loads on
>   the main and alt pairs, as measured on the line card PCB.

>   Command: temp[erature]

>   Response: printf(":p%d %3d C, %3d C\\n", port, tempC, tempC);

Example: p2 temp

Example response: :p2 27 C, 29 C\<CR\>\<LF\>
