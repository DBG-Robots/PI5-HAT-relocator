# PI5-HAT-relocator

[![English](https://img.shields.io/badge/English-switch-lightgrey)](README.md) [![Deutsch](https://img.shields.io/badge/Deutsch-ausgewählt-blue)](README.de.md)

Eine einfache, flache KiCad-Platine, mit der das Kinematics-Kit-HAT in einen schmalen Roboterrahmen passt: Buchsenleisten oben, Stiftleisten unten.

![3D-Rendering der PI5-HAT-relocator-Platine](images/board-3d.png)

## Hintergrund

Unser Roboter nutzt das **Kinematics Kit** von EduArt Robotik in der Variante mit Raspberry-Pi-HAT (wie im Roboter Eduard) als Motor- und Antriebselektronik. Dieselben Module gibt es als [Kinematics Kit Kim](https://www.eduart-robotik.com/products/kinematicskit-kim), dort mit einer reinen Ethernet-Platine statt des Pi-HATs. Im Originallayout ragen die Motoranschlüsse **seitlich** aus dem HAT heraus. Für die meisten Aufbauten ist das unproblematisch, es kostet aber Breite, und genau die haben wir nicht.

## Das Problem

- **Breitenlimit von 30 cm.** Das ist die wichtigste Einschränkung, gegen die wir ankämpfen. Alles, auch die seitlich abstehenden Anschlüsse des Kits, muss in dieses Maß passen.
- **Sehr flacher Rahmen.** Unsere Doppelquerlenker-Federung (Double Wishbone, 3 Räder pro Seite) sitzt an den **Seiten** des Roboters. Die meisten anderen Roboter der Liga platzieren die Federung *unter* dem Elektronikgehäuse, was den Schwerpunkt nach oben verlagert. Wir haben uns für die seitliche Anordnung entschieden, um einen tieferen Schwerpunkt zu erreichen, dafür bleibt für die Elektronik aber deutlich weniger Platz in Breite und Höhe.

## Die Lösung

Diese Platine verlegt die Anschlüsse des HATs. Indem der obere Teil des Kinematics-Kit-HATs um **90°** gedreht wird, liegen die Motoranschlüsse nicht mehr seitlich abstehend, sodass das **komplette Kinematics Kit vollständig in unseren Rahmen passt**, und zwar innerhalb des 30-cm-Breitenlimits und mit dem flachen Profil, das wir brauchen.

<img src="images/kinematics-kit-stack-render.jpg" alt="3D-Rendering des Kinematics-Kit-Stapels auf einem Raspberry Pi 5 mit dem PI5-HAT-relocator zwischen Adapterplatine und Motor-Shields" width="600">

*Der Stapel auf dem Raspberry Pi 5: unten die Adapterplatine, darauf der Relocator (die glatte Platine ohne Bauteile), darüber um 90° gedreht die Motor-Shields, ganz oben das Power-Management.*

Die Platine ist bewusst einfach gehalten:

- **Buchsenleisten oben** und **Stiftleisten unten**, sodass sie zwischen Pi/HAT und dem gedrehten oberen Teil sitzt.
- Kein Flachbandkabel, das hält den Aufbau niedrig und vermeidet zusätzlichen Platzbedarf und Verkabelung.
- Beschriftung im Bestückungsdruck (VCC, GND, EN und Signalpaare) an jedem Anschluss für einfachen Aufbau und einfache Fehlersuche.

## Pinbelegung

Die Platine führt 16 Pins durch (8 zweipolige Leisten oben, 8 unten). Pro Motorkanal (1 und 2) sind das `CH`, `CL`, `EN`, `VCC1`, `VCC2` und dazu `GND`.

Elektrisch wichtig sind nur **3 der 8 Leisten**: eine `VCC`-, eine `EN`- und eine CAN-Leiste (`CH`/`CL`). Das hat uns [snaens](https://github.com/snaens) bestätigt. Über `VCC` fließt nur der Strom für den Raspberry Pi, nicht der Motorstrom: Das Power-Management sitzt ganz oben im Stapel und reicht den Motorstrom nur bis zu den Motorcontrollern durch, nicht durch diese Platine.

Wir führen trotzdem alle 16 Pins durch und bestücken alle Leisten:

- Die Stiftleisten halten den gedrehten oberen Teil mechanisch fest. Ohne sie säße er nicht stabil.
- Die Größe der Platine hängt an der Lage der Steckverbinder. Mit weniger Leitungen wäre sie weder kleiner noch billiger.
- So bleibt die Platine auch nutzbar, falls später mehr Pins gebraucht werden.

Leiterbahnen: Signale 0,2 mm, `VCC` 2,0 mm, `GND` als Fläche auf beiden Lagen.

## Prüfung

KiCad 10.0.3, Stand 11.11.2026:

- **DRC:** keine Fehler, keine offenen Verbindungen. Nur Warnungen: Bestückungsdruck überlappt, Footprints weichen von der Bibliothek ab, und bei x 117 / y 52 mm liegen zwei Durchkontaktierungen übereinander (eine davon kann weg).
- **ERC:** keine Meldungen.

## Dateien

| Datei | Beschreibung |
| --- | --- |
| `MotorControllerHeader.kicad_pro` / `.kicad_sch` / `.kicad_pcb` | KiCad-Projekt, Schaltplan und Platinenlayout |
| `PI5-HAT-relocator.step` | 3D-Modell der bestückten Platine |
| `production/` | Fertigungsdaten (Stückliste, Positionen, Netzliste, Zip) |
| `SketchPi2PHeaders.dxf` | Mechanische Skizze / Umrissreferenz |

## Credits

Entwickelt von DBG-Robots, Merlin Ortner (Dietrich-Bonhoeffer-Gymnasium Oberasbach).
Kinematics Kit von EduArt Robotik ([Kinematics Kit Kim](https://www.eduart-robotik.com/products/kinematicskit-kim) ist die Variante mit Ethernet-Platine).
