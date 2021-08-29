# SkyScan
## Coordinate-based waypoint system
This is a proof-of-concept system for ship location, velocity and waypoints for Starbase ships. It is not meant to replicate or replace ISAN, which is a much more comprehensive system and you should probably just use that. ISAN is better than SkyScan in almost every way. In fact, [here's a link to that](https://github.com/Collective-SB/ISAN) because that's probably what you want instead. 

## Features
- 3-point coordinate location system ✅
- Save up to two locations in memory for reference ✅
- Velocity! ✅

## Comparison to ISAN

SkyScan was developed from scratch as a kind of personal challenge that turned out better than expected, so I have decided to publish the code. All code for this system was developed independently of ISAN, and any similarities are purely coincidental.

Skyscan uses a calculation method called ["True Range Multilateration"](https://en.wikipedia.org/wiki/True-range_multilateration) to triangulate a ship's position, assiging `origin_gate` as `(0,0,0)` rather than inventing an imaginary origin point and axes. This is essentially how the GPS in your phone works. 

Because of this, **Skyscan's coordinate system is different than ISAN**, though it's entirely possible to convert Skyscan coordinates to ISAN-compatible ones with a translate and rotate function. Please feel free to contribute code if you find an easy way to do this. 
<figure>
    <img src="img/Skyscan-vs-ISAN-axes.png" width=800></img>
    <figcaption><small>SkyScan coordinate system (dashed and colored lines) relative to ISAN coordinates.</small></figcaption>
</figure><br><br>

- While functionally similar to ISAN, SkyScan was developed to be modular and simple. 
- Skyscan is more of a personal waypoint system, but it can be used as an alternative to ISAN if desired. 
    - Since [**Skyscan uses the transmitters as the coordinate axes**](img/Skyscan-vs-ISAN-axes.png), it _greatly_ simplifies the position calculation - SkyScan can run in just 7 lines of YOLOL, and the Velocity plugin is [just 4 lines](Velocity/skyscan-velocity.yolol)!
- Skyscan is not as feature-rich and does not have a companion website like https://isan.to, which is a wonderful community resource. 


## Limitations
- Slow-ish, ~2 second refresh delay
- Only works up to 1000KM away from Origins
- Requires at least one Advanced YOLOL Chip (two if using the Velocity plugin)
- Requires 3 Navigation Receivers
- Skyscan is not scalable. In fact it may actually be possible to have a single coordinate refer to two different points in space (though it is unlikely you will encounter these points)
- No one's checked my math, yet.
- Ongoing support and updates of this system is limited* <br><small>*The author has a full-time job, a newborn baby, and is finishing graduate certificate courses. What little free time is left will probably be spent actually trying to playing the game.</small>

## Installation
(Steps can be perfomed in any order)

### 1. Install controls and display:
!["Skyscan console controls"](img/console-controls.png)
- Add a Hybrid Button with 1st device field set to `SkyScan`
    - `ButtonStyle : 1`
- Add a Hybrid Button with 1st device field set to `LocMark`
    - `ButtonStyle : 1`
- Add a Text Panel with 1st device field `Location`
- Add a text panel with 1st device field `Velocity`
- Add a text panel with 1st device field `SavedLoc1`
- Add a text panel with 1st device field `SavedLoc2`

### 2. Install and connect YOLOL Device Racks according to the following recommended configuration:
!["Skyscan YOLOL chip devices"](img/YOLOL-chips-config.png)
- [skyscan.yolol](/skyscan.yolol) on an Advanced YOLOL Chip
- [skyscan-velocity.yolol](Velocity/skyscan-velocity.yolol) on an Advanced YOLOL Chip
    - Provides speed and velocity information to panels
- [skyscan-locmark.yolol](LocationMark/skyscan-locmark.yolol) on a Basic YOLOL Chip
    - Save up to two locations in long-term memory.
- A blank YOLOL Memory Chip with the default device field names (`ChipField1`, `ChipField2`, etc)

### 3. Install Navigation Receivers
!["Receiver Config"](img/receiver-config.png)
- Place 3 small or regular Navigation Recievers on hardpoints or turntables. Set up each Nav Receiver device fields as follows:
    - Nav Receiver 1
        - Replace `Message` device field name with `nsig`  
        - Replace `SignalStrength` field name with `nss`
        - Set `ListenAngle` value to `180`
        - Set `TargetMessage` value to `"origin_north"`
    - Nav Receiver 2
        - Replace `Message` device field name with `gsig`  
        - Replace `SignalStrength` field name with `gss`
        - Set `ListenAngle` value to `180`
        - Set `TargetMessage` value to `"origin_gate"`
    - Nav Receiver 3
        - Replace `Message` device field name with `wsig`  
        - Replace `SignalStrength` field name with `wss`
        - Set `ListenAngle` value to `180`
        - Set `TargetMessage` value to `"origin_west"`

<small>Note: if nav receivers aren't working correctly after first installing, you may need to restart your game.</small>

## Operation
Press the `SKYSCAN` button to turn on scanning and location. Your `Location` display will show your X,Y and Z coordinates. The `Velocity` display shows your velocity in each coordinate direction and overall speed. Negative values indicate you are traveling toward the `origin_gate` station.

Press `SKYSCAN` again to turn off and/or reset.

Press `LOCMARK` button to save a location to longer-term memory. A blinking caret (`^`) indicates which memory slot will be written to next.