![SofleKeyboard default keymap](https://github.com/josefadamcik/SofleKeyboard/raw/master/Images/soflekeyboard.png)
![SofleKeyboard adjust layer](https://github.com/josefadamcik/SofleKeyboard/raw/master/Images/soflekeyboard_layout_adjust.png)


# Default keymap for Sofle Keyboard

Layout in [Keyboard Layout Editor](http://www.keyboard-layout-editor.com/#/gists/76efb423a46cbbea75465cb468eef7ff) and [adjust layer](http://www.keyboard-layout-editor.com/#/gists/4bcf66f922cfd54da20ba04905d56bd4)


Features:

- Symmetric modifiers (CMD/Super, Alt/Opt, Ctrl, Shift)
- Various modes, can be switched (using Adjust layer and the selected one is stored in EEPROM.
- Modes for Qwerty and Colemak support
- Modes for Mac vs Linux/Win support -> different order of modifiers and different action shortcuts on the "UPPER" layer (the red one in the image). Designed to simplify transtions when switching between operating systems often.
- The OLED on master half shows selected mode and caps lock state and is rotated.
- Left encoder controls volume up/down/mute. Right encoder PGUP/PGDOWN.


## Updating

1. Make changes to `keymap.c` and save
2. Run `qmk compile`
3. Detach minijack cable
4. Run `qmk flash`
5. Connect usb-c cable to other half and run `qmk flash` again

## Flashing issues

The homebrew installed version of avrdude resulted in the following error when flashing:

```
% qmk flash  
Ψ Compiling keymap with gmake -r -R -f builddefs/build_keyboard.mk -s flash KEYBOARD=sofle/rev1 KEYMAP=junkafarian KEYBOARD_FILESAFE=sofle_rev1 TARGET=sofle_rev1_junkafarian INTERMEDIATE_OUTPUT=.build/obj_sofle_rev1_junkafarian VERBOSE=false COLOR=true SILENT=false QMK_BIN="qmk"


avr-gcc (Homebrew AVR GCC 8.5.0_2) 8.5.0
Copyright (C) 2018 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

Size before:
   text    data     bss     dec     hex filename
      0   22032       0   22032    5610 sofle_rev1_junkafarian.hex

Copying sofle_rev1_junkafarian.hex to qmk_firmware folder                                           [OK]
Checking file size of sofle_rev1_junkafarian.hex                                                    [OK]
 * The firmware size is fine - 22032/28672 (76%, 6640 bytes free)
Flashing for bootloader: caterina
Waiting for USB serial port - reset your controller now (Ctrl+C to cancel)....
Device /dev/tty.usbmodem1201 has appeared; assuming it is the controller.
Waiting for /dev/tty.usbmodem1201 to become writable.
avrdude warning: mosi is deprecated, will be removed in v8.0, use sdo [/opt/homebrew/etc/avrdude.conf:404]
...
avrdude warning: has_updi is deprecated, will be removed in v8.0, use prog_modes [/opt/homebrew/etc/avrdude.conf:18001]
avrdude warning: System wide configuration file version ()
        does not match Avrdude build version (7.3)
avrdude error: cannot find programmer id avr109
use -c? to see all possible programmers
gmake: *** [platforms/avr/flash.mk:173: flash] Error 1
```

reinstalling didn't seem to make a difference, but installing avrdude from source [following these instructions](https://github.com/avrdudes/avrdude/wiki/Building-AVRDUDE-for-macOS) seemed to work. N.B. I needed to uninstall avrdude without uninstalling qmk through homebrew so ran `brew uninstall --ignore-dependencies avrdude`

