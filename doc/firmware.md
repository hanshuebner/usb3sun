[README](../README.md) >

firmware
========

## how to build the firmware

1. fix the -DCFG_TUSB_CONFIG_FILE in platformio.ini for your absolute path
2. apply patches to <.pio/libdeps/pico/Adafruit TinyUSB Library/src/host/usbh.c> (version 2.0.1)
    1. `git apply tinyusb1.patch` — [tinyusb1.patch](tinyusb1.patch) fixes a race condition in enumeration when two devices are connected at the same time (hathach/tinyusb#1786, upstreamed in 2.0.2 as hathach/tinyusb#1960)
    2. `git apply tinyusb2.patch` — [tinyusb2.patch](tinyusb2.patch) improves compatibility with Microsoft Wired Keyboard 600 (045E:0750) and 400 (045E:0752) when CFG_TUSB_DEBUG < 2 by adding a delay in tuh_control_xfer

### windows users

if you encounter problems with paths being too long:

1. open an admin command prompt (Win+X, A)
2. `git config --system core.longpaths true`
3. whenever you get `[WinError 3]` or `[WinError 145]`, delete `%USERPROFILE%\.platformio\.cache\tmp`

if you get “patch does not apply” errors in step 2:

1. change the line endings from CRLF to LF in <.pio/libdeps/pico/Adafruit TinyUSB Library/src/host/usbh.c>
