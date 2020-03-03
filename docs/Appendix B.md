Overview
--------

>   This Appendix gives an overview of basic test setups. No port or group
>   prefixes are shown. PSE, PD as defined in IEEE 802.3bt. The RT-PoE5 commands
>   are issued in the order shown.

B.2 Signature Detect
--------------------

| **RT-PoE commands:**           | **PSE check after commands issued**                     |
|--------------------------------|---------------------------------------------------------|
| reset                          | Verify that the PSE recognizes a valid PD.              |
| detect ok                      |                                                         |
| mps on                         |                                                         |
| connect on                     |                                                         |
| connect off                    | Verify that the PSE detects a low signature resistance. |
| detect lo                      |                                                         |
| connect on                     |                                                         |
| connect off                    | Verify that the PSE recognizes a valid PD.              |
| detect ok                      |                                                         |
| connect on                     |                                                         |
| connect off                    | Verify that the PSE detects a bad capacitance.          |
| cap on                         |                                                         |
| connect on                     |                                                         |

<br>B.3 Class Detect, dual signature mode
-----------------------------------------

| **RT-PoE commands:**                      | **PSE check after commands issued**                                                       |
|-------------------------------------------|-------------------------------------------------------------------------------------------|
| reset                                     | Verify that the PSE sees a legacy class 0 PD.                                             |
| detect ok                                 |                                                                                           |
| single off                                |                                                                                           |
| class 0                                   |                                                                                           |
| connect on                                |                                                                                           |
| connect off                               | Verify that the PSE sees a compliant class 1 PD.                                          |
| class 1                                   |                                                                                           |
| connect on                                |                                                                                           |
| connect off                               | Verify that the PSE sees a legacy class 1 PD.                                             |
| class 1L                                  |                                                                                           |
| connect on                                |                                                                                           |
| connect off                               | Verify that the PSE sees a compliant class 5 PD.                                          |
| class 5                                   |                                                                                           |
| connect on                                |                                                                                           |
| connect off                               | Verify that the PSE is able to detect autoclass capability, and support a load of xxx mA. |
| class aon                                 |                                                                                           |
| set xxx                                   |                                                                                           |
| connect on                                |                                                                                           |

<br>B.4 Class Detect, single signature mode
-------------------------------------------

| **RT-PoE commands:**                          | **PSE check after commands issued**                                                       |
|-----------------------------------------------|-------------------------------------------------------------------------------------------|
| reset                                         | Verify that the PSE sees a class 0 PD.                                                    |
| detect ok                                     |                                                                                           |
| single on                                     |                                                                                           |
| mps 1                                         |                                                                                           |
| class 0                                       |                                                                                           |
| connect on                                    |                                                                                           |
| connect off                                   | Verify that the PSE sees a class 1 PD.                                                    |
| class 1                                       |                                                                                           |
| connect on                                    |                                                                                           |
| connect off                                   | Verify that the PSE sees a class 2 PD.                                                    |
| class 2                                       |                                                                                           |
| connect on                                    |                                                                                           |
| connect off                                   | Verify that the PSE sees a class 3 PD.                                                    |
| class 3                                       |                                                                                           |
| connect on                                    |                                                                                           |
| connect off                                   | Verify that the PSE sees a class 4 PD.                                                    |
| class 4                                       |                                                                                           |
| connect on                                    |                                                                                           |
| connect off                                   | Verify that the PSE sees a class 5 PD.                                                    |
| class 5                                       |                                                                                           |
| connect on                                    |                                                                                           |
| connect off                                   | Verify that the PSE sees a class 6 PD.                                                    |
| class 6                                       |                                                                                           |
| connect on                                    |                                                                                           |
| connect off                                   | Verify that the PSE sees a class 7 PD.                                                    |
| class 7                                       |                                                                                           |
| connect on                                    |                                                                                           |
| connect off                                   | Verify that the PSE sees a class 8 PD.                                                    |
| class 8                                       |                                                                                           |
| connect on                                    |                                                                                           |
| connect off                                   | Verify that the PSE is able to detect autoclass capability, and support a load of yyy mA. |
| class aon                                     |                                                                                           |
| set yyy                                       |                                                                                           |
| connect on                                    |                                                                                           |

<br>B.5 Power Status and overload (IEEE 802.3af)
------------------------------------------------

| **RT-PoE commands:**                  | **PSE check after commands issued**                               |
|---------------------------------------|-------------------------------------------------------------------|
| reset                                 |                                                                   |
| detect ok                             |                                                                   |
| class 3                               |                                                                   |
| set 20                                |                                                                   |
| connect on                            |                                                                   |
|                                       | Enable power to port                                              |
|                                       | Verify that PSE sees the device taking power.                     |
| status                                | Verify that power is on.                                          |
| getv                                  | Verify that voltages are as expected.                             |
| set 350                               | Verify that PSE is providing full power.                          |
| set 390                               | Verify that PSE sees overload and shuts off power.                |
| status                                | Verify that power is off.                                         |

B.6 Power Status and overload (IEEE 802.3at)
--------------------------------------------

Same as above, but use “class 4”, and “set 600” for full power and “set 660” for
overload.

<br>B.7 Power Status and overload (IEEE 802.3bt, single signature) 
-------------------------------------------------------------------

| **RT-PoE commands:**                           | **PSE check after commands issued**                                  |
|------------------------------------------------|----------------------------------------------------------------------|
| reset                                          |                                                                      |
| detect ok                                      |                                                                      |
| single on                                      |                                                                      |
| class 8                                        |                                                                      |
| set 20                                         |                                                                      |
| connect on                                     |                                                                      |
|                                                | Enable power to port                                                 |
|                                                | Verify that PSE sees the device is taking power.                     |
| status                                         | Verify that power is on.                                             |
| getv                                           | Verify that voltages are as expected.                                |
| set 1426                                       | Verify that PSE is providing full power.                             |
| set 2000                                       | Verify that PSE sees overload and shuts off power.                   |
| status                                         | Verify that power is off.                                            |

B.8 Power Status and overload (IEEE 802.3bt, dual signature) 
-------------------------------------------------------------

| **RT-PoE commands:**                            | **PSE check after commands issued**                                  |
|-------------------------------------------------|----------------------------------------------------------------------|
| reset                                           |                                                                      |
| detect ok                                       |                                                                      |
| single off                                      |                                                                      |
| class 5                                         |                                                                      |
| set 20                                          |                                                                      |
| connect on                                      |                                                                      |
|                                                 | Enable power to port                                                 |
|                                                 | Verify that PSE sees the device is taking power.                     |
| status                                          | Verify that power is on.                                             |
| getv                                            | Verify that voltages are as expected.                                |
| set 1426                                        | Verify that PSE is providing full power.                             |
| set 2000                                        | Verify that PSE sees overload and shuts off power.                   |
| status                                          | Verify that power is off.                                            |

B.9 Data transmission under power
---------------------------------

| **RT-PoE commands:**                  | **PSE check after commands issued**                                                |
|---------------------------------------|------------------------------------------------------------------------------------|
| (as above for specific test required) |                                                                                    |
|                                       | Enable power to port.                                                              |
|                                       | Verify that PSE sees that device powers up.                                        |
| status                                | Verify that power is on.                                                           |
| ext on                                | Run traffic test between port pairs 1 and 2, 3 and 4,…23 and 24. Verify no errors. |
