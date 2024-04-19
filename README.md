# Sun-tracking-and-automatic-solar-pannel-position-adjustment-system-using-arduino
In this project i have made a automatic  solar pannel position adjustment system which adjust its position based on the sun movement to produce maximum electricity using ardrino and LDR sensor

Also, it moves through the dual axis. I used one servo motor and two LDR sensors for that.

component used
Arduino UNO board x 1 
Solar panel x 1 
SG90 servo motor x 1 
LDR sensor x 2 
10k resistor x 2 
Jumper wires 
Rigifoam / Foam board / Cardboard

ardrino code :-
/*Solar tracking system
   https://srituhobby.com
*/

//Include the servo motor library
#include <Servo.h>
//Define the LDR sensor pins
#define LDR1 A0
#define LDR2 A1
//Define the error value. You can change it as you like
#define error 10
//Starting point of the servo motor
int Spoint =  90;
//Create an object for the servo motor
Servo servo;

void setup() {
//Include servo motor PWM pin
  servo.attach(11);
//Set the starting point of the servo
  servo.write(Spoint);
  delay(1000);
}

void loop() {
//Get the LDR sensor value
  int ldr1 = analogRead(LDR1);
//Get the LDR sensor value
  int ldr2 = analogRead(LDR2);

//Get the difference of these values
  int value1 = abs(ldr1 - ldr2);
  int value2 = abs(ldr2 - ldr1);

//Check these values using a IF condition
  if ((value1 <= error) || (value2 <= error)) {

  } else {
    if (ldr1 > ldr2) {
      Spoint = --Spoint;
    }
    if (ldr1 < ldr2) {
      Spoint = ++Spoint;
    }
  }
//Write values on the servo motor
  servo.write(Spoint);
  delay(80);
}
