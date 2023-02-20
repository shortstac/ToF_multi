# ToF_multi
//arduino code for multiple VL53L0X time of flight sensors
//sensors 4-6 are not connected
#include "Adafruit_VL53L0X.h"
Adafruit_VL53L0X sensor1 = Adafruit_VL53L0X();
Adafruit_VL53L0X sensor2 = Adafruit_VL53L0X();
Adafruit_VL53L0X sensor3 = Adafruit_VL53L0X();
//Adafruit_VL53L0X sensor4 = Adafruit_VL53L0X();
//Adafruit_VL53L0X sensor5 = Adafruit_VL53L0X();
//Adafruit_VL53L0X sensor6 = Adafruit_VL53L0X();

void setup() {
    Serial.begin(2000000);
//    pinMode(9, OUTPUT);
//    pinMode(8, OUTPUT);
//    pinMode(7, OUTPUT);
    pinMode(6, OUTPUT);
    pinMode(5, OUTPUT);
    pinMode(4, OUTPUT);
//RESET ALL XSHUT PINS
        digitalWrite(4, LOW);
        digitalWrite(5, LOW);
        digitalWrite(6, LOW);
//        digitalWrite(7, LOW);
//        digitalWrite(8, LOW);
//        digitalWrite(9, LOW);
        delay(10);
        digitalWrite(4, HIGH);
        digitalWrite(5, HIGH);
        digitalWrite(6, HIGH);
//        digitalWrite(7, HIGH);
//        digitalWrite(8, HIGH);
//        digitalWrite(9, HIGH);
        digitalWrite(4, LOW);
        digitalWrite(5, LOW);
        digitalWrite(6, LOW);
//        digitalWrite(7, LOW);
//        digitalWrite(8, LOW);
//        digitalWrite(9, LOW);
//RESET COMPLETE
//SET ADDRESSES
      digitalWrite(4, HIGH);
        sensor1.begin(0x30);
      digitalWrite(5, HIGH);
        sensor2.begin(0x31);
      digitalWrite(6, HIGH);
        sensor3.begin(0x32);
/*      digitalWrite(7, HIGH);
        sensor4.begin(0x33);
      digitalWrite(8, HIGH);
        sensor5.begin(0x34);
      digitalWrite(9, HIGH);
        sensor6.begin(0x35); */
//START CONTINUOUS RANGING
  sensor1.startRangeContinuous();
  sensor2.startRangeContinuous();
  sensor3.startRangeContinuous();
//  sensor4.startRangeContinuous();
//  sensor5.startRangeContinuous();
//  sensor6.startRangeContinuous();
}


void loop() {
  int m[3][100];
  int t[3][100];
  //READING DATA
    for(int i=0;i<10;i++){
            if (sensor1.isRangeComplete()) {
              (m[0][i]=sensor1.readRange());
              (t[0][i]= millis());
            }
            else {
            (m[0][i]= 0);
            (t[0][i]= millis());
            }
    }
    for(int i=0;i<10;i++){
            if (sensor2.isRangeComplete()) {
              (m[0][i]=sensor2.readRange());
              (t[0][i]= millis());
            }
            else {
            (m[0][i]= 0);
            (t[0][i]= millis());
            }
    }
    for(int i=0;i<10;i++){
            if (sensor3.isRangeComplete()) {
              (m[0][i]=sensor3.readRange());
              (t[0][i]= millis());
            }
            else {
            (m[0][i]= 0);
            (t[0][i]= millis());
            }
    }
   /* for(int i=0;i<10;i++){
            if (sensor4.isRangeComplete()) {
              (m[0][i]=sensor4.readRange());
              (t[0][i]= millis());
            }
            else {
            (m[0][i]= 0);
            (t[0][i]= millis());
            }
    }
    for(int i=0;i<10;i++){
            if (sensor5.isRangeComplete()) {
              (m[0][i]=sensor5.readRange());
              (t[0][i]= millis());
            }
            else {
            (m[0][i]= 0);
            (t[0][i]= millis());
            }
    }
    for(int i=0;i<10;i++){
            if (sensor6.isRangeComplete()) {
              (m[0][i]=sensor6.readRange());
              (t[0][i]= millis());
            }
            else {
            (m[0][i]= 0);
            (t[0][i]= millis());
            }
    }
  */
  //PRINTING DATA
Serial.print("\n MEASUREMENTS: ");
   for(int i=0;i<3;i++){
        for(int j=0;j<10;j++){           
            Serial.print(m[i][j]);
            Serial.print(" ");
        }
        Serial.print("\n");     
    }

Serial.print("\n TIMES: ");              
    for(int i=0;i<3;i++){
        for(int j=0;j<10;j++){           
            Serial.print(t[i][j]);
            Serial.print(" ");
        }
        Serial.print("\n");     
    }
      Serial.print("\n");
      delayMicroseconds(1);  
}
