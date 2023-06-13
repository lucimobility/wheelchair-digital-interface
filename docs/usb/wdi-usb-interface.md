# USB Wheelchair Digital Interface
## Background
The WDI relies on the existing [USB HID Specifications](https://www.usb.org/hid) and the corresponding [Linux input event interface (evdev)](https://docs.kernel.org/input/input.html#evdev) to translate user input into actions on the wheelchair. Creating a device that meets the USB HID spec will not be covered here, but some example HID descriptors can be seen [here](example-report-descriptors/). This page will only specify what USB HID usages and events can be used to control the wheelchair.

 In the WDI, the two main HID usages are gamepad for proportional control and keyboard for digital control. Relative devices such as mice are not supported.

 ## Behavior
 The WDI is event based, which means it maintains the latest input event until a new one is received. For example, if a a joystick report indicates that the chair should drive forward, it will continue to drive forward until a new joystick report indicates otherwise.

 Button presses and releases are separate events, and the WDI acts upon a button press for non-driving actions. This means that the duration of the press does not matter. Any driving done through a digital button press will stop when the button is released. Multiple buttons can be pressed simultaneously.

 ### Active Control
 Only one device is allowed to control movement on the chair at a time. A device takes or gives up control by sending a specific button press (listed as "Enable device control" below). A device that is not in control may still affect other aspects of the chair such as modifying speed setting, profile, and controlling the lights.


## Button Mapping
This section defines what input events lead to what output on the chair.
### Note on Gamepad Usage Button Mapping
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

If the usage extends past the typical 15 gamepad buttons, then the buttons start getting mapped to `BTN_TRIGGER_HAPPYX`.These typically are not present on off-the-shelf gamepad devices.

### Implementation-dependant Buttons
Since what needs to be controlled varies depending on the WDI [implementation](../implementations/), the following standard buttons and axes are reserved to be specific to the implementation:

**Gamepad:**
* BTN_EAST
* BTN_C
* BTN_WEST
* BTN_NORTH
* BTN_Z
* BTN_TR2
* BTN_TL2
* BTN_MODE
* BTN_THUMBL
* BTN_THUMBR
* ABS_Z
* ABS_RX
* ABS_RY
* ABS_RZ

**Keyboard** - any key not listed below can be used


### Drive Actions
| Action | Keyboard Controls | Gamepad Controls |
|--------|------|-----|
| Drive forward | 'w' \| up arrow | Y axis (towards min val) |
| Drive backward | 's' \| down arrow | Y axis (towards max val) |
| Drive left | 'a' \| left arrow | X axis (towards min val) |
| Drive right | 'd' \| right arrow | X axis (towards max val) |
| Emergency stop | backspace | BTN_SOUTH |
| Enable device control | enter | BTN_START |



### Chair Control Actions
User menu control matches drive controls.
| Action | Keyboard Controls | Gamepad Controls |
|--------|------|-----|
| Power/Sleep toggle | escape | BTN_SELECT to wake up (slept through user menu) |
| Open/close user menu | 'o' | BTN_SELECT |
| Adjust maximum speed | 1/2/3/4/5 for direct jump, '-'/'=' for decrement/increment | d-pad left/right(ABS_HAT0X = -1/1) or TL/TR for decrement/increment |
| Change profile | F1-F8 for direct, '.' for incrementing | d-pad up (ABS_HAT0Y = -1) for increment |
| Switch mode | tab | d-pad down (ABS_HAT0Y = 1) |
| Headlight toggle | 'l' | user menu only |
| Hazard lights | 'h' | user menu only |
| Left blinker | 'b' | user menu only |
| Right blinker | 'n' | user menu only |
| Horn | spacebar (while pressed) | BTN_THUMBR (while pressed) |

### Seating
Seating can be controlled using the drive controls when in seating adjust mode. Alternatively, the following actions are mapped to specific inputs. For now, the gamepad mapping uses buttons outside the range of typical usage, but a mapping such that off-the-shelf gamepads are usable will be created too.

| Action | Keyboard Controls | Gamepad Controls |
|--------|------|-----|
| Memory seating 1 forward | SHIFT + 1 | BTN_TRIGGER_HAPPY1 |
| Memory seating 1 backward | CTRL + 1 | BTN_TRIGGER_HAPPY2 |
| Memory seating 2 forward | SHIFT + 2 | BTN_TRIGGER_HAPPY3 |
| Memory seating 2 backward | CTRL + 2 | BTN_TRIGGER_HAPPY4 |
| Memory seating 3 forward | SHIFT + 3 | BTN_TRIGGER_HAPPY5 |
| Memory seating 3 backward | CTRL + 3 | BTN_TRIGGER_HAPPY6 |
| Tilt forward | SHIFT + numpad 0 | BTN_TRIGGER_HAPP7 |
| Tilt backward | CTRL + numpad 0 | BTN_TRIGGER_HAPPY8 |
| Recline forward | SHIFT + numpad 1 | BTN_TRIGGER_HAPPY9 |
| Recline backward | CTRL + numpad 1 | BTN_TRIGGER_HAPPY10 |
| Legs up | SHIFT + numpad 2 | BTN_TRIGGER_HAPPY11 |
| Legs down | CTRL + numpad 2 | BTN_TRIGGER_HAPPY12 |
| Elevate up | SHIFT + numpad 3 | BTN_TRIGGER_HAPPY13 |
| Elevate down | CTRL + numpad 3 | BTN_TRIGGER_HAPPY14 |
| Footplates up | SHIFT + numpad 4 | BTN_TRIGGER_HAPPY15 |
| Footplates down | CTRL + numpad 4 | BTN_TRIGGER_HAPPY16 |
