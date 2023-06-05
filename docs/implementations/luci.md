# LUCI Implementation
LUCI implements the WDI for USB and will be compatible with Bluetooth in the future. Not all WDI functions are currently supported by LUCI.

## Limitations and Known Issues
### General
1. LUCI turns off when the wheelchair does, so an input device cannot be used to turn the chair on through LUCI. This also means devices powered through the USB connection to LUCI are off when LUCI is off.
1. Seating position cannot be moved using the input device through LUCI.
1. User menu cannot be navigated using the input device through LUCI.
1. Speed setting adjustments made by LUCI are not remembered by the wheelchair electronics. This means that the previously set speed setting will come back if the profile is changed or the the chair is rebooted, and that any changes made to speed setting through the normal joystick interface will change based on what the speed setting was before LUCI changed it (e.g. speed 5 -> LUCI changes to speed 1 -> speed setting decrease through JSM leads to speed 4).
1. LUCI sound feedback sometimes breaks or sounds weird when using the WDI.

### Chairs with Tracking (ESP)
This includes most modern Permobil chairs.
1. Speed setting does not affect maximum speed.
1. Profile does not affect drive behavior.

### Xbox Controllers
Notes on interfacing with Xbox controllers specifically (including Xbox Adaptive Controller)
1. Xbox controllers plugged in before the chair/LUCI is turned on will **not** turn on and connect automatically. The controller has to be plugged in after LUCI is powered. This is a known bug and believed to be an issue with the underlying Linux driver (xpad).