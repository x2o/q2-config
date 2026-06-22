# Qidi Q2 Custom Configs

To ensure that updates don't make me lose my customizations.

#Slicer Start G-Code

```
INIT_MAPPING_VALUE
PRINT_START BED=[bed_temperature_initial_layer_single] HOTEND=[nozzle_temperature_initial_layer] CHAMBER=[chamber_temperature] EXTRUDER=[initial_no_support_extruder]
SET_PRINT_STATS_INFO TOTAL_LAYER=[total_layer_count]
T[initial_tool]
M83
LINE_PURGE
SKEW_PROFILE LOAD=Calilantern
PROTECT_HOTEND_ON
```
#Slicer End G-Code

```
PROTECT_HOTEND_OFF
DISABLE_BOX_HEATER
M141 S0
M140 S0
BUFFER_MONITORING ENABLE=0
DISABLE_ALL_SENSOR
G1 E-3 F1800
G0 Z{max_layer_z + 3} F600
UNLOAD_FILAMENT T=[current_extruder]
G0 Y270 F12000
G0 X90 Y270 F12000
{if max_layer_z < max_print_height / 2}G1 Z{max_print_height / 2 + 10} F600{else}G1 Z{min(max_print_height, max_layer_z + 3)}{endif}
M104 S0
BED_MESH_CLEAR
G31
CLEAR_LAST_FILE
SET_SKEW CLEAR=1
BEEP I=2 DUR=500
SET_FAN_SPEED FAN=chamber_circulation_fan SPEED=1
UPDATE_DELAYED_GCODE ID=delayed_fan_off DURATION=300
M84
```
