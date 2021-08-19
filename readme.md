# SkyScan - Basic coordinate reference system
This is a proof-of-concept location and coordinate system for Starbase ships. **It is not meant to replicate or replace ISAN**, which is a much more comprehensive system and you should probably just use that. ISAN is better than this in almost every way. In fact, [here's a link to that](https://isan.to/isan.pdf) because that's probably what you want instead. 

# [skyscan-turntable.yolol](SkyScan//Scanner/skyscan-turntable.yolol)
Controls a single nav receiver, performs scanning and storing of coordinates.
Works best when your ship is not moving.

## Requirements:   
  
Run another chip with [skyscan-display.yolol](SkyScan/Display/skyScan-display.yolol) for displaying info on a text panel
  
A working, large nav receiver on a turntable.

Nav receiver should use field `frequency : 1` (default)
    
Turntable must have these device fields: 
  
- `SSTR` (Replacing `TurretRotation`)
  
- `SSCTR` (Replace `TurretCurrentRotation`)
  
A memory chip with default device names (`ChipField1`, `ChipField2`, etc)
  
- `ChipField1` is Origin North
  
- `ChipField2` is Origin East
  
- `ChipField3` is Origin West
  
- `ChipField4 `is Scan index (for matching coords to a scan run)
  
If running [locmark.yolol](SkyScan/LocationMark/locmark.yolol):
  
- `ChipField5` is Saved Location 1 Origin North
  
- `ChipField6` is Saved Location 1 Origin East
  
- `ChipField7` is Saved Location 1 Origin West
  
- `ChipField8` is Saved Location 2 Origin North
  
- `ChipField9` is Saved Location 2 Origin East
  
- `ChipField10` is Saved Location 2 Origin West
  




