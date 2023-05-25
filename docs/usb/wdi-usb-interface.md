# USB Wheelchair Digital Interface
## Background
The WDI relies on the existing [USB HID Specifications](https://www.usb.org/hid) and the corresponding [Linux input event interface (evdev)](https://docs.kernel.org/input/input.html#evdev) to translate user input into actions on the wheelchair. Creating a device that meets the USB HID spec will not be covered here, but some example HID descriptors can be seen here (TODO: Example keyboard and joystick descriptors). This page will only specify what USB HID usages and events can be used to control the wheelchair.

The most important aspect of controlling a power wheelchair is driving. This is accomplished either through the use of a proportional/analog device like a joystick or a digital device such as a switch array. In the WDI, these are controlled by either defining the device as a Gamepad/Joystick for proportional control, or as a keyboard for digital control.

In general, want this to make off-the-shelf generic HIDs usable.

Recommend Gamepad + Joystick usages for buttons if using proportional (allow d-pad for digital too?)\
^ Joystick usage recommended if wanting the device to integrate with XAC?? \
Touchpad or other digitizer for other proportional? Multitouch actions? Maybe a future feature...

Recommend keyboard for digital drive.

Where do relative devices like mice fit in?