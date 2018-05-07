# Coding Storybook

![Image of The Project](https://github.com/degokay/Coding-Storybook/blob/master/WeChat%20Image_20180507153744.jpg)

## Project Description
For more than a decade, education researchers, policymakers, and industry leaders have recognized the **importance of helping young people cultivate computational thinking, or the ability to use concepts from computer science to solve problems and understand the world in new ways (Wing, 2006)**. These concepts include how to _think algorithmically_, to _break down complex ideas into smaller parts_, or to _uncover issues or “bugs” in instructions_. 

While many technologies have emerged to **support youth in exploring computational concepts and practices**, opportunities in **early childhood are especially promising to cultivate interests early in computing as well as to support the development of social, emotional, and cognitive milestones (Bers, 2017)**. Many studies have shown that early interventions can have compounding effects later in life and influence personal and academic outcomes (Shonkoff, 2017), such as helping mitigate barriers to participation in computing. 

**Coding Storybook is a concept designed for young children around 5-7 to learn computational thinking through storytelling.** The system includes a **storybook** and **some electronics**, such as servos, and a set of physical coding blocks. The characters and scene objects in each story can be torn down and assembled into 3D animals with electronics, then children can use a virtual programming interface (mobile or web based programming application) create a block of code to control the motion of the paper robot according to the storyline. Combining coding and storytelling in this concept not only makes traditional storytelling more interactive, but also makes computing more appealing and fun to young children.

## Project Components
- A Storybook
- A Physical Structure and
- Coding Blocks to be used for the sets of Instructions

## Team Members
[Junnan Yu](https://github.com/Junnanyu)

[Siqi Feng](https://github.com/Siqi77feng)

[Babatunde Adegoke](https://github.com/degokay)



## Code
```Java
/*************************************************** 
  This is an example for our Adafruit 16-channel PWM & Servo driver
  Servo test - this will drive 8 servos, one after the other on the
  first 8 pins of the PCA9685
  Pick one up today in the adafruit shop!
  ------> http://www.adafruit.com/products/815
  
  These drivers use I2C to communicate, 2 pins are required to  
  interface.
  Adafruit invests time and resources providing this open source code, 
  please support Adafruit and open-source hardware by purchasing 
  products from Adafruit!
  Written by Limor Fried/Ladyada for Adafruit Industries.  
  BSD license, all text above must be included in any redistribution
 ****************************************************/
#include <Wire.h>
#include <Adafruit_PWMServoDriver.h>
// called this way, it uses the default address 0x40
Adafruit_PWMServoDriver pwm = Adafruit_PWMServoDriver();
// you can also call it with a different address you want
//Adafruit_PWMServoDriver pwm = Adafruit_PWMServoDriver(0x41);
// you can also call it with a different address and I2C interface
//Adafruit_PWMServoDriver pwm = Adafruit_PWMServoDriver(&Wire, 0x40);
// Depending on your servo make, the pulse width min and max may vary, you 
// want these to be as small/large as possible without hitting the hard stop
// for max range. You'll have to tweak them as necessary to match the servos you
// have!
#define SERVOMIN  150 // this is the 'minimum' pulse length count (out of 4096)
#define SERVOMAX  600 // this is the 'maximum' pulse length count (out of 4096)
// our servo # counter
uint8_t servoRight=0;
uint8_t servoLeft=1;
//uint8_t servo1=1;
char receivedChar;
boolean newData = false;
void setup() {
  Serial.begin(9600);
  Serial.println("Coding commands: \n(s)Start\n(f) Move forward\n(l) Turn left\n(r)Turn right\n(p)Stop\nPlease input s, f, l, r, or p to control the robot");
  pwm.begin();
  pwm.setPWMFreq(50);  // Analog servos run at ~60 Hz updates
  delay(10);
}
void recvOneChar() {
 if (Serial.available() > 0) {
 receivedChar = Serial.read();
 newData = true;
 }
}
void start()
{
  pwm.setPWM(servoRight, 0,303);
  pwm.setPWM(servoLeft, 0, 280);
}
void moveForward()
{
  pwm.setPWM(servoRight, 0, 305);
  pwm.setPWM(servoLeft, 0, 279);
}
void moveLeft()
{
  pwm.setPWM(servoRight, 0, 310);
  pwm.setPWM(servoLeft, 0, 286);
}
void moveRight()
{
  pwm.setPWM(servoRight, 0, 300);
  pwm.setPWM(servoLeft, 0, 278);
}
void stopMove()
{
  pwm.setPWM(servoRight, 0,295);
  pwm.setPWM(servoLeft, 0, 295);
}
void showNewData() {
 if (newData == true) {
    
  if (receivedChar=='s'){
    Serial.println("\nYour command: Start");
    start();
    delay(1000);
    }
  if (receivedChar=='f'){
    Serial.println("\nYour command: Move forward");
    moveForward();
    delay(5000);
    }
  if (receivedChar=='l'){
    Serial.println("\nYour command: Turn left");
    moveLeft();
    delay(5000);
    }
  
  if (receivedChar=='r'){
    Serial.println("\nYour command: Turn Right");
    moveRight();
    delay(5000);
    }
  if (receivedChar=='p'){
    Serial.println("\nYour command: Stop");
    stopMove();
    }
 newData = false;
 }
 else stopMove();
 
}
void loop() {
  recvOneChar();
  showNewData();
}
```
## Resources
- TopCode Library: http://users.eecs.northwestern.edu/~mhorn/topcodes/
- Janson’s walking mechanism
- Laser Cutting Machine 




