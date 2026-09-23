# Sofle Choc or MX with 2 encoders.  Testing repo for trackpad wireless build

Flash firmware:
1. Keep both halves powered on.
2. Plug in right half. > press the physical reset button(located on the inner sides) twice quickly. > That will open a new directory on your computer called nice nano. > drag and drop the settings_reset file into that directory. (after transfer it will auto unmount and may give an error.  Ignore this error and continue.) > after transfer unplug right half.
3. Plug in left half. > press physical reset button twice quickly. > Drag and drop same settings_reset file into directory. > after transfer leave plugged in.
4. Press physical reset button twice. > drag and drop sofle_left firmware into directory. > after transfer unplug. *if using displays use the nice view one
5. Plug in right half > press reset button twice again > drag and drop sofle_right firmware into directory. *if using displays use the nice view one
*My shops https://keyboard-hoarders.com & https://keyboardhoarders.etsy.com
![IMG_0823](https://github.com/user-attachments/assets/2ea9dfec-71c9-428f-aef8-a898e3273b3d)


## Keymap
![sofle2enc](https://github.com/user-attachments/assets/97862878-3886-4d13-90c4-bc0ee6767be2)


## Trackpad (Azoteq TPS43)

The right half has an Azoteq TPS43 trackpad instead of a nice!view display
(`sofle_right` is built without `nice_view_adapter nice_view` in `build.yaml`,
which frees the OLED header's I2C pins and the nice!view CS pad).

| TPS43 pin | nice!nano pad |
|---|---|
| VDD | 3V (OLED header) |
| GND | GND (OLED header) |
| SDA | D2 (OLED header "SDA/MOSI" pad) |
| SCL | D3 (OLED header "SCL/SCK" pad) |
| RDY | D0 |
| RST | D1 (nice!view CS pad) |

Note: RDY is on **D0**, not D21 as on the lily58/corne trackpad builds - on the
Sofle, D20/D21 are the right encoder's A/B pins, so D21 isn't available. D4
can't be used either: the PCB routes it to the first matrix row, so RDY there
makes the trackpad type "6789" instead of moving the cursor. Both encoders keep
working with this wiring.

After changing `config/west.yml` you'll need to run `west update` (or let the
GitHub Action do it) to pull in the trackpad driver module before building.

Cursor movement, scrolling, tap-to-click, two-finger right-click,
press-and-hold drag, pinch-to-zoom, and 4-direction swipes all work out of the
box. If the cursor is inverted or the axes are swapped once you flash it,
adjust the `switch-xy` / `invert-x` / `invert-y` / `invert-scroll-y` properties
in `config/sofle_right.overlay` to match how the module ends up mounted.
Swipe/zoom shortcuts default to Windows/Linux-style bindings; comment out the
`TRACKPAD_WIN_MODE` define at the top of `config/sofle_left.overlay` for
macOS-style shortcuts instead.


## Bluetooth
![soflebluetooth](https://github.com/user-attachments/assets/6c6c1d46-74e9-4e91-8191-667fd3f0ec6d)
