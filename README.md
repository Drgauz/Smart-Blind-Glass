# Smart Blind Glass

## Overview
**Smart Blind Glass** is an IoT-based wearable device designed to assist visually impaired individuals by detecting obstacles at head level and providing real-time audio feedback.  
The system uses an **ultrasonic sensor**, **Arduino UNO**, and a **buzzer** to alert the user when obstacles are nearby.  
The buzzer’s pitch increases as the obstacle gets closer, enabling intuitive distance awareness.

---

## Features
- **Head-level obstacle detection** – Overcomes limitations of white canes.
- **Real-time audio feedback** – Dynamic buzzer pitch based on distance.
- **Compact & wearable** – Built into eyewear frames.
- **Low-cost & easy to assemble** – Uses affordable parts.
- **Battery-powered** – Portable for daily use.

---

## Hardware Requirements
- Arduino UNO R3
- Ultrasonic Sensor (HC-SR04)
- Passive Buzzer
- Jumper Wires
- 9V Battery with Connector
- Safety Glasses/Goggles frame

---

## Software Requirements
- [Arduino IDE](https://www.arduino.cc/en/software)
- C/C++ for Arduino
- [Tinkercad](https://www.tinkercad.com/) 
- [Draw.io](https://app.diagrams.net/) 

---

## Circuit Connections
**Ultrasonic Sensor (HC-SR04)**  
- VCC → Arduino 5V  
- GND → Arduino GND  
- Echo → Arduino Digital Pin 10  
- Trig → Arduino Digital Pin 9  

**Buzzer**  
- Positive (+) → Arduino Digital Pin 6  
- Negative (-) → Arduino GND  

**Power**  
- 9V Battery → Arduino VIN & GND  

---

## How It Works
1. The ultrasonic sensor sends sound waves to detect obstacles ahead.
2. The Arduino calculates the distance from the reflected signal.
3. If the distance is ≤ 100 cm, the buzzer turns on.
4. The pitch of the buzzer increases as the object gets closer.
5. When no obstacle is detected, the buzzer remains silent.

---

## Results
- Successfully detects **obstacles within 100 cm** at head level.
- Provides **instant audio feedback** with variable pitch.
- Comfortable, **lightweight design** integrated into eyewear.
- **Limitations**:
  - Cannot detect very thin or narrow objects.
  - Limited range due to single sensor.

---

## Future Enhancements
- **GPS Navigation** – Provide route guidance and caregiver tracking.
- **Voice Assistance** – Give spoken alerts and navigation instructions.
- **Weatherproofing** – For outdoor and all-weather use.
- **Multiple Sensors** – Improve detection accuracy for thin/narrow objects.
- **Solar Charging** – Sustainable and extended battery life.

---

## Authors
- **Dirghayu Pradhanang** – Team Leader / System Developer  
- **Pradip Joshi** – Tester / Coder  
- **Aashray Sangroula** – Diagram Designer  
- **Amit Kumar Tharu** – System Design / Integration  
- **Samriddhi Poudel** – Research & Documentation  
- **Shreyan Rimal** – Report Framework Development  

---

## Code
```cpp
const int trigPin = 9;
const int echoPin = 10;
const int buzzerPin = 6;

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance <= 100) {
    int freq = map(distance, 100, 5, 200, 2000);
    freq = constrain(freq, 200, 2000);
    tone(buzzerPin, freq);
    Serial.print("Tone Frequency: ");
    Serial.println(freq);
  } else {
    noTone(buzzerPin);
    Serial.println("Buzzer OFF");
  }
  delay(100);
}
