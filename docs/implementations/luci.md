# LUCI Implementation
LUCI implements the WDI for USB and will be compatible with Bluetooth in the future. Not all WDI functions are currently supported by LUCI.

## General Notes
* LUCI collision avoidance and dropoff protection is still active when the chair is controlled via the WDI.
* LUCI plays a sound when a device becomes the active controller and a different sound when the device is deactivated.
* Unplugging any device deactivates any active device and returns control to the normal wheelchair electronics.

## Button Mapping
| Action | Keyboard | Gamepad |
|-----|---|---|
| Override | caps lock | BTN_EAST |
| Reset changes | Home | None |
| Profile decrement | matches main spec | ABS_HAT0Y = 1 (temporarily implemented until mode switching is implemented) |
| Power/Sleep toggle | None (Escape temporarily mapped to emergency stop until power controls implemented) | None |
| Switch mode | None (Tab temporarily mapped to emergency stop until mode controls implemented) | None |

## Limitations and Known Issues
### General
1. LUCI turns off when the wheelchair does, so an input device cannot be used to turn the chair on through LUCI. This also means devices powered through the USB connection to LUCI are off when LUCI is off.
1. Seating position cannot be moved using the drive commands on the input device through LUCI (on most existing chairs).
1. The mapping of HID commands to seating axis is not consistent across chair manufacturers. It should match on Permobil chairs. On other chairs, all axes should be accessible through the same WDI commands, but may not line up with the mapping exactly. Additionally, numpad 5-9 are also mapped to potential seating axes seen on other chair models and can be used the same way (SHIFT up, CTRL down).
1. User menu cannot be navigated using the input device through LUCI.
1. Speed setting adjustments made by LUCI are not remembered by the wheelchair electronics. This means that the previously set speed setting will come back if the profile is changed or the the chair is rebooted, and that any changes made to speed setting through the normal joystick interface will change based on what the speed setting was before LUCI changed it (e.g. speed 5 -> LUCI changes to speed 1 -> speed setting decrease through JSM leads to speed 4).
1. LUCI does not know how many profiles are enabled on the chair and currently assumes there are 4. On chairs with fewer than 4, incrementing to a disabled profile is a no-op on the chair, and incrementing continues to be no-ops until wrapping back around to profile 1. On chairs with more than 4 enabled profiles, there is no way to access the additional profiles via the WDI currently.

### Chairs with Tracking (ESP)
This includes most Permobil chairs made between 2020-2024 (before Power Platform). These issues occur only when the chair is being controlled via the WDI.
1. Programmed RNET settings do not affect drive behavior.
1. Speed settings 4 and 5 do not affect drive behavior and are functionally equivalent to speed 3.
1. Profile does not affect drive behavior.
1. Chair may drive differently through the WDI than with the standard joystick due to tracking interaction with the WDI.

### Xbox Controllers
Notes on interfacing with Xbox controllers specifically (including Xbox Adaptive Controller)
1. Xbox controllers plugged into the LUCILink Hub before the chair/LUCI is turned on will **not** turn on and connect automatically. The controller has to be plugged in after LUCI is powered. This is not an issue if the device is plugged directly into one of the MPU USB ports.