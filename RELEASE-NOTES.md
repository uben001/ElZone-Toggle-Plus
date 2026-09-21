# ElZone Toggle+Plus — ISO-specific scales

Fix 11 adds ISO-specific legend extensions and red labels beyond the selected
clipping point, plus a semi-transparent backdrop with 8-pixel side margins and
no bottom margin. It preserves half-second legend toggling, default legend on,
menu preference/recovery and warm-restart handling from Fix 10.

- ISO 100/200: +3 colour through the right edge; +4/+5/+6 labels red.
- ISO 400/3200: +5 colour through the right edge; +6 label red.
- All other ISO values: original colours and white labels.

Original SIGMA fp firmware 5.02 only. RAM-only standalone AutoRun.
The owner reported all 80 Fix 11 ARM scenarios passing and package/source
identity passing. Latest visual changes and real camera transitions still need
hardware confirmation. See README.md for installation and recovery.
