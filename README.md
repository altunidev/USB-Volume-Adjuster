# USB-Volume-Adjuster

The idea behind this device is to have an in-line hardware adapter that injects keystrokes to raise or lower volume alongside using media controls (i.e. pause/play, skip track, previous track). Another (side) goal is to have active communication controls for calling and voice chatting. This device is built to emulate the inline media controls of the likes of the Apple Earpods (microphone module) and many other earbuds similar to this. It is different in that it simply adds the controls to a USB-C port while allowing passthrough of any other USB 2.0 signals.

## Project Goals

- Functionality
  - Add media controls as a USB-C passthrough device
    - volume up / down
    - play / pause
    - next track / previous track
  - Potentially add communication controls
    - accept call / decline call
    - mute / unmute
      - may be more difficult based on calling software
      - may need to investigate driver-based muting/unmuting functionality depending on complexity
    - hang up
- Usability goals
  - Ergonomics
    - tiny, very smol
    - lightweight, portable
  - Electronics
    - minimalist
      - in hardware complexity
      - software complexity
      - power draw
      - packet sending
    - practically lossless data passthrough

### End goal:

I'm designing this device to work as a drop-in passthrough volume control device that simply sends volume change requests through a USB "keyboard" to the operating system. This device is designed first for the Bigscreen Beyond headset such that it works with any USB-C audio solution such as the Beyond Audio Strap, FiiO KA1 DAC (and subsequently, any 3.5mm audio device connected to the other end), Apple USB-C -> 3.5mm DAC (or third party variants, etc.), or even wireless solutions (as this will be interfacing with the operating system volume controls). While this is originally intended for the Bigscreen Beyond, I don't see why it shouldn't work on other devices either (i.e. phones, tablets, etc.), since it will use standardized keyboard inputs.

Very basic (not technical in any way) layout:
<img width="977" alt="Screenshot 2024-02-09 at 12 36 12" src="https://github.com/altunidev/USB-Volume-Adjuster/assets/66493425/ebc5b4ef-8a19-49ae-951d-2891289d2c83">

## Side goals:

- allow for additional user-configurable buttons
  - perhaps through QMK? or VIA?
  - while using the Bigscreen Beyond, can be useful in various cases where controllers are not necessary -- such as Flight or Driving Simulators

---

## Starting points

### useful
- Mechanical keyboard firmware
  - [QMK](https://qmk.fm/) -- already has groundwork for basically every keystroke anyone would need and more
    - [MCU documentation](https://docs.qmk.fm/#/platformdev_selecting_arm_mcu)
    - [KB2040 keyboard guide](https://learn.adafruit.com/using-qmk-on-rp2040-microcontrollers/adafruit-kb2040-on-the-pb-gherkin-30-keyboard)
      - [RP2040 QMK specific docs](https://docs.qmk.fm/#/platformdev_rp2040)
  - [XInput](https://github.com/dmadison/ArduinoXInput_AVR)
    - SteamVR tends to only recognize XInput instead of keyboard input. This might be useful for a SteamVR button of some kind
    - Reported behaviour: SteamVR only recognizes this form of input when a controller is powered on.
      - Would it be possible to emulate a SteamVR controller with a driver of some sort? This way, bypassing the need to power on a SteamVR controller of any kind.
    - https://github.com/terminal29/Simple-OpenVR-Driver-Tutorial/blob/master/driver_files/src/Driver/ControllerDevice.hpp
    - https://www.instructables.com/Arduino-LeonardoMicro-as-Game-ControllerJoystick/
- USB Hubs
  - [A source of FE1.1s component](https://www.lcsc.com/product-detail/USB_FE1-1S_C9359.html)
    - [FE1.1s datasheet](https://cdn-shop.adafruit.com/product-files/2991/FE1.1s%20Data%20Sheet%20(Rev.%201.0).pdf)
  - [FE1.1 pinout and wiring diagram stuffs i guess](https://www.open-electronics.org/terminus-fe1-1-usb-hub-board-the-solution-to-connect-four-usb-devices/)

### probably not as useful
- USB passthrough keylogger hardware
  - USB Rubber Ducky
    - [Docs](https://docs.hak5.org/hak5-usb-rubber-ducky/ducky-script-basics/keystroke-injection#system-keys)
  - USBKeyLogger (various branches)
    - https://github.com/Push3AX/USBKeylogger
    - https://github.com/justcallmekoko/USBKeylogger
- USB keystroke injector
  - https://github.com/AmirrezaNasiri/usb-keystroke-injector
  - https://www.hackster.io/AmirrezaNasiri/usb-keystroke-injector-arduino-badusb-2767d0

### Other things to research:
- https://en.wikipedia.org/wiki/BadUSB
- https://github.com/0xADE1A1DE/USB-Injection
- https://hackaday.io/project/183688-diy-usb-20-4-port-hub
- https://www.amazon.com/One-Handed-Mechanical-Keyboard-Programming-Swappable/dp/B09PD2BWHL/
