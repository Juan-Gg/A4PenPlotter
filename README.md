# A4PenPlotter
A4 Pen Plotter

This is a pen plotter capable of printing on A4 paper sheets. It is intended to be similar to the Aritma Amagraph pen plotter, be as compact and robust as posible as well as reliable.
It is controlled by means of an arduino with a grbl shield, wich drives the x and y motors, and the solenoid used for lifting-lowering the pen in response to g-code generated in inkscape and sent through grbl controller. Scroll down for a gif of it working, bill of materials, instructions...

Whatch a video here: https://www.youtube.com/watch?v=bf3e0SFeA1A
https://youtu.be/e5mVlJlMX_E
More projects here: https://juangg-projects.blogspot.ca/

(This is also on Thingiverse: https://www.thingiverse.com/thing:2504587, here as a backup)


Materials
1) 3d printed parts (All files starting with "Print"):
Print one of each (ending in x1) or two (ending in x2). One needs to be mirrored as specified in its name.

2) Non 3d printed parts:
a)Metal profiles:
Stls included for dimensions. Material specified in their name.
In addition, two 6mm ID 30 mm long 0,5 mm thickness brass tubes are needed to act as
bearings between x carriage and the steel shafts.

b)Screws (and their nuts):
1 M4x20 mm
1 M4x40 mm
15 M3x12 mm
4 M3x30 mm
10 M2,5x8mm
8 2x10 wood screws
2 M4 wing nuts (optional)

c)Electronics:
1 Arduino UNO
1 arduino CNC shield (with drivers)
Mosfet circuit to drive the solenoid using the spindle pin(example included)
1 Enstop
1Power switch
1 Jack conector
1Red LED
1 470 Ohm resistor
Asorted wires
USB cable
A computer to generate and send the g-code to the plotter.

d) Actuators:
2 NEMA 17 x 35 mm stepper motors.
1 Spring loaded 12v solenoid (mine was from an old printer, use the one you have and glue
it in place.

e) Misc:
Paper rollers from an old printer (you can print them yourself)
Sand paper to glue on the 12mm alumninum tube to grip the paper
4 Ball bearings 4mmID 13mmOD 5mm thickness
Heatsrink tubing
Cable ties
6mm wide Belt and pulley
6 x 12 mm spring

And the compulsory one: Some free time.

Instructions
1) Mechanical assembly:
Follow the photographs, drawings, and the assembly reference step file, it should be pretty obvious where everything goes.
Some hints:

Captive nuts that hold everything toguether are located on the inside of the holes where the profiles go (there is an hexagonal slot in which they fit), insert them and engage the screw BEFORE putting the profile in.

The 12 mm OD aluminum tube is fixed to the motor shaft in one end and to an M4 screw on the other end by means of three M 2.5 x 8 mm screws in a triangle arrangement (see photo gallery), with the nuts inside, so they press on the shaft. This allows to center it precisely. If you find it too complicated, you can always use lots of tape, but that its not very professional, neither reliable.

X motor screw holes are a bit enlarged to adjust belt tension.

There is one spring in the moving carriage that presses the pen against tha paper. This spring is kept in place between two small circular slots. The solenoid spring must overcome this spring force in order to push the lever up.

Sandpaper is wraped in a spiral way around the 12 mm OD tube in order to grip the paper. You can glue this with contact glue or similar.
Don't hesitate to ask any questions, and sorry for not providing step-by-step guide with photographs. I am not able to do that at the moment.

2) Electrical assembly
I assume I don't have to provide an schematic for the main power switch and LED.

The tricky part is the solenoid driving circuit. While you can use the schematic provided with a P-chanel MOSFET, I encourage you to use an N-chanel MOSFET so you can get rid of the transistor. Look for schematics online.

I added an LED to check whether the solenoid is powered or not and some buttons (Pause, continue, reset, e-stop) These are not necesary for it to work, but they come in handy.
3) Loading and configuring grbl
Download grbl here: https://github.com/grbl/grbl
Configuration instructions: https://github.com/gnea/grbl/wiki/Grbl-v1.1-Configuration
Scroll down for the settings I used. (Steps per mm may vary in your machine, just print some squares and keep adjusting until you get it right)

4.1) G-code generation (Vector files)
Use this for lineal drawings, or with dxf, svg...files.

You can convert bitmaps to vector on inkscape on path > trace bitmap.

To generate g-code, I used inkscape and jtech photonics laser tool (https://jtechphotonics.com/?page_id=2012).

This plug in needs some modifications in order to work for our needs:

Go to C:\Program Files (x86)\Inkscape\share\extensions\laser.py, open it with your
favourite text edditor (I used notepad ++) and make sure the following three lines look like
in the photo below:


This will allow us to use custom g-code to turn the laser(in our case the solenoid) on and off.
Otherwise it will add laser power and more stuff. This way it worked for me.
I used the spindle enable pin on the cnc shield (m8 on, pen down, m9 off, pen up), but you can use the coolant pin as well.


4.2) G-code generation (Bitmaps)
Use this to print images like the submarine photo you can see above. Keep in mid that this will take much longer, depending on the resolution used.

For this, I used another plug-in for inkscape:
https://github.com/305engineering/Inkscape
This needs no modifications.
5) G-code sending
I used grbl controller (https://github.com/zapmaker/GrblHoming/releases)
This program will also let you configure grbl once it is loaded.
