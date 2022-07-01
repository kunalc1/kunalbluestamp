# Solar Panel Sun Tracker/Phone Charger
This project utilizes two photoresistors to measure light and more a servo motor accordingly to move a solar panel to the most optimal position. The energy can be taken from the solar panel to power any 5V devices.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Kunal C. | Mission San Jose | Software Engineering | Incoming Freshman

(https://bluestampengineering.com/wp-content/uploads/2016/05/improve.jpg)
  
# Final Milestone
My final milestone was finalizing the design. I included the solar panel and built the frame out of wood. My modification was the LCD screen which displays how much light went to each photoresistor. Some issues that I had were that I didn't have access to spring steel, so the motor wasn't able to move the solar panel without it. I substituted this part with a pipe cleaner, which is a cheaper and more available alternative. I also had trouble building the wooden frame, but I persevered and got it done in the end.

<iframe width="800" height="450" src="https://www.youtube.com/embed/ikWYol-akvw" title="Kunal C Milestone 3" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Second Milestone
My second milestone is that a servo motor will turn in the direction of the light. For this to work, I used the same photoresistors, but I also connected a servo motor to the Arduino which could take data through the analog pins. One issue that I had was that the motor wasn't turning even when I put light. To fix this, I changed when the motor would move to be more sensitive. This will be used in my final design to move the solar panel.

<iframe width="800" height="450" src="https://www.youtube.com/embed/hPz20W8WfWU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


# First Milestone
  

My first milestone was using my Arduino UNO to change the brightness of a LED light when there was less light. To achieve this, I used a photoresistor and some math to change the LED brightness. One problem that I had was that the photoresistor wasn't reading correctly, and I wasn't able to use it to change the LED. This milestone important because being able to change a value slightly depending on the light will be useful when moving the solar panel in the final design.

<iframe width="800" height="450" src="https://www.youtube.com/embed/s-QJcNgnrjE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


# Final Code

```
#include <Servo.h>
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>
Servo servo;   // Create a servo object to control the servo
LiquidCrystal_I2C lcd(0x27,16,2); //defines the size of the lcd
int eLDRPin = A0; // Assign pins to the LDR's
int wLDRPin = A1;
int eastLDR = 0; //Create variables to store to LDR readings
int westLDR = 0;
int difference = 0; //Create a variable to compare the two LDR's
int error = 10;  // Variable for is there is a noticable difference between the tow LDR's
int servoSet = 90; //Variable for position of servo - will be different for each device
void setup() {
 servo.attach(9);   //attaches the servo object to PWM pin 9
 Serial.begin(9600); 
 lcd.init();                      // initialize the lcd 
 lcd.init();
 // Print a message to the LCD.
 lcd.backlight();
}
void loop() {
 eastLDR = analogRead(eLDRPin); //Read the eastLDR value
 westLDR = analogRead(wLDRPin); //Read the westLDR value

 difference = eastLDR - westLDR ; //Check the difference 
 if (difference > 5) {
   if (servoSet <= 100) {
     servoSet ++;
     servo.write(servoSet);
   }
 } else if (difference < -3) { // the west panel is less sensitive, so I changed the value for the solar panel to go towards it to 3 instead of 5.
   if (servoSet >= 0) {
     servoSet --;
     servo.write(servoSet);
   }
 }
 lcd.setCursor(0,0);
 lcd.print("EastLDR: ");
 lcd.setCursor(9,0);
 lcd.print(eastLDR);
 if (eastLDR < 10){
  lcd.setCursor(10,0);
  lcd.print("  ");
 }
 lcd.setCursor(0,1);
 lcd.print("WestLDR: ");
 lcd.setCursor(9,1);
 lcd.print(westLDR);
 if (westLDR < 10){
  lcd.setCursor(10,1);
  lcd.print("  ");
 }
 Serial.print(eastLDR);      //Serial monitor can be useful for debugging/setting up
 Serial.print("   -   ");
 Serial.print(westLDR);
 Serial.print("   -   ");
 Serial.print(difference);   
 Serial.print("   -   ");
 Serial.print(servoSet);
 Serial.print("   -   ");
 Serial.println(".");
 delay(100);}
```
 
 # Total Cost
Circuits:
 - Arduino UNO: $20
 - Jumper Wires: $5
 - Breadboard: $4
 - Servo Motor: $5
 - Step Up Power Supply: $7
 - I2C LCD Display: $12
 - Solar Panel: $7
 - 9V battery: $3
 - USB A: $7
Frame:
 - Balsa Wood: $0.50
Other Equipment:
 - Hot Glue Gun: $15
 - Cutting Mat: $7
 - Protective Eyewear: $4
 - Hobby Knife: $5

**Total: $101.50**
