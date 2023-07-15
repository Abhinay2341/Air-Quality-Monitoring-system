# Air Quality  Monitoring System
This is IOT based Air Pollution Monitoring System which measures indoor harmful gases present in air like Carbon Dioxide(CO2) using an MQ135 gas sensor and Carbon Monoxide(CO) using an MQ7 sensor. The device would be showing the air quality in PPM(Parts Per Million) on the LCD Display provided.

#components required
* Arduino uno R3
* 16*2 display
* mq135 gas sensor
* jumper wires
* Bread board
* I2C SP serial interface Module Port 

## Architecture
![arduino](https://github.com/Abhinay2341/Air-/assets/128236738/89cfb90e-5a61-4967-83d0-fc69ff095973)


## Software code


#include <LiquidCrystal.h>      //Header file for LCD
const int rs=12, en=11, d4=5, d5=4, d6=3, d7=2; //pins of LCD connected to Arduino
LiquidCrystal lcd(rs,en,d4,d5,d6,d7); //lcd function from LiquidCrystal

const int aqsensor = A0;  //output of mq135 connected to A0 pin of Arduino
int threshold = 250;      //Threshold level for Air Quality

void setup() {

  pinMode (aqsensor,INPUT); // MQ135 is connected as INPUT to arduino

  Serial.begin (9600);      //begin serial communication with baud rate of 9600

  lcd.clear();              // clear lcd
  lcd.begin (16,2);         // consider 16,2 lcd
}
void loop() {

  int ppm = analogRead(aqsensor); //read MQ135 analog outputs at A0 and store it in ppm

  Serial.print("Air Quality: ");  //print message in serail monitor
  Serial.println(ppm);            //print value of ppm in serial monitor

  lcd.setCursor(0,0);             // set cursor of lcd to 1st row and 1st column
  lcd.print("Air Qualit: ");      // print message on lcd
  lcd.print(ppm);                 // print value of MQ135

  if (ppm > threshold)            // check is ppm is greater than threshold or not
    {
      lcd.setCursor(1,1);         //jump here if ppm is greater than threshold
      lcd.print("AQ Level HIGH");
    }
  else
    {
      lcd.setCursor(1,1);
      lcd.print ("AQ Level Good");
      Serial.println("AQ Level Good");
    }  
  delay (500);
}


## Working
https://github.com/Abhinay2341/Air-/assets/128236738/e2577799-52bb-418e-9cb8-a0dc84e835fe



