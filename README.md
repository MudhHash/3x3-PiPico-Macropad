# 9x9-PiPico-Keypad
This 9-key macropad is designed using a Raspberry Pi Pico microcontroller programmed with CircuitPython using KMK firmware.

## Overview
This repository provides the schematics and code used in this project. The goal of this project was to build a compact, low-cost, and easily programmable marcopad which ultimately serve the purpose of offering quick access to frequently used shortcuts, macros, and commands in a streamlined, tactile form.

<p>
<img src="https://github.com/user-attachments/assets/cb409a6a-1e72-40f1-b899-9c6feae2a3f9" width="50%"/><img src="https://github.com/user-attachments/assets/e8847921-90f3-446d-b79a-8a1b97df8496" width="50%"/>
</p>

## Bill of Materials

Item | Quantity | Cost
--- | --- | ---
Macropad PCB | 1 | $0.40 (Excluding Shipping)
Raspberry Pi Pico | 1 | $9.95 
Mechanical Keyboard Switch | 10 | $4.89
PBT Blank Keycaps | 10 | $9.59

## PCB
The PCB was designed using KiCAD with a focus on simplicity, compactness, and ease of assembly. It includes all the necessary connections for the microcontroller, switches, and diodes, while minimizing overall footprint and cost.

[Files](https://github.com/MudhHash/3x3-PiPico-Macropad/tree/main/PCB) Included:
* .kicad_pcb – Main PCB layout
* .sch – Schematic design
<p>
<img src="https://github.com/user-attachments/assets/6256552b-c434-4c3f-8ffc-dc88d65c02b0" width="50%"/><img src="https://github.com/user-attachments/assets/f983f34f-efbb-4d6c-9545-3c53d105d367" width="50%"/>
</p>

## Firmware and Code
This macropad uses KMK Firmware, keyboard firmware written in CircuitPython. KMK is ideal for small custom keyboards and macropads due to its ease of use, real-time reprogrammability, and active development community.

How to Implement:
* Flash the CircuitPython .uf2 file for your board from [circuitpython.org](https://circuitpython.org/downloads)
* Drag-and-drop the firmware onto the mounted USB drive (CIRCUITPY)
* Install [KMK](https://github.com/KMKfw/kmk_firmware) by copying its files into the lib directory on the device
* Add or edit the code.py file to define your keymap and macros
* Example Code:
```bash
import board  # Access pin definitions specific to the microcontroller
from kmk.kmk_keyboard import KMKKeyboard  # Base KMK keyboard class
from kmk.keys import KC  # Keycode library for standard key constants
from kmk.scanners.digitalio import DiodeOrientation  # Diode orientation options for the matrix

# Create a keyboard object instance
keyboard = KMKKeyboard()

# Define the row and column GPIO pins based on your physical wiring
keyboard.row_pins = (board.GP10, board.GP11, board.GP12)  # 3 row pins
keyboard.col_pins = (board.GP6, board.GP7, board.GP8)     # 3 column pins

# Specify the diode orientation used in the matrix (important for correct scanning)
keyboard.diode_orientation = DiodeOrientation.COL2ROW

# Define the keymap layout as a flat list of keycodes (3x3 matrix in this case)
keyboard.keymap = [
    [KC.KP_1, KC.KP_2, KC.KP_3,
     KC.KP_4, KC.KP_5, KC.KP_6,
     KC.KP_7, KC.KP_8, KC.KP_9]
]

# Run the keyboard firmware loop when the script is executed
if __name__ == '__main__':
    keyboard.go()

```

Feel free to modify the code to suit your own workflow!

## Resources
* KiCad Footprints: The component footprints used in this project were sourced from [ScottoKeebs](https://github.com/joe-scotto/scottokeebs).
