# PI5-HAT-relocator

[![English](https://img.shields.io/badge/English-switch-lightgrey)](README.md) [![Deutsch](https://img.shields.io/badge/Deutsch-ausgewählt-blue)](README.de.md)

Eine einfache, flache KiCad-Platine, mit der das Kinematics-Kit-HAT in einen schmalen Roboterrahmen passt: Buchsenleisten oben, Stiftleisten unten.

![3D-Rendering der PI5-HAT-relocator-Platine](images/board-3d.png)

## Hintergrund

Unser Roboter nutzt das **Kinematics Kit** von Eduard als Motor- und Antriebselektronik. Im Originallayout ragen die Motoranschlüsse **seitlich** aus dem HAT heraus. Für die meisten Aufbauten ist das unproblematisch, es kostet aber Breite, und genau die haben wir nicht.

## Das Problem

- **Breitenlimit von 30 cm.** Das ist die wichtigste Einschränkung, gegen die wir ankämpfen. Alles, auch die seitlich abstehenden Anschlüsse des Kits, muss in dieses Maß passen.
- **Sehr flacher Rahmen.** Unsere Doppelquerlenker-Federung (Double Wishbone, 3 Räder pro Seite) sitzt an den **Seiten** des Roboters. Die meisten anderen Roboter der Liga platzieren die Federung *unter* dem Elektronikgehäuse, was den Schwerpunkt nach oben verlagert. Wir haben uns für die seitliche Anordnung entschieden, um einen tieferen Schwerpunkt zu erreichen, dafür bleibt für die Elektronik aber deutlich weniger Platz in Breite und Höhe.

## Die Lösung

Diese Platine verlegt die Anschlüsse des HATs. Indem der obere Teil des Kinematics-Kit-HATs um **90°** gedreht wird, liegen die Motoranschlüsse nicht mehr seitlich abstehend, sodass das **komplette Kinematics Kit vollständig in unseren Rahmen passt**, und zwar innerhalb des 30-cm-Breitenlimits und mit dem flachen Profil, das wir brauchen.

Die Platine ist bewusst einfach gehalten:

- **Buchsenleisten oben** und **Stiftleisten unten**, sodass sie zwischen Pi/HAT und dem gedrehten oberen Teil sitzt.
- Kein Flachbandkabel, das hält den Aufbau niedrig und vermeidet zusätzlichen Platzbedarf und Verkabelung.
- Beschriftung im Bestückungsdruck (VCC, GND, EN und Signalpaare) an jedem Anschluss für einfachen Aufbau und einfache Fehlersuche.

## Dateien

| Datei | Beschreibung |
| --- | --- |
| `MotorControllerHeader.kicad_pro` / `.kicad_sch` / `.kicad_pcb` | KiCad-Projekt, Schaltplan und Platinenlayout |
| `PI5-HAT-relocator.step` | 3D-Modell der bestückten Platine |
| `production/` | Fertigungsdaten (Stückliste, Positionen, Netzliste, Zip) |
| `SketchPi2PHeaders.dxf` | Mechanische Skizze / Umrissreferenz |

## Credits

Entwickelt von DBG-Robots, Merlin Ortner (Dietrich-Bonhoeffer-Gymnasium Oberasbach).
Kinematics Kit von Eduard.
