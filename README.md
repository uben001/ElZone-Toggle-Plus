# ElZone Toggle+Plus — ISO-specific scales

Experimental RAM-only EL Zone button toggle and ISO-specific legend for the
**original SIGMA fp running firmware 5.02**. This build is Fix 11.

## Install

1. Assign **False Color** to a custom button and select **EL ZONE** as its style.
2. Turn the camera off and copy this folder's `AutoRun.txt` to the SD-card root,
   replacing the previous AutoRun file.
3. Disconnect USB. Remove the battery for 10 seconds when changing builds to
   clear the previous RAM patch, then reinsert it and start the camera.

This is a standalone AutoRun. Do not concatenate it with other patches.
To revert, remove `AutoRun.txt` and cold-boot the camera. Nothing is flashed.
This build targets fp 5.02 only, not fp L or other firmware versions.

## Controls

- Short press from off: enable EL Zone with the legend.
- Short press while on: turn off EL Zone and the legend.
- Hold for half a second from off: enable both while the button is still held.
- Hold for half a second while on: toggle only the legend.
- Menus hide the legend; returning remembers whether it was shown or hidden.

## ISO-specific legends

| Selected ISO | Colour-band extension | Red labels |
| --- | --- | --- |
| 100, 200 | Existing +3 colour continues to the right edge | +4, +5, +6 |
| 400, 3200 | Existing +5 colour continues to the right edge | +6 |
| All other values | Original legend | None |

The clipping-point label itself stays white. Auto/unknown ISO uses the
original legend; effective Auto ISO tracking is not implemented.
These are user-specified legend thresholds. They do not change native EL Zone
image colours, sensor processing or ISO settings, and are not a calibration
claim for every recording mode.

The scale uses 90% of the original width, a cropped band height, and the approved
bottom placement at the 16:9 picture boundary. It has one semi-transparent dark
backdrop, 8-pixel side margins, and no bottom margin. Colours reach the lower
edge; labels and top padding share the same backdrop.

## Validation

The packaged AutoRun matches the rebuilt source. The camera owner reported
**80 passing ARM-emulation scenarios** for Fix 11, covering red labels,
geometry, ISO changes, gestures, menu behavior and simulated reboots.
Fix 10 was confirmed working on the camera. Fix 11's latest visual changes
and real transitions still need camera confirmation at publication preparation.
Emulation stubs firmware timing/display services and cannot prove real camera
frame alignment, autofocus behavior or every shutdown/restart transition.

## Source and rebuilding

`src/fcscale.S` contains the ARM overlay and gesture code.
`src/fcscale_native.inc.S` contains the generated legend tables and glyph masks.
`tools/build_fcscale_autorun.py` rebuilds the standalone AutoRun.
`tools/verify_gestures.py` is the current scenario suite; `verify_fcscale.py`
provides its emulator support and is not the current standalone test entry point.

To rebuild, provide the verified fp 5.02 MAIN image at
`analysis/MAIN_c0000000.bin` (the builder verifies its SHA-256).
Proprietary firmware images are not included. Install Python dependencies
`unicorn` and `capstone`, and provide the fpSup assembler helper at
`reference/fpSup/fp_usb_shell/armasm.py` from
[ijigen/fpSup](https://github.com/ijigen/fpSup/tree/58c2b1c5223e6fdb513b61805a823aa3bf8de9b4).
The helper also needs its normal ARM assembler toolchain available.

```sh
python3 tools/build_fcscale_autorun.py
python3 tools/verify_gestures.py
```

The rebuilt card is `builds/fcscale/AutoRun.txt`.

## Credits

Based on [lachgil/sigma-fp-lab](https://github.com/lachgil/sigma-fp-lab), its
False Color toggle and OSD research, with assembler tooling and research from
[ijigen/fpSup](https://github.com/ijigen/fpSup).
Legend colours and glyphs originate from the camera's native EL Zone scale.

## AutoRun checksum

SHA-256: `cd4f6c75b64caf73e026dde6981ab706d7cba3a10248553ed06a64daf2965bbc`
