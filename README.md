# penplotter
Experiments using an old 3D printer as a pen plotter

2D Plotter from an Prusa Printer
===
## General modus operandi

* Use Prusa Slicer for gcode generation
* User SD Card or Pronterface (via USB) to transfer gcode
  * Pronterface offers 2 clicks to start solution
    

## Printer preperation

* Add plotter holder [https://www.printables.com/model/63385-pen-plotter-attachment-for-prusa-mk3s](https://www.printables.com/model/63385-pen-plotter-attachment-for-prusa-mk3s)
* lower PINDA Sensor to accomondate for the 10mm longer pen tip
* do a first layer calibration on the thick paper
    * issue: bed heats up to 50°C and warps your first paper
    * needs only to be done once

## Slicer Settings

### New Filament Profile
* Copy PLA Profile
* Change Temperature to something save (reduce burn risk) like
    * Nozzle: 40°C (above room temperature, if lower, printer will not start)
    * Bed: 20°C
* Set z hop to 2mm (Filament Overrides -> Lift height) - to prevent travel moves to be drawn

### new printer profile
* Move origin by x=45mm and y=30mm by setting the bed origin to that values (and reduce bed size accordingly) to account for the pen being at an offset
* Remove intro line (start gcode) as it sometimes collides with paper holder and is unneccessary anyway
* Removing of mesh bed leveling is not recommended

### new print settings
* Change Infil->Bottom Fill pattern to fill boxes and other shapes interestingly

## Workflow
* Slice gcode
* Save to disk
* Remove cap from pen (if not: homing will not work due to crash)
* Transfer to printer
    * via SD card
    * via Pronterface: Load gcode, click print
        * On main screen: Button "load file"
        * "Print"-Button to start the print
* Do Live-Z adjustments for perfekt line width from the printers menu. greatly improves visual apperience of the lines

## ToDo:
* Add a marlin pause command to prusa slicer, so you can adjust the pen or even add the pen right at the start of the plot for adjustment
* Do a calibration
    * With pronterface move loaded pen to lower left corner
        * Result: X:41.40 Y:39.10 
        * Create Printer Profile with Offset Bed Origin at X:-41.40 Y:-39.10 and place objects on grey bed area
    * Upper right corner X:255, Y=209 (obviously)
        
    * 
    * z: Moving PINDA probe so that a z=0 equals not touching the paper but 1mm above. Then adjust via live-z to z=-1mm the actual printing. That way bed leveling does not draw but actual drawing does
        * note: printer cannot move below z=0, so live-z have to do it

        
## Issues
* use first text marker, then fine line. the other way around, text marker smears
* beware of the offset of the different holders. A thinner pen has another y-coordinate than a thicker pen. this creates an offset on the paper
* mesh bed leveling should not draw, but an incorrect z of the pen holder can create unwanted lines. be extra carefull when inserting the pens
  * hack: pause a print and then insert the holder and tighten the screws adjust z height of the pen
* Slicing mode: close holes can help on filigrane details
* Printing on hight objects (e.g a tile of 7mm height)
    * bed leveling and PINDA will collide with tile, so 
        * render gcode with a z-offset of 8mm
        * start print, pause on first line after leveling
        * add tile
        * insert and adjust pen to correct heigt (which is 7mm higher than usual)
    * perfect bed leveling and repeatability, only fix tile after leveling
    * printing at 200% speed is also fine

## Links and further reading

[https://www.printables.com/model/63385-pen-plotter-attachment-for-prusa-mk3s/comments](https://www.printables.com/model/63385-pen-plotter-attachment-for-prusa-mk3s/comments) - especially [https://www.printables.com/make/557511](https://www.printables.com/make/557511)
[https://github.com/SonarSonic/DrawingBotV3](https://github.com/SonarSonic/DrawingBotV3)
[https://plotterfiles.com](https://plotterfiles.com)
[https://github.com/beardicus/awesome-plotters](https://github.com/beardicus/awesome-plotters)
