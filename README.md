# Wheelchair Digital Interface (WDI)
The Wheelchair Digital Interface (WDI) API detailed in this project is a modern, two-way communication standard for power wheelchairs built on widely accepted HID prototocols.

## Purpose
The purpose of the open WDI standard is: 
1. to allow faster development of new accessible wheelchair alternative controls by removing the need for 9-pin printer cable adapter circuits currently required to adapt to today's proprietary TRACE/DB-9 alternative drive inputs, 
2. to make current, commercially available adaptive gaming and computer interfaces available to power wheelchair users, and, 
3. to allow two-direction commumication between the power wheelchair and the controller. 

## Background
The WDI was initially conceived and developed as part of the National Science Foundation (NSF) Convergence Accelerator Track H project "Mobility Independence through Accelerated Wheelchair Intelligence" (NSF SP0076554) with input from a wide range of stakeholders. 

## Stakeholders
These stakeholders do not cover every use case, but they cover the major use cases that the WDI seeks to address.
### 1. User with Rapidly Degenerative Condition
* Users are often reliant on clinicians/care team to inform, acquire, and setup equipment. Options are hard to find because specialized field (very limited off-the-shelf options), often have to go through insurance, and are unique to setup on the power wheelchair.
* Physical abilities change rapidly, so best drive method also changes rapidly.
* Cannot get new drive methods quickly enough to keep up with changing condition, so often times users skip to end use case (eye drive). This leads to situations where the **drive method is not chosen based on the users current ability**

### 2. Tech savvy user
* Uses computer, smartphone, plays video games, tinkers with technology
* Very comfortable with current drive method.
* Wants to tinker with using other things to drive the chair, like phone or game controller, so they can get the best setup for themselves
* Would like to use chair control device to control other technology.
* Wants ability to play with configuration/button mapping to best fit their needs.

### 3. Accessible Technology Maker
* Makes a device for controlling computers in an alternative way.
* Wants to adapt device to drive chair to increase addressable market without designing additional hardware.
* Does not want to learn about proprietary wheelchair electronics

### 4. Clinician/ATP
* Wants to be able to quickly and easily test multiple drive options to find what best fits users needs
* Wants to spend less time writing/justifying devices to insurance/funding sources.

### 5. Researcher
* Wants to be able to rapidly iterate/prototype devices.
* Wants data to come back from the chair to do ???

## Requirements
* WDI shall allow for devices to control all aspects of a power wheelchair that the user can currently control.
* WDI shall interface with off-the-shelf control devices. (Separate into what types of specific devices?)
* WDI shall allow for bi-directional communication.
* WDI shall allow for devices to self-report their capabilities and bounds (e.g. joystick ranges)
* 


## What is controlled on a wheelchair
\* = May optionally be adjusted/actuated within a menu that is controlled via normal driving directional commands.

| Action | Notes |
| -------------|---------|
| Power/sleep toggle* | Distinct but functionally equivalent |
| Move forward | Proportional or Digital |
| Move backward | Proportional or Digital |
| Turn Left | Proportional or Digital |
| Turn Right | Proportional or Digital |
| Adjust Maximum speed* | Up/down |
| Change Profile* | Includes switching to attendant control |
| Switch Mode* | Mainly between drive/seating control |
| Seating controls | matches movement controls, left/right select actuator, up/down moves actuator |
| Open user menu | Usually a digital switch, can be input sequence |
| Navigate user menu | matches movement controls |
| Headlight toggle* | |
| Hazard lights toggle* | |
| Left/Right blinker toggles* | |
| Horn | |

Possible LUCI actions:
* Override
* Silence sounds
* Launch setup tool
* Capture and upload troubleshooting data


Future Actions:
* ???


## WDI Overview
The WDI builds upon existing specifications for using [Human Interface Devices (HID)](https://en.wikipedia.org/wiki/Human_interface_device).


### USB
coming soon... /docs/usb/wdi-usb-interface.md

### Bluetooth
coming soon... /docs/ble/wdi-ble-interface.md

## License
The WDI is open for use under an Apache 2.0 License.

## Versioning
**THE WDI IS CURRENTLY UNDER ACTIVE DEVELOPMENT AND PRE-RELEASE.**

Versioning is handled on a major.minor.patch method, until the official WDI is released all developers will be using a version < 1.0.0. All official releases will be tagged. 

## List of Current Support
The companies and organizations listed support the open, inclusive future provided by the WDI.

| Organization | Description |
| -------------|---------|
| Argallab at Northwestern University | Founding Member |
| Team Gleason | Founding Member |
| LUCI | Founding Member, LUCI units with LuciCore X.X and newer software are compatible with USB and BLE WDI controllers. | 
