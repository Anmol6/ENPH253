# ENPH253
<b>INSTALLATION</b>

1. Visual Studio with the Arduino extension must be installed first. 
2. In the default Arduino folder (../Documents/Arduino), install the TINAH library (http://projectlab.engphys.ubc.ca/wp-content/uploads/TINAH_DocumentsFolder.zip)
and replace some of the files in Arduino/libraries/TINAH with those in this repository (Modified TINAH Library).

<b> MENU SYSTEM </b>

Menu navigation is based on the two pushbuttons (start and stop) and two analog knobs on the TINAH. A short stopbutton press (~200ms) switches menus, short startbutton enables editing menu parameters, long startbutton (>1 second) saves menu parameters to EEPROM, and long stopbutton loads parameters from the EEPROM. 

Menu order is defined under switchMenu() in menu.cpp.

##Overview 

The robot uses an Arduino-based controller called TINAH, and is programmed mainly in C++ using Visual Studio with the Arduino extension. The software was modularized as much as possible; there were several different source and header files for components such as navigation, tape following, arm control (for pickup and dropoff), and multiplexing.

The TINAH has two buttons (‘stop’ and ‘start’) and two analog potentiometers that were used as input to the menu system, allowing for quick navigation between different parts of the software system for testing. The menu system consists of a loop function that continuously gets called by the main Arduino loop(), and it has a switch statement that chooses between different menu states represented by enumerations; each menu state then can run its own loop for time-sensitive functions such as tape following.

Using the menu system has saved our team a lot of time debugging; instead of going back to the code and modifying a few lines to change the behaviour of the robot (such as PID values, IR thresholds) before re-uploading, it can now be done swiftly from the TINAH.

For navigation, we have chosen to store the course as a undirected graph, with intersections as nodes and paths between nodes as edges. In conjunction with the IR, the robot makes decisions at intersections by scanning the far-range IR for passengers. If no IR is detected, each node also stores two preferred neighboring nodes to create a path the robot can navigate through; this path would route the robot through regions with the most passenger spaces for the maximum probability to find a passenger.

Overall the modular design made it easier to put all the components of the software together for the robot to function autonomously, and it also allowed for testing of individual parts of the software system.

### Authors

Anmol Jawandha (High-level navigation, arm control)

Henry Liu (Menu System, low-level testing)
