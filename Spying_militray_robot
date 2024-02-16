
#include <SoftwareSerial.h>                                                    //add the soft serial libray
SoftwareSerial Bluetooth(0, 1);  
int motorPin1 = 4;     // pin 2 on L293D IC
int motorPin2 = 5;     // pin 3 on L293D IC
int motorPin3 = 6;     // pin 4 on L293D IC
int motorPin4 = 7;     // pin 5 on L293D IC

char BT_input;     
int sensorpin = 10;
float sensorValue;  //Gas
int val;            //metal
int Buzzer = 9;     //Buzzer
int triggerPin = 12;
int echoPin = 11;
void setup() {
    Serial.begin(9600); 
    Bluetooth.begin(9600); 
    pinMode(triggerPin, OUTPUT);       // Sets the trigPin as an OUTPUT
    pinMode(echoPin, INPUT);          // Sets the echoPin as an INPUT
    pinMode(motorPin1, OUTPUT);
    pinMode(motorPin2, OUTPUT);
    pinMode(motorPin3, OUTPUT);
    pinMode(motorPin4, OUTPUT);
    digitalWrite(motorPin1,LOW) ;
    digitalWrite(motorPin2,LOW) ;
    digitalWrite(motorPin3,LOW) ;
    digitalWrite(motorPin4,LOW) ;
    pinMode(Buzzer,OUTPUT);     //Buzzer
    digitalWrite(Buzzer, LOW);
    pinMode (sensorpin,INPUT);  // Metal Sensor

}

void loop() {
    // Gas Sensor
    sensorValue = analogRead(A1); // read analog input pin 0
    Serial.print("MQ3 Sensor Value: ");
    Serial.println(sensorValue);
    if (sensorValue > 600)
    {
      Serial.println("Gas Detected");
      Serial.println("BITMAP TECHNOLOGY");
      tone(Buzzer,200);
      delay(500);
      noTone(Buzzer);
      delay(500);
      Bluetooth.println("Gas Detected");
      Bluetooth.print("BITMAP TECHNOLOGY");
     }
     // Metal Sensor
     val= digitalRead(sensorpin);
     Serial.print("Metal Detector ");
     Serial.println(val);
     if (val==1)
     { 
          Serial.println("Metal Detected");
          Serial.println("BITMAP TECHNOLOGY");
          tone(Buzzer,200);
          delay(500);
          noTone(Buzzer);
          delay(500);
          Bluetooth.print("Metal Detected");
          Bluetooth.print("BITMAP TECHNOLOGY");
          Bluetooth.print(sensorpin); // 
          Bluetooth.println();
      }
      //Ultrasonic
       long highPulseDuration;
       int calculatedDistanceCm;
    
       //Set the trigPin to low, before setting it to high for the pulse
       digitalWrite(triggerPin, LOW);
       delayMicroseconds(5);
    
       // Create the 10 seconds pulse on the trig pin
       digitalWrite(triggerPin, HIGH);
       delayMicroseconds(10);
    
       // Set the pin to low to end the pulse
       digitalWrite(triggerPin, LOW);
    
       // Read the duration of the high pulse on the echo pin
       highPulseDuration = pulseIn(echoPin, HIGH);
    
       // Calculating the distance
       calculatedDistanceCm = highPulseDuration * 0.034 / 2; // Speed of sound wave divided by 2 (go and back)
    
       // Displays the distance on the Serial Monitor
       Serial.print("Calculated Distance: ");
       Serial.print(calculatedDistanceCm);
       Serial.println(" cm");
    //   Bluetooth.print("Calculated Distance: ");
    //   Bluetooth.print(calculatedDistanceCm);
    //   Bluetooth.println(" cm");
        delay(1000);
    
       if ( calculatedDistanceCm < 30)
       {
          digitalWrite(12,HIGH);
          delay(1);//wait for 1ms
          digitalWrite(12,LOW);
          delay(1);//wait for 1ms
          digitalWrite(motorPin1, LOW);   
          digitalWrite(motorPin2, LOW);   
          digitalWrite(motorPin3, LOW);   
          digitalWrite(motorPin4, LOW);   
          Serial.println("Stop");
          Bluetooth.println("Stop");
          delay(1000);
        
       }
       // MOTOR CODE
  if (Bluetooth.available())
  {
   BT_input=Bluetooth.read();
   Serial.print("BT_input:");
   Serial.println(BT_input);
    if (BT_input=='1')
    {
      digitalWrite(motorPin1, HIGH); 
      digitalWrite(motorPin2, LOW); 
      digitalWrite(motorPin3, HIGH); 
      digitalWrite(motorPin4, LOW);
      Serial.println("Motors are rotating FORWARD");
      Bluetooth.println("Motors are rotating FORWARD");
     
    }
    if (BT_input=='2')
    {
       digitalWrite(motorPin1, LOW); 
      digitalWrite(motorPin2, HIGH); 
      digitalWrite(motorPin3, LOW); 
      digitalWrite(motorPin4, HIGH); 
      Serial.println("Motors are rotating BACKWORD");
      Bluetooth.println("Motors are rotating BACKWORD");
      
    }
   if (BT_input=='3')
    {
      digitalWrite(motorPin1, HIGH); 
      digitalWrite(motorPin2, LOW); 
      digitalWrite(motorPin3, LOW); 
      digitalWrite(motorPin4, LOW); 
      Serial.println("RIGHT");
       Bluetooth.println("RIGHT");
     
    }
    if (BT_input=='4')
    {
      digitalWrite(motorPin1, LOW); 
      digitalWrite(motorPin2, LOW); 
      digitalWrite(motorPin3, HIGH); 
      digitalWrite(motorPin4, LOW); 
      Serial.println("left");
       Bluetooth.println("left");
      
    }
    if (BT_input=='5')
    {
      digitalWrite(motorPin1, LOW);   
      digitalWrite(motorPin2, LOW);   
      digitalWrite(motorPin3, LOW);   
      digitalWrite(motorPin4, LOW);   
      Serial.println("Stop");
      Bluetooth.println("Stop");
     
    } 
  }
    

}
