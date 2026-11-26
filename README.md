![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg) ![](../../workflows/wokwi_test/badge.svg) ![](../../workflows/fpga/badge.svg)

# Quiz Bee Buzzer Switch

A 5-player quiz bee buzzer with lock-out latches, a 3-bit encoder and a 7-segment winner display, built from 61 basic logic gates (AND, OR, NOT, NAND) in Wokwi for [Tiny Tapeout](https://tinytapeout.com). Pure logic gates, no microcontroller and no clock, which makes it a good teaching example for basic logic circuits: SR latches, lock-out logic, encoders and decoders.

- [Read the documentation for project](docs/info.md)

## Overview

- **Inputs:** `ui[0]`..`ui[4]` are buzzers 1-5, `ui[5]` is CLEAR (all active high, use pull-downs).
- **Outputs:** `uo[0]`..`uo[6]` drive a common-cathode 7-segment display (a-g); `uo[7]` (DP) is always 0.
- **Behaviour:** the first buzzer pressed wins and the display shows its number (`1`-`5`); all other buzzers are locked out until CLEAR is pressed. Idle shows `0`. Press CLEAR once after power-up.
- **Design:** five cross-coupled NAND latches with a 4-AND lock-out chain each, an encoder, and a 7-segment decoder. All gates sit inside the chip between the Wokwi input and output blocks.

## Wokwi project

The design lives in Wokwi (`wokwi_id` in [info.yaml](info.yaml)). The GitHub action fetches the digital netlist from Wokwi and builds the ASIC files. The `wokwi_id` is the number after `wokwi.com/projects/` in your project's URL; after changing the diagram, make sure it points to the updated project.

Wokwi link: https://wokwi.com/projects/481740336442682369

## Enable GitHub actions to build the results page

- [Enabling GitHub Pages](https://tinytapeout.com/faq/#my-github-action-is-failing-on-the-pages-part)

## Resources

- [FAQ](https://tinytapeout.com/faq/)
- [Digital design lessons](https://tinytapeout.com/digital_design/)
- [Learn how semiconductors work](https://tinytapeout.com/siliwiz/)
- [Join the community](https://tinytapeout.com/discord)
- [Build your design locally](https://www.tinytapeout.com/guides/local-hardening/)
