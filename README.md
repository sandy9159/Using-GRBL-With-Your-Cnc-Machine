# Using-GRBL-With-Your-Cnc-Machine

![TT](https://user-images.githubusercontent.com/19898602/143076616-c697ac57-f60c-4327-b7f9-8c4ed5b28d3d.gif)



This instructables will teach you how to install and adapt grbl to your cnc mill/laser cutter.
So first thing first, What is GRBL?

GRBL is a firmware for arduino boards(uno,nano,Duemillanove) that controls stepper motors and spindles/lasers. GRBL uses gcode as input and outputs signals via the arduino pins.
Most industrial cnc machines uses parallel port controller that requires Those big purple connectors. Because GRBL arduino boards you just hook it up to a free usb port.

If you already have your hardware you can skip directly to step 3!

# HARDWARE

![image](https://user-images.githubusercontent.com/19898602/143075369-841c0391-22a1-4347-a525-46f006695795.png)


Grbl is compatible with all atmega 328 based arduino boards, meaning that you could use a uno or a nano but not the mega as its atmega 2560 based. The arduino mega is used in alot of 3d printer because of its more powerful processor but because of the relatively easy tasks of a cnc mill the arduino uno is enough.

To drive stepper motors you need some sort of driver. Some popular choices are a4988 and drv8825 for small motors like nema 14 or 17, but should not be used with more powerful motors like nema23 and higher. Its a good idea to stay clear of the easy drivers.

To connect your motor drivers and arduino you can use a pre-made board like the popular arduino uno cnc shield or build your own. Building your own is pretty easy but can take alot of time. There are also arduino nano based boards made specially for laser cutting.

To summarize:
you will need these parts for a typical cnc machine:

1x arduino board
3x stepper drivers(x,y,z)
1x cnc shield


# INSTALLATION

![image](https://user-images.githubusercontent.com/19898602/143075511-1dd596cd-67fa-48ef-9fbf-ee5e0edf2a86.png)


To Install grbl you need two things:

Arduino IDE (download as .zip if you are on a school computer)
latest grbl release
Download the latest grbl sourcecode as .zip
If you dont have the arduino ide yet, download and install it
Open the grbl .zip and navigate to a folder simply called "grbl"
Extract the folder to a known place and open the arduino ide
In the arduino ide, navigate to sketch>include library> add .ZIP library
Navigate to the grbl folder and click ok.
Grbl is now installed as a arduino library. Navigate to file>example>grbl>grblupload.
A new sketch will open with instructions on how to flash grbl to your board.


# SETUP

![image](https://user-images.githubusercontent.com/19898602/143075681-4f91e070-e7d9-4dfb-9684-9dc58ab35dfa.png)


Now with firmware on your board you need to adapt grbl to your specific machine. To communicate with your board you need to open the arduino ide serial monitor. You should see a message like this "Grbl x.xj ['$' for help]" if you dont see the message, make sure that your are connected to the correct port and use the baudrate of 115200.

Type "$$" and a list of commands should appear, like this:

$100=250.000 (x, step/mm)
$101=250.000 (y, step/mm)
$102=3200.000 (z, step/mm)
$110=500.000 (x max rate, mm/min)
$111=500.000 (y max rate, mm/min)
$112=500.000 (z max rate, mm/min)
$120=10.000 (x accel, mm/sec^2)
$121=10.000 (y accel, mm/sec^2)
$122=10.000 (z accel, mm/sec^2)
$130=200.000 (x max travel, mm)
$131=200.000 (y max travel, mm)
$132=200.000 (z max travel, mm)

The most important part to change is the steps/mm. Steps/mm needs to be calculated and the easiest way of doing it is by using prusas reprap calulator.

To change a setting, type the identifier of the parameter (for example $100 for x steps) "=" and then the new value.
For example: typing $112=600 changes the z max rate to 600.
Make sure that your setting has been saved by typing $$ and checking the values.

Some settings (like corexy setup,variable spindle) needs to be changed trough the config.h. You find the config file in the arduino library folder for grbl. The file has instructions and should be pretty straight forward to edit. When you have edited the config file you need to reupload the sketch to your board.



Hopefully This instructables was helpful and your cnc machine is up and running!
If something is wrong/missing feel free to point it out in the comments.
