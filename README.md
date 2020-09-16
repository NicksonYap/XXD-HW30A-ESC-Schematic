# XXD HW30A 30A ESC Schematic

This schematic is obtained by reverse-engineering from the fabricated PCB.

### Schematic

Make sure this is the correct schematic you are looking for by referring to the attached PCB images below.

The schematic is only roughly verified.  
Please manually verify again.  
Feel free to open an issue/pull request if any mistake was found.  


![Reverse-engineered schematic of XXD HW30A 30A ESC](/images/schematic.png)


### Video Preview

It was intended for modifying the firmware on the HW30A as a brushless motor controller for a gimbal/robotic arm.

[![Reverse-engineered schematic of XXD HW30A 30A ESC](/images/video_thumbnail.png)](https://www.facebook.com/nicksonyap/posts/1440113766010972)

Code not available, it has been lost. Works as a test to spin the motors very slowly anyways

### Board images

![Front of XXD HW30A 30A ESC](/images/front_mosfets.jpg)


![Back of XXD HW30A 30A ESC](/images/back_driver.jpg)

### MOSFET switching performance

Using 2s battery (8.8V when unloaded), 700-900kv 2212 motor (no props)

High side rise time is about 16us (one of the MOSFET turns on in 192ns)  
High side fall time is about 470-550ns (one of the MOSFET turns off in 37ns)

Low side rise time is about 400-600ns  
Low side fall time is about 370-600ns

Low side gate charge and discharge peaks at arouind 74mA through 27ohm resistor

High side gate charge peaks at 9.2mA through 1.5kOhm resistor, discharge current not measured.


High side driver 6.4-8.2us turn on delay (one of MOSFET 2.2us)  
High side driver 2.5-2.8us turn off delay

Low side driver 100-130ns turn on delay  
Low side driver 140-188ns turn off delay

Based on the values above, the minimum deadtime to switch from:  
LOW to HIGH is 188ns+600ns = 788ns (can be lower since HIGH side turns on relatively slow)  
HIGH to LOW is 2.8us+550ns = 3.35us  
(driver delay + MOSFET delay)


### Flash and EEPROM dump

The flash and EEPROM memory obtained from XXD HW30A ESC can be found in the "memory dump" folder.  

Fuse defaults:  
LOW = 0x04  
HIGH = 0x9F  
Lock bits = 0x3F  

Based on http://www.engbedded.com/fusecalc:  
It uses internal RC Oscillator at 8MHz  
Brown-out level set at 4.0V  
SPI program downloading and watch-dog timer on.
