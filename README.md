# Microcomputers Lab 4

## **OBJECTIVE**
Design a modest water level control system for a water tank using interrupts and other PIC16F877A programming techniques.

## **INTRODUCTION**
<p align="justify">
This laboratory is an excellent illustration of how to use an external interrupt routine in a real setting. We have a water tank with three switches that detect water level. When the bottom switch is turned on, water fills and continues to fill even when the middle switch is turned on. When the third switch is turned on, however, the interrupt (RB0 external interrupt) is activated, removing water from the tank for 500 ms, or half a second. Our job was to design a PCB on which a PIC16F877A microcontroller could be mounted and signals sent to perform the stated action.
  </p>
