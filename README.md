# MODIFIED BCN3D Sigma Firmware

In this version of 1.26, Duplication and Mirror modes are enabled.
Duplication Mode and Mirror modes have been tested.

Here is there start code which needs to be manually edited into your gcode.
In this case, it was heating the hot ends to 240, for ABS printing.

DUPLICATION MODE:

```
;FLAVOR:Marlin
;TIME:920
;Filament used: 0.321482m
;Layer height: 0.2
;POSTPROCESSED
;Generated with Cura_SteamEngine 2.7.0
M190 S100
M104 T0 S240
M104 T1 S240
M109 T0 S240
M109 T1 S240

;Sigma ProGen 2.0.0 (Build 18JH2019)
;Sigma Vitamins plugin enabled (Build 18JH2019)
; - Fix Tool Change Z Hop
; - SmartPurge
; - Fix Temperature Oscilation

G21		;metric values
G90		;absolute positioning
M82		;set extruder to absolute mode
M107		;start with the fan off
G28 X0 Y0		;move X/Y to min endstops
G28 Z0		;move Z to min endstops
G1 Z5 F200		;safety Z axis movement

T0		;switch to the left extruder
G92 E0		;zero the extruded length
G1 E20 F50		;extrude 20mm of feed stock
G92 E0		;zero the extruded length
G4 P2000		;stabilize hotend's pressure
G1 F2400 E-8		;retract

T1		;switch to the right extruder
G92 E0		;zero the extruded length
G1 E20 F50		;extrude 20mm of feed stock
G92 E0		;zero the extruded length
G4 P2000		;stabilize hotend's pressure
G1 F2400 E-8		;retract

G90		;absolute positioning
T0		;switch to the left extruder
M605 S2 X105.0		;set dual carriage mode, Duplication, 105mm offset (Half build platform)
G92 E-8		;zero the extruded length again
```

MIRROR MODE:

```
;FLAVOR:Marlin
;TIME:2996
;Filament used: 0.95626m
;Layer height: 0.2
;POSTPROCESSED
;Generated with Cura_SteamEngine 2.7.0

M190 S100
M104 T0 S240
M104 T1 S240
M109 T0 S240
M109 T1 S240

;Sigma ProGen 2.0.0 (Build 18JH2019)
;Sigma Vitamins plugin enabled (Build 18JH2019)
; - Fix Tool Change Z Hop
; - SmartPurge
; - Fix Temperature Oscilation

G21		;metric values
G90		;absolute positioning
M82		;set extruder to absolute mode
M108 P1		;enable layer fan for idle extruder
M107		;start with the fan off
G28 X0 Y0		;move X/Y to min endstops
G28 Z0		;move Z to min endstops
G1 Z5 F200		;safety Z axis movement

T1		;switch to the right extruder
G92 E0		;zero the extruded length
G1 E20 F50		;extrude 20mm of feed stock
G92 E0		;zero the extruded length
G4 P2000		;stabilize hotend's pressure
G1 F2400 E-8		;retract

T0		;switch to the left extruder
G92 E0		;zero the extruded length
G1 E20 F50		;extrude 20mm of feed stock
G92 E0		;zero the extruded length
G4 P2000		;stabilize hotend's pressure
G1 F2400 E-8		;retract

G90		;absolute positioning
T0		;switch to the left extruder
M605 S4 X105.0		;set dual carriage mode, Mirror Mode, 105mm offset (Half build platform)
G92 E-8		;zero the extruded length again
```

Just make sure that the `G1 F2400 E-8` is the same value as the `G92 E-8` found at the end.
Also if using Vitamins, make sure the 'Prevent Filament Grinding' is disabled, as this does not play ball at the moment.
