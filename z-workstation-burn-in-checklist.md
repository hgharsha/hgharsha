# HP Z workstation (128 GB) - 30-day return burn-in checklist

Goal: find any hardware fault before the return window closes. Start date: 2026-11-21. Return deadline: confirm the exact date from the receipt.

Note: I (Claude) had no record of an earlier plan when this was written. If you were given steps elsewhere, merge them in below.

## Photograph and keep
- Receipt, order number, return deadline
- Serial number and product number (sticker on the case)
- Every diagnostic result screen, especially any failure ID and 24-character code

## HP PC Hardware Diagnostics UEFI (F2 at boot)
- [ ] Memory Test > Quick Test (about 59 min at 128 GB) - started 2026-11-21
- [ ] Memory Test > Extensive Test (many hours, run overnight, power plugged in)
- [ ] Processor tests
- [ ] Storage Tests (quick, then extensive on every drive)
- [ ] System Board Test
- [ ] Keyboard Test

## If a memory test fails
- Note the failure ID and 24-character code
- Test one stick at a time to find the bad one
- Contact HP support with the code and request replacement or return

## Beyond the UEFI tests (inside the OS)
- [ ] Check all RAM is detected (128 GB) and runs at the rated speed
- [ ] Stress CPU and RAM for a few hours and watch temperatures
- [ ] Stress the GPU if one is installed
- [ ] Check every drive's SMART health
- [ ] Test all ports, network, audio and display outputs
- [ ] Watch for crashes, freezes, noise or heat over the first week

## Results log
(date, test, result, notes)
