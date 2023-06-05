# Wheelchair Digital Interface
The Wheelchair Digital Interface (WDI) API detailed in this project is a modern, two-way communication standard for power wheelchairs built on widely accepted HID prototocols.

## Purpose
The purpose of the open WDI standard is: 
1. to allow faster development of new accessible wheelchair alternative controls by removing the need for 9-pin printer cable adapter circuits currently required to adapt to today's proprietary TRACE/DB-9 alternative drive inputs, 
2. to make current, commercially available adaptive gaming and computer interfaces available to power wheelchair users, and, 
3. to allow two-direction commumication between the power wheelchair and the controller. 

## Background
The WDI was initially conceived and developed as part of the National Science Foundation (NSF) Convergence Accelerator Track H project "Mobility Independence through Accelerated Wheelchair Intelligence" (NSF SP0076554) with input from a wide range of stakeholders. 

WDI is intended to fill a gap in current power wheelchair standards. RESNA WC-2 and ISO 7176 do not define or provide guidance on power wheelchair interfaces for third party input devices, and previous attempts to provide a standard for power wheelchair interfaces and accessories (such as the M3S standard) have failed due to lack of industry adoption.

Prior to the WDI, the state-of-the-art in power wheelchair controls was to communicate with the wheelchair through a proprietary third-party interface module using a 9-pin D-Sub (DB9) connector. This interface was commonly referred to as "TRACE", was an input only/one-way interface, and was defined slightly differently by each wheelchair electronics manufacturer. See manufacturer technical documents for more details. TRACE is not a published or maintained industry standard.

## Stakeholders
These stakeholders do not cover every use case, but they cover the major use cases that the WDI seeks to address.
### 1. Users with Progressive or Changing Conditions
* Users are often reliant on clinicians/care team to inform, acquire, and setup equipment. Holistic options are hard to find because of the specialized needs (very limited off-the-shelf options), challenging insurance reimbursement, and solutions are unique to set up on a power wheelchair. Users without reimbursement challenges still need customizable options with a setup process they or a care team member can accomplish.
* Physical capabilities change rapidly, and therefore, so does the functional drive method.
* Users cannot get new drive methods quickly enough to keep up with changing conditions, so often times users skip to the end use case (eye drive). This leads to situations where the drive method is not chosen based on the user's current ability The reimbursement model is challenging and time-consuming in such a way that by the time a funded solution arrives and is setup, the user's condition may have progressed and that is no longer an applicable solution.

### 2. Tech Savvy User
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
* Wants data to come back from the chair for feedback to the user (e.g. lights, sounds, haptics)


## Requirements
* WDI shall allow for devices to control all aspects of a power wheelchair that the user can currently control.
* WDI shall interface with off-the-shelf control devices. (Separate into what types of specific devices?)
* WDI shall allow for bi-directional communication with the input device for use with feedback such as haptics, lights, or sounds.
* WDI shall allow for devices to self-report their capabilities and bounds (e.g. joystick ranges)
* WDI shall allow for multiple complimentary devices to be used simultaneously.
* WDI shall require a specific input before allowing a device to control the wheelchair.
* WDI shall stop the chair and return control to the native wheelchair control device upon losing connection to an input.


## What is controlled on a wheelchair
\* = May optionally be adjusted/actuated within a menu that is controlled via normal driving directional commands.

| Action | Notes |
| -------------|---------|
| Power/sleep toggle* | Distinct but functionally equivalent |
| Move forward | Proportional or digital |
| Move backward | Proportional or digital |
| Turn left | Proportional or digital |
| Turn right | Proportional or digital |
| Adjust maximum speed* | Up/down |
| Change profile* | Includes switching to attendant control |
| Switch mode* | Mainly between drive/seating control |
| Emergency stop | Typically used with latch drive mode |
| Seating controls | Matches movement controls, left/right select actuator, up/down moves actuator |
| Open user menu | Usually a digital switch, can be input sequence |
| Navigate user menu | Matches movement controls |
| Headlight toggle* | |
| Hazard lights toggle* | |
| Left/right blinker toggles* | |
| Horn* | |

Future Needs:
* Override a system behavior
* Silence sounds
* Launch setup tool
* Engage/disengage one or more automated features
* Enable/disable airplane mode/communications

## WDI Overview
The WDI builds upon existing specifications for using [Human Interface Devices (HID)](https://en.wikipedia.org/wiki/Human_interface_device).


### USB
Work in progress started [here](/docs/usb/wdi-usb-interface.md)

### Bluetooth
coming soon... /docs/ble/wdi-ble-interface.md

### Other Physical Interfaces
HID is also supported on the following interfaces:
* I2C
* CAN

### Suggested Other Devices
These are non-generic devices (may require a driver or may work differently with a driver) that the WDI is specifically designed to work with:

| Controller | Notes |
|------|-----|
| Xbox | Requires driver (xpad) |
| Playstation 5 (DualSense) | Can work generically, but has right stick axes and buttons mapped differently with driver. Motion and touchpad capabilities require driver |

## Implementations
Known implementations of the WDI and any specific information about those implementations can be found [here](docs/implementations/)

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
| [LUCI](https://www.luci.com) | Founding Member, LUCI units with LuciCore 2.0 and newer software are compatible with USB WDI controllers. |
