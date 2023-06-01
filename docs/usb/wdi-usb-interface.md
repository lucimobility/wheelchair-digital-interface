# USB Wheelchair Digital Interface
## Background
The WDI relies on the existing [USB HID Specifications](https://www.usb.org/hid) and the corresponding [Linux input event interface (evdev)](https://docs.kernel.org/input/input.html#evdev) to translate user input into actions on the wheelchair. Creating a device that meets the USB HID spec will not be covered here, but some example HID descriptors can be seen [here](example-report-descriptors/). This page will only specify what USB HID usages and events can be used to control the wheelchair.

 In the WDI, the two main HID usages are gamepad for proportional control and keyboard for digital control. Relative devices such as mice are not supported.


## Note on Gamepad Usage Button Mapping
When the HID is defined as a gamepad, the button usages get mapped to particular events by the linux kernel. A gamepad HID with the following usage would be able to trigger all of the subsequent button press events.

```
0x05, 0x09,        //   Usage Page (Button)
0x19, 0x01,        //   Usage Minimum (0x01)
0x29, 0x0f,        //   Usage Maximum (0x0f)
```

https://gitlab.freedesktop.org/libevdev/libevdev/-/blob/master/include/linux/linux/input-event-codes.h#L380
```
 BTN_GAMEPAD / 	BTN_SOUTH / BTN_A
 BTN_EAST / BTN_B
 BTN_C
 BTN_NORTH / BTN_X
 BTN_WEST / BTN_Y
 BTN_Z
 BTN_TL
 BTN_TR
 BTN_TL2
 BTN_TR2
 BTN_SELECT
 BTN_START
 BTN_MODE
 BTN_THUMBL
 BTN_THUMBR
```

## Drive actions
| Action | Keyboard Controls | Gamepad Controls |
|--------|------|-----|
| Drive forward | 'w' \| up arrow | Y axis (towards min val) |
| Drive backward | 's' \| down arrow | Y axis (towards max val) |
| Drive left | 'a' \| left arrow | X axis (towards min val) |
| Drive right | 'd' \| right arrow | X axis (towards max val) |
| Emergency stop | backspace | button_east?? would like this to be something that is easy to press under stress |
| Enable drive | enter | start button |
| 