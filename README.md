# servo-motor

A Servo Motor is a small device that has an output shaft. This shaft can be positioned to specific angular positions by sending the servo a coded signal. As long as the coded signal exists on the input line, the servo will maintain the angular position of the shaft. If the coded signal changes, the angular position of the shaft changes. In practice, servos are used in radio-controlled airplanes to position control surfaces like the elevators and rudders. They are also used in radio-controlled cars, puppets, and of course, robots.
Usually, they have a servo arm that can turn 180 degrees. Using the Arduino, we can tell a servo to go to a specified position and it will go there. 

We will need the following things:
An Arduino board connected to a computer via USB
A servo motor
Jumper wires


Step 1: How to Connect Them
A servo motor has everything built in: a motor, a feedback circuit, and most important, a motor driver. It just needs one power line, one ground, and one control pin.

Following are the steps to connect a servo motor to the Arduino:

The servo motor has a female connector with three pins. The darkest or even black one is usually the ground. Connect this to the Arduino GND.
Connect the power cable that in all standards should be red to 5V on the Arduino.
Connect the remaining line on the servo connector to a digital pin on the Arduino.

Step 2: Code

// Include the Servo library 
#include <Servo.h> 
// Declare the Servo pin 
int servoPin = 3; 
// Create a servo object 
Servo Servo1; 
void setup() { 
   // We need to attach the servo to the used pin number 
   Servo1.attach(servoPin); 
}
void loop(){ 
   // Make servo go to 0 degrees 
   Servo1.write(0); 
   delay(1000); 
   // Make servo go to 90 degrees 
   Servo1.write(90); 
   delay(1000); 
   // Make servo go to 180 degrees 
   Servo1.write(180); 
   delay(1000); 
}

Step 3: How It Works

Servos are clever devices. Using just one input pin, they receive the position from the Arduino and they go there.
Internally, they have a motor driver and a feedback circuit that makes sure that the servo arm reaches the desired position.
But what kind of signal do they receive on the input pin?
It is a square wave similar to PWM. Each cycle in the signal lasts for 20 milliseconds and for most of the time, the value is LOW. 
At the beginning of each cycle, the signal is HIGH for a time between 1 and 2 milliseconds.
At 1 millisecond it represents 0 degrees and at 2 milliseconds it represents 180 degrees.
In between, it represents the value from 0–180. This is a very good and reliable method. The graphic makes it a little easier to understand.

Remember that using the Servo library automatically disables PWM functionality on PWM pins 9 and 10 on the Arduino UNO and similar boards

How Do You Communicate the Angle at Which the Servo Should Turn?
The control wire is used to communicate the angle. The angle is determined by the duration of a pulse that is applied to the control wire. This is called Pulse Coded Modulation. The servo expects to see a pulse every 20 milliseconds (.02 seconds). The length of the pulse will determine how far the motor turns. A 1.5 millisecond pulse, for example, will make the motor turn to the 90-degree position (often called as the neutral position). If the pulse is shorter than 1.5 milliseconds, then the motor will turn the shaft closer to 0 degrees. If the pulse is longer than 1.5 milliseconds, the shaft turns closer to 180 degrees.


Code breakdown
The code simply declares the servo object and then initializes the servo by using the servo.attach() function. 
We shouldn't forget to include the servo library. In the loop(), we set the servo to 0 degrees, wait, then set it to 90, and later to 180 degrees.
