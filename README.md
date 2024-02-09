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

## Side goals:

- allow for additional user-configurable buttons
  - perhaps through QMK? or VIA?
  - while using the Bigscreen Beyond, can be useful in various cases where controllers are not necessary -- such as Flight or Driving Simulators

---

## Starting points

- Mechanical keyboard firmware
  - [QMK](https://qmk.fm/) -- already has groundwork for basically every keystroke anyone would need and more
- USB passthrough keylogger hardware
  - USB Rubber Ducky
    - [Docs](https://docs.hak5.org/hak5-usb-rubber-ducky/ducky-script-basics/keystroke-injection#system-keys)
  - USBKeyLogger (various branches)
    - https://github.com/Push3AX/USBKeylogger
    - https://github.com/justcallmekoko/USBKeylogger
- USB keystroke injector
  - https://github.com/AmirrezaNasiri/usb-keystroke-injector

Other things to research:
- https://en.wikipedia.org/wiki/BadUSB
- https://github.com/0xADE1A1DE/USB-Injection
