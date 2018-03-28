![Logo](admin/onkyo.png)
# ioBroker.onkyo-vis

[![NPM version](http://img.shields.io/npm/v/iobroker.onkyo-vis.svg)](https://www.npmjs.com/package/iobroker.onkyo-vis)
[![Downloads](https://img.shields.io/npm/dm/iobroker.onkyo-vis.svg)](https://www.npmjs.com/package/iobroker.onkyo-vis)
[![Travis-CI](https://travis-ci.org/Eisbaeeer/ioBroker.onkyo-vis.svg?branch=master)](https://www.travis-ci.org/Eisbaeeer/ioBroker.onkyo-vis)   
[![NPM](https://nodei.co/npm/iobroker.onkyo-vis.png?downloads=true)](https://nodei.co/npm/iobroker.onkyo-vis/)


This adapter allows control of Onkyo AVRs using the EISCP protocol.

It uses node-eiscp: https://github.com/tillbaks/node-eiscp

The node-eiscp module parses raw EISCP messages into high-level
structured names like "master-volume", and the states will have those
high level names, e.g. "onkyo.0.master-volume"

For sending commands, there is a special state "command". Writes to that state
trigger either an high-level EISCP command as described in the "Command syntax" section
of https://github.com/tillbaks/node-eiscp like

    system-power=on
    zone2.power=on
    main.balance=3

or a raw EISCP command in the form of "PWR01".

## VIS compatibility
If you activate the checkbox "use fix variables" you will be able to use this variables in VIS with buttons and/or widgets.
The adapter will convert the given values in Onkyo readable values and sends it directly to the receiver and vice versa.
In this way you can set the value of e.g. volume with a slider or input box. If you control your receiver via IR you will get this reply also on this object.
As an second example, you can use a boolean switch button to control the power-button of the receiver.

|OBJECT WHO CAN USED IN VIS   |ISCP  |Input value         |Example  |Description                           |
|-----------------------------|:----:|:------------------:|:-------:|-------------------------------------:|
|Volume_Zone1                 |MVL   |1-99 decimal        |20       |"Master volume (Zone 1)"              |                
|Volume_Zone2    	            |ZVL   |1-00 decimal        |22       |"Volume zone2 (Zone 2)"               |
|Audio_Mute_Zone1             |AMT   |true/false or 00/01 |00       |"Mute Zone1"                          |
|Audio_Mute_Zone2             |ZMT   |true/false or 00/01 |01       |"Mute Zone2"                          |
|Input_Select_Zone1           |SLI   |00-FF hex           |2B       |"See excel list EISCP for hex values" |
|Input_Select_Zone2           |SLZ   |00-FF hex           |2F       |"See excel list EISCP for hex values" |
|Internet_Radio_Preset_Zone1  |NPR   |1-40 decimal        |12       |"Internet radio preset number Zone 1" |
|Internet_Radio_Preset_Zone2  |NPZ   |1-40 decimal        |10       |"Internet radio preset number Zone 2" |
|Tuner_Preset_Zone1           |PRS   |1-30 decimal        |08       |"Tuner preset number Zone 1"          |
|Tuner_Preset_Zone2           |PRZ   |1-30 decimal        |11       |"Tuner preset number Zone 2"          |
|Power_Zone1                  |PWR   |true/false or 00/01 |00 or 0  |"Power Zone 1"                        |
|Power_Zone2                  |ZPW   |true/false or 00/01 |01 or 1  |"Power Zone 2"                        |

Another special state maintained by the adapter is "connected". It's a boolean
showing whether node-eiscp is currently connected to a receiver.

Example of VIS view
![VIS](admin/onkyo-vis.png)     

To DO:
- Auto-discovery like SONOS
- Using eiscp.get_commands

## THIS IS A SPLIT BRANCH OF ONKYO

## ChangeLog
### 1.0.2 (2018.02.28)
* (Eisbaeeer) Changed name of adapter
* (Eisbaeeer) Added testing of adapter in travis

### 1.0.0 (2017.11.28)
* (Eisbaeeer) Add max volume settings to zone1 and zone2.   
* (Eisbaeeer) changed objects to switch
* (Eisbaeeer) moved adapter to "multimedia"
* (Eisbaeeer) cleaned log outputs

### 0.1.20 (2016.03.29)
* (Eisbaeeer) Add checkbox in settings for VIS objects. Volumes can be set in
  decimal. Power states, mute states, etc. are now usable with VIS buttons.

### 0.1.12 (2016.02.25)
* (installator) Fix power state

### 0.1.11 (2016.01.13)
* (installator) Fix regexp error

### 0.1.10
* (installator) For command CTL sets Center Level -12 - 0 - +12

### 0.1.9
* (installator) change power to system-power

### 0.1.8
* (installator) fix values to control power and enable using of 1 and 0

### 0.1.7
* (bluefox) fix creation of specific states (twice)

### 0.1.6
* (bluefox) fix creation of specific states

### 0.1.5
* (bluefox) fix node-eiscp package

### 0.1.4
* (bluefox) add debug outputs

### 0.1.1
* (bluefox) replace git with tarball

### 0.1.0
* (bluefox) update adapter for new concept

### 0.0.4
* (owagner) use verify_commands=false, to be able to send high-level commands to unknown AVR models

### 0.0.3
* (owagner) allow setting of states other than "command". This will trigger a high level
  command with the state name being set to the new value. Note that this will fail for
  many newer models, as they are not yet properly represented in node-eiscp's
  command table. Use the raw command in that case
* send some initial queries upon connect to get basic state information from the AVR

### 0.0.2
* (owagner) support node-eiscp's Autodiscovery mechanism
* (owagner) updated README, notably removing bogus reference to single instancing

### 0.0.1
* (owagner) initial version

