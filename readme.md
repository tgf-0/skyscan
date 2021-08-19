# SkyScan - Basic coordinate reference system

## Requirements:   
- Nav Receiver with standard fields,   
    - `Angle` set to 20  
- A textpanel with device field set to `navinfo`  
- A button with device field set to `SkyScan`  
    - `Style` 1  
- Turret Turntable with device fields:  
    - SSTT  
- Memory chip with fields:   
    - `last_n`  
    - `last_e`  
    - `last_w`  




# skyscan-turntable.nolol

Turntable version with more comprehensive scanning.  
Controls receiver, scanning and storing coordinates.  
Works best when not moving.  
Nav receiver should be on `frequency`:1  
Also need to run SkyScan-display.yolol for displaying info  
Turntable must have device fields:   
- `SSTR` (Replacing `TurretRotation`)  
- `SSCTR` (Replace `TurretCurrentRotation`)  
Memory chip must be default named (`ChipField1`, `ChipField2`, etc)  
- CF1 is Origin North  
- CF2 is Origin East  
- CF3 is Origin West  
- CF4 is Scan index (for matching coords to a scan run)  
If running locmark.yolol:  
- CF5 is Saved Location 1 Origin North  
- CF6 is Saved Location 1 Origin East  
- CF7 is Saved Location 1 Origin West  
- CF8 is Saved Location 2 Origin North  
- CF9 is Saved Location 2 Origin East  
- CF10 is Saved Location 2 Origin West  




