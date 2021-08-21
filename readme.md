# SKYSCAN - Basic coordinate reference system
This is a proof-of-concept location and coordinate system for Starbase ships. **_It is not meant to replicate or replace ISAN_**, which is a much more comprehensive system and you should probably just use that. ISAN is better than Skyscan in almost every way. In fact, [here's a link to that](https://isan.to/isan.pdf) because that's probably what you want instead. 

## Installation

  
1. Place 3 fixed Nav Recievers on hardpoints or turntables, preferably facing different sections of the sky (0°, 120° and 240° are good). Set up each Nav Receiver device fields as follows:
    - Nav Receiver 1
        - `Frequency : 1`
        - `ListenAngle : 180`
        - Replace `Message` device field with `nsig`  
        - Replace `SignalStrength` field with `nss`
        - `TargetMessage : "origin_north"`
        - If on turntable, recommend `TurretRotation : 0`
    - Nav Receiver 2
        - `Frequency : 1`
        - `ListenAngle : 180`
        - Replace `Message` device field with `esig`  
        - Replace `SignalStrength` field with `ess`
        - `TargetMessage : "origin_east"`
        - If on turntable, recommend `TurretRotation : 120`
    - Nav Receiver 3
        - `Frequency : 1`
        - `ListenAngle : 180`
        - Replace `Message` device field with `wsig`  
        - Replace `SignalStrength` field with `wss`
        - `TargetMessage : "origin_west"`
        - If on turntable, recommend `TurretRotation : 240`
2. Install and connect a YOLOL Device Rack with the following:
    - [skyscan.yolol](/skyscan.yolol) on a Basic YOLOL chip:
        - This is the main SKYSCAN program which controls both the receivers and display output
    - A blank memory chip with default device field names (`ChipField1`, `ChipField2`, etc)
3. Install controls and display:
    - Add a Hybrid Button with 1st device field set to `SkyScan`
	    - `ButtonStyle : 1`
    - Add a Text Panel with 1st device field `:Location`
4. If you want to save coordinates, run another Basic YOLOL chip with [locmark.yolol](/LocationMark/locmark.yolol)
    - Add a text panel with 1st device field `SavedLoc1`
  
*<sub>Do not run SkyScan-Display.yolol concurrently, this script will handle its own display.<sub>

  
## Operation
Press the `SKYSCAN` button to turn on realtime scanning and coordinate updates. Your `Location` display will show your relative distance (in KM) from the Origin North, Origin East, and Origin West radio transmitters

Press `SKYSCAN` again to turn off and reset (i.e. to save battery/fuel).

Press `LOCMARK` button to save a location to longer-term memory. 
@TODO Cycle locmark savedloc1 and savedloc2

@TODO Speed plugin?


