<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

A 5-contestant quiz bee buzzer built entirely from basic logic gates (61 gates, designed in Wokwi). The first contestant to press a button wins; everyone else is locked out until the host presses CLEAR. The winner's number is shown on a 7-segment display.

1. **Buzzer latches (x5).** Each buzzer has a cross-coupled NAND SR latch. Its set input is `NOT(buttonN AND Q_other1 AND Q_other2 AND Q_other3 AND Q_other4)`, built from a 4-gate AND chain and an inverter, so a press only sets the latch if no other latch has already fired. CLEAR drives the latch reset through an inverter. The latch outputs `Q1..Q5` are **active low**: `1` = idle, `0` = this buzzer won.
2. **Encoder.** Converts the winning buzzer into a 3-bit code (idle = 000, buzzer N = N): `d0 = b1|b3|b5`, `d1 = b2|b3`, `d2 = b4|b5`.
3. **7-segment decoder.** Converts the code to segments a-g for a common-cathode display (segments active high). Idle shows `0`; the winner shows `1`-`5`.

All of the gates (latches, encoder and decoder) are inside the chip, between the input and output pins. The clock and reset pins are not used, because the design is purely gate/latch based.

> **Power-up:** the latches start in an unknown state. Press CLEAR once after power-up.

## Pinout

| Pin | Function |
|---|---|
| `ui[0]`..`ui[4]` | Buzzer 1..5 push buttons (active high) |
| `ui[5]` | CLEAR push button (active high) |
| `ui[6]`, `ui[7]` | Unused (tied low in the design) |
| `uo[0]`..`uo[6]` | 7-segment a..g (common cathode, active high) |
| `uo[7]` | DP (always 0) |
| `uio[7:0]` | Unused |

## How to test

1. Pulse `ui[5]` (CLEAR). The display shows `0`.
2. Press one buzzer button. The display shows that buzzer's number; further presses on the other buttons do nothing, and the winner stays latched after the button is released.
3. Press CLEAR to arm for the next question.

In Wokwi: start the simulation, press keys `1`-`5` for the buzzers and `C` to clear, and watch the 7-segment display.

## External hardware

5 buzzer push buttons and 1 CLEAR push button, each with a pull-down resistor (e.g. 10k to GND) so they read 0 when released, and 1 common-cathode 7-segment display (the Tiny Tapeout demo board display works).

Pressing two buttons at *exactly* the same instant is a genuine race: either may win, but the lock-out guarantees only one ever does.
