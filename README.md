# PI5-HAT-relocator

[![English](https://img.shields.io/badge/English-selected-blue)](README.md) [![Deutsch](https://img.shields.io/badge/Deutsch-wechseln-lightgrey)](README.de.md)

A simple, shallow KiCad board that lets the Kinematics Kit HAT fit into a narrow robot frame: female connectors on top, male connectors on bottom.

![3D render of the PI5-HAT-relocator board](images/board-3d.png)

## Background

Our robot uses the **[Kinematics Kit Kim](https://www.eduart-robotik.com/products/kinematicskit-kim)** by EduArt Robotik (maker of the Eduard robot) as its motor and drive electronics. In its canonical layout, the motor connectors stick out on the **sides** of the HAT. That is fine for most builds, but it costs width, and width is exactly what we do not have.

## The problem

- **30 cm width limit.** This is the main constraint we are fighting. Everything, including the connectors that stick out of the kit, has to fit inside it.
- **Very shallow frame.** Our double wishbone suspension (3 wheels per side) is mounted on the **sides** of the robot. Most other robots in the league put the suspension *below* the electronics enclosure, which raises the center of mass. We chose the side-mounted layout for a lower center of mass, but it leaves a much narrower and shallower space for the electronics.

## The solution

This board relocates the connectors of the HAT. Rotating the top part of the Kinematics Kit HAT by **90°** brings the motor connectors out of the side-protruding position, so the **entire Kinematics Kit fits fully inside our frame** while staying within the 30 cm width limit and the low profile we need.

The board is intentionally simple:

- **Female connectors on top** and **male connectors on bottom**, so it sits between the Pi/HAT and the rotated top section.
- No ribbon cable, which keeps the stack low and avoids extra bulk and wiring.
- Silkscreen labels (VCC, GND, EN and signal pairs) on every connector to make assembly and debugging easy.

## Pinout

The board passes through 16 pins (8 two-pin connectors on top, 8 on the bottom). Per motor channel (1 and 2) these are `CH`, `CL`, `EN`, `VCC1`, `VCC2`, plus `GND`.

Only 6 of them are needed electrically. We still pass all 16 through and populate every connector:

- The pin headers hold the rotated top part in place mechanically. Without them it would not sit firmly.
- The board size is set by the connector positions. With only 6 traces it would be neither smaller nor cheaper.
- The board stays usable if more pins are needed later.

Traces: signals 0.2 mm, `VCC` 2.0 mm, `GND` as a pour on both layers.

## Checks

KiCad 10.0.3, as of 2026-11-11:

- **DRC:** no errors, no unconnected pads. Warnings only: silkscreen overlaps, footprints differ from the library, and two vias are stacked at x 117 / y 52 mm (one can be removed).
- **ERC:** no messages.

## Files

| File | Description |
| --- | --- |
| `MotorControllerHeader.kicad_pro` / `.kicad_sch` / `.kicad_pcb` | KiCad project, schematic and PCB layout |
| `PI5-HAT-relocator.step` | 3D model of the assembled board |
| `production/` | Fabrication outputs (BOM, positions, netlist, zip) |
| `SketchPi2PHeaders.dxf` | Mechanical sketch / outline reference |

## Credits

Developed by DBG-Robots, Merlin Ortner (Dietrich-Bonhoeffer-Gymnasium Oberasbach).
[Kinematics Kit Kim](https://www.eduart-robotik.com/products/kinematicskit-kim) by EduArt Robotik.
