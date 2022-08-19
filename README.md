# Microcomputers Lab 4

## **OBJECTIVE**
Design a modest water level control system for a water tank using interrupts and other PIC16F877A programming techniques.

## **INTRODUCTION**
<p align="justify">
This laboratory is an excellent illustration of how to use an external interrupt routine in a real setting. We have a water tank with three switches that detect water level. When the bottom switch is turned on, water fills and continues to fill even when the middle switch is turned on. When the third switch is turned on, however, the interrupt (RB0 external interrupt) is activated, removing water from the tank for 500 ms, or half a second. Our job was to design a PCB on which a PIC16F877A microcontroller could be mounted and signals sent to perform the stated action.
</p>

## **OPERATIONAL DESIGN AND TRUTH TABLE**
<p align="center">
<img width="500" length="500" src="https://user-images.githubusercontent.com/111479144/185607815-fa3dd7d7-dfff-4c6f-961f-f438f919d109.png">
</p>
<p align="center">
<img width="500" length="500"src="https://user-images.githubusercontent.com/111479144/185607867-f41bef47-e0a9-48b1-aabb-b8b743ac689e.png">    
</p>

## **APPARATUS**
* 3 x IR Obstacle Avoidance Sensor
* Jumper Wires
* 2 x 220uF Capacitors 
* 16 Pin IC Base
* L293D Motor Driver IC
* 40 Pin IC Base
* 40x1 Male Header
* 2 x 220nf capacitors
* 2 x DC Motors(5V)
* 1 x 10k Resistor
* Breadboard
* Arduino UNO Board
* 20 MHz Crystal Oscillator

## **PCB DESIGN**
<p align="center">
<img width="400" length="400"src="https://user-images.githubusercontent.com/111479144/185615075-56db750d-a21e-4942-970b-506c32b15403.png">
</p>

## **IMPLEMENTATION**
<p align="center">
<img width="400" length="400"src="https://user-images.githubusercontent.com/111479144/185616019-f4a9f692-34b0-418b-8666-33c988f37d61.jpg">
</p>
