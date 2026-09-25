# nice_view_custom

ZMK's stock `nice_view` shield, right (peripheral) half only, showing one of 30
Hammerbeam images at random on boot instead of balloon/mountain.

Art and original shield: https://github.com/GPeye/hammerbeam-slideshow (MIT).
Vendored rather than used as a west module, so this config keeps building if
that repo goes away.

## Revert to stock

In `build.yaml`, change the right half back to `nice_view`, then delete this
directory. Nothing else in the repo references it.

## What differs from stock

Copied from ZMK v0.3 `app/boards/shields/nice_view`. The only changes:

- `widgets/art.c` — the 30 images, replacing balloon + mountain
- `widgets/peripheral_status.c` — two spots, both marked `Differs from stock`
- `CMakeLists.txt` — peripheral only; this will not compile on the central half
- `custom_status_screen.c` — includes `peripheral_status.h`, which drops two
  canvas buffers the peripheral never uses
- `Kconfig.shield`, `Kconfig.defconfig`, `nice_view_custom.zmk.yml` — renamed

## Upgrading ZMK

Copy these over from the new ZMK `nice_view` as-is:

    nice_view_custom.conf  nice_view_custom.overlay  widgets/bolt.c
    widgets/util.c  widgets/util.h  widgets/peripheral_status.h

Then reapply the two marked lines in `peripheral_status.c`. `art.c` never changes.
