# cODTECH-task2

NAME : LINGAM SREE KEERTHI


COMPANY : CODTECH IT SOLUTIONS


ID : CT04DF1246


DOMAIN : IOT


DURATION : ONE MONTH


MENTOR : NEELA SANTOSH


OVERVIEW OF THE PROJECT

Goal: Control multiple home devices (light, fan, etc.) using a mobile app or virtual switches.
Platform: Tinkercad Circuits (for simulation), Blynk (for real-world implementation).
Microcontroller: Arduino UNO (simulated in Tinkercad).
Communication: Simulated via Serial Monitor in Tinkercad / WiFi using NodeMCU in real hardware.


COMPONENTS USED:
1. Arduino UNO


2. LEDs (to represent appliances like light, fan, etc.)


3. Resistors (220Ω) for LEDs


4. Breadboard


5. Push buttons or serial input (for app simulation)

 
Key Benefits of This Prototype:

Scalable to more devices

Easily upgradable to use sensors (temperature, motion, etc.)

Works in simulation (Tinkercad) and hardware (BLYNK)



#code using tinkercad


int lightPin = 2;
int fanPin = 3;
int lockPin = 4;

void setup() {
  Serial.begin(9600);
  pinMode(lightPin, OUTPUT);
  pinMode(fanPin, OUTPUT);
  pinMode(lockPin, OUTPUT);
  Serial.println("Enter: light on/off, fan on/off, lock on/off");
}

void loop() {
  if (Serial.available()) {
    String command = Serial.readStringUntil('\n');
    command.trim();

    if (command == "light on") digitalWrite(lightPin, HIGH);
    else if (command == "light off") digitalWrite(lightPin, LOW);

    else if (command == "fan on") digitalWrite(fanPin, HIGH);
    else if (command == "fan off") digitalWrite(fanPin, LOW);

    else if (command == "lock on") digitalWrite(lockPin, HIGH);
    else if (command == "lock off") digitalWrite(lockPin, LOW);
  }
}


#code using blynk


#define BLYNK_TEMPLATE_ID "TMPLXXXX"
#define BLYNK_DEVICE_NAME "Home Automation"
#define BLYNK_AUTH_TOKEN "YourAuthToken"

#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

char auth[] = "YourAuthToken";
char ssid[] = "YourWiFi";
char pass[] = "YourPassword";

#define lightPin D2
#define fanPin D3
#define lockPin D4

void setup() {
  Blynk.begin(auth, ssid, pass);
  pinMode(lightPin, OUTPUT);
  pinMode(fanPin, OUTPUT);
  pinMode(lockPin, OUTPUT);
}

BLYNK_WRITE(V1) { digitalWrite(lightPin, param.asInt()); }
BLYNK_WRITE(V2) { digitalWrite(fanPin, param.asInt()); }
BLYNK_WRITE(V3) { digitalWrite(lockPin, param.asInt()); }

void loop() {
  Blynk.run();
}
