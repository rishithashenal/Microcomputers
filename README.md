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

## **RESULTS**
<p align="justify">
It is operating as expected on the PCB. The code was written in a way that if the switches were to input something other than the updated truth table values provided, it would momentarily stop all activities until the input matched what was required once more. This is due to the possibility that a malfunction may be the cause in the real world, and it is typically not a good idea to operate during a malfunction. The PCB circuit that has been implemented successfully performs both the function and the duty that were described.
</p>

## **CODE**
```ruby
// PIC16F877A Configuration Bit Settings

// 'C' source line config statements

// CONFIG
#pragma config FOSC = HS        // Oscillator Selection bits (HS oscillator)
#pragma config WDTE = OFF       // Watchdog Timer Enable bit (WDT disabled)
#pragma config PWRTE = OFF      // Power-up Timer Enable bit (PWRT disabled)
#pragma config BOREN = OFF      // Brown-out Reset Enable bit (BOR disabled)
#pragma config LVP = OFF        // Low-Voltage (Single-Supply) In-Circuit Serial Programming Enable bit (RB3 is digital I/O, HV on MCLR must be used for programming)
#pragma config CPD = OFF        // Data EEPROM Memory Code Protection bit (Data EEPROM code protection off)
#pragma config WRT = OFF        // Flash Program Memory Write Enable bits (Write protection off; all program memory may be written to by EECON control)
#pragma config CP = OFF         // Flash Program Memory Code Protection bit (Code protection off)

// #pragma config statements should precede project file includes.
// Use project enums instead of #define for ON and OFF.
#define _XTAL_FREQ 20000000 

#include <xc.h>

void __interrupt() isr(void){  //ISR
    if(INTF==1){     //CHECK IF THE INTERRUPT IS ON
        INTF = 0;    //CLEAR THE INTERRUPT
        
        if(RB2==0 && RB1==0){
          //MOTOR 1 OFF
        RC0 = 0;   //IN1 LOW
        RC1 = 0;   //IN2 LOW
        
          //MOTOR 2 ON
        RC3 = 1;   //IN3 HIGH
        RC5 = 0;   //IN4 LOW
        __delay_ms(500);   //MOTOR 2 ON FOR 500ms
        RC3 = 0;   //IN3 LOW
        
        }
    }
}
      
void main(void){
    TRISB0 = 1;   //SENSOR 3
    TRISB1 = 1;   //SENSOR 2
    TRISB2 = 1;   //SENSOR 1
    
    TRISC0 = 0;   //IN1
    TRISC1 = 0;   //IN2
    TRISC3 = 0;   //IN3
    TRISC5 = 0;   //IN4
    INTF = 0;     //CLEAR THE INTERRUPT
    
    GIE = 1;    //ENABLE GLOBAL INTERRUPT BIT
    PEIE = 1;   //ENABLE THE PERIPHERAL INTERRUPT BIT
    INTE = 1;   //ENABLE RB0 AS EXTERNAL INTERRUPT BIT

    PORTC = 0X00;  //PORTC LOW
    while(1){
        RC0 = 0;   //IN1 LOW
          //MOTOR 2 OFF
        RC3 = 0;   //IN3 LOW
        RC5 = 0;   //IN4 LOW
        
        if(RB2==0 && RB1==1 && RB0==1){
              //MOTOR 1 ON
            RC1 = 1;   //IN2 HIGH
        }else if(RB2==0 && RB1==0 && RB0==1){
              //MOTOR 1 ON
            RC1 = 1;   //IN2 HIGH
        }else{
            RC0 = 0;   //IN1 LOW
            RC0 = 0;   //IN2 LOW
            RC3 = 0;   //IN3 LOW
            RC5 = 0;   //IN4 LOW
        }
    }
}
```
