#define temperature A0
#define pinfan 9
#include <math.h>
#include <rgb_lcd.h>
#include<Wire.h>
#include "rgb_lcd.h"

const int B=4275;                 // B value of the thermistor
const int R0 = 100000;            // R0 = 100k
const int pinTempSensor = A0;     // Grove - Temperature Sensor connect to A0
 
rgb_lcd lcd;
const int colorR = 255;
const int colorG = 0;
const int colorB = 0;

void setup()
{
    Serial.begin(9600);
    lcd.begin(16, 2);
    pinMode(pinfan, OUTPUT);
    lcd.setRGB(colorR, colorG, colorB);
digitalWrite(pinfan, LOW);

}
 
void loop()
{
    double a = analogRead(pinTempSensor );
 
    float R = 1023.0/((float)a)-1.0;
    R = 100000.0*R;
 
    float temperature=1.0/(log(R/100000.0)/B+1/298.15)-273.15;//convert to temperature via datasheet ;

 lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Temperature:");
    lcd.print(temperature);
    Serial.println("Temperature");
    Serial.println(temperature);
    lcd.setRGB(255,0,255);
    delay(3000);
