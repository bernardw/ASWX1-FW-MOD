# ASWX1-FW-Mod
Artillery Sidewinder X1 Firmware Mod  

The ASWX1-FW-Mod is an optimization for the Artillery Sidewinder X1 3D printer consisting of the interdependent firmware for the MKS GEN L motherboard and the Makerbase MKS-TFT 3.2 touch display.

The repository here is the continuation of **Robscar's firmware** from Thingiverse 
https://www.thingiverse.com/thing:3856144 with its support and expertise.

## Releases

##.02.2020 ASWX1-FW-Mod-0.1

## Optimizations

The Artillery Sidewinder X1 is delivered with Marlin 1.19 and deactivated EEPROM memory function (M500)
This FW-Mod brings the Marlin firmware of the printer motherboard to the current version of 2.0.3 and unlocks useful functions.

1. **Save to EEPROM**  
   Enabled EEPROM to persist settings.  
   Now you can store PIDs and ZOffsets to EEPROM  
2. **P.I.D. Autotune**  
  PID Tuning improves your hotend/bed temperatur stability and will positively impact print quality. This command initiates a           process of heating and cooling to determine the proper PID values for your hotend. This may take up to 5 minutes. During the       tuning process the LED will stay Red. Once the process is finished, the LED will turn Green. Make sure you wait! Your machine      specific PID values are now in use. However, if you want to persist your PID settings you must execute “Store to EEPROM”

3. **Preheat Presets for PLA and PETG**
   lets you easily preheat to given presets, you can change the temps in the mks_config.txt
   
4. **Manual Bed Leveling**  
   Manual Bed Leveling Homes(G28) and turns off all stepper motors except Z-Motors. Now you can freely move your hotend to the   desired positions. I find this helpful for initial bed leveling as you can carefully move your printhead. Do not forget to preheat bed and hotend for accurate leveling. You can use Z+ Z- commands to drive the head up or down overall. However, you need to execute StoreToEEPROM to persist Z Values.
   
5. **Live Adjust Z / Babystepping Z**
   During printing the first layer you can still adjust the distance between the nozzle and the print-bed.  
   E.g. if you find  your print is not sticking you can carefully step down the nozzle or correct it up again   
   without the need to relevel all four screws at the same time.  
   However, this assumes the bed is in level overall but maybe just a little too low or too high overall.  
   You need to execute StoreToEEPROM to persist Z Values.
   
6. **Linear activated**  
   Linear Advance is now activated in Marlin, by default I set the K_Factor to 0, so it is disabled. To enable it using gcode you should first calibrate your specific K factor. You can do this [here](https://marlinfw.org/tools/lin_advance/k-factor.html). Accordingly set the K factor within your slicer using e.g. M900 K0.2

7. **S_CURVE_ACCELERATION activated**
   much quieter now when using Linear Advance  
   
8. **ADAPTIVE_STEP_SMOOTHING activated**
   much quieter now when using Linear Advance



## Installation
### Marlin Firmware for MKS Gen L Motherboard

Optimized Firmware based on [Marlin Firmware Version 2.0](https://github.com/MarlinFirmware/Marlin/tree/2.0.x)
and on Marlin [Artillery Sidewinder X1 config](https://github.com/MarlinFirmware/Configurations/tree/master/config/examples/Artillery/Sidewinder%20X1)


#### Individual adjustments
Individual adjustments can be made in Configuration.h.
The firmware must be recompiled.
The precompiled firmware can be flashed directly without customization. 

#### Flashing
Two methods:  
1. Disconnect the display  
2. Loop method  

### Makerbase MKS-TFT Display

Original http://www.artillery3d.com/DownLoad/15689.html
https://github.com/makerbase-mks/MKS-TFT/tree/master/MKS-TFT2.8-3.2
Is only available as precompiled firmware.
Adjustments / Extensions only possible to a limited extent ...

#### Individual Adjustments
Adjustments can be made via the mks_config.txt.  

#### Flashing
Simply copy all files in the tft folder to a microSD-Card, insert to your printer and reboot printer, wait until process is finished.  
Check for mks_config.txt for further information on how to alter specific settings.


#### Reset to factory defaults
I recommend to reset the newly flashed firmware to its defaults and overwrite any older settings. The gcode command is M502 to reset the firmware to the hardcoded defaults, followed by M500 to save these default setting to EEPROM. You can execute the gcode commands using a terminal program (Arduino has one included) or using the Terminal Tab in octoprint. If you have no serial monitor for running the command you could temporary modify mks_config.txt with a text editor, to include the M502/M500 commands in Line 191 to look like this:
#SaveToEEPROM >moreitem_button4_cmd:M42 P4 S0;M42 P5 S255;M42 P6 S0;M502;M500;G4 S1;M42 P4 S255;M42 P5 S0;M42 P6 S0;

Now, if you press SaveToEEPROM you will reset to factory defaults and save the settings. Everything will get overwritten, so if you already have done PID Tuning you will need to redo this. Do not forget to remove the M502 command after you executed it once, otherwise you will always reset your settings back to defaults and loose PIDs and ZOffsets.

## TIPPS
In case your USB Stick does not work anymore after the upgrade, check the following option on your TFT: SET/File/USB. That was always there but defaulted back to SD after TFT Upgrade

RICS 3D Marlin 2 https://www.youtube.com/watch?v=JlgykMHhMzw
