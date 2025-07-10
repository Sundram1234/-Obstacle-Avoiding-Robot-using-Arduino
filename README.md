# 🤖 Obstacle Avoiding Robot using Arduino

This is an autonomous robot built using **Arduino UNO**, **Ultrasonic Sensor**, and **L293D Motor Driver**. The robot detects obstacles using the ultrasonic sensor and avoids them by changing direction — making it ideal for basic robotics and automation learning.

---

## 📦 Components Used

| Component              | Quantity |
|------------------------|----------|
| Arduino UNO            | 1        |
| Ultrasonic Sensor (HC-SR04) | 1 |
| L293D Motor Driver     | 1        |
| DC Motors + Wheels     | 2        |
| Robot Chassis          | 1        |
| Battery Pack (9V or Li-ion) | 1 |
| Jumper Wires           | As needed |

---

## ⚡ Circuit Diagram

![Obstacle Avoiding Robot Circuit](circuit.png)

> 📌 Make sure to connect ENA/ENB of L293D to 5V  
> Use external battery to power motors

---

## 🔌 Circuit Connections

### 🔷 Ultrasonic Sensor (HC-SR04):
- VCC → 5V  
- GND → GND  
- TRIG → D9  
- ECHO → D10  

### ⚙️ Motor Driver (L293D):
- IN1 → D2  
- IN2 → D3  
- IN3 → D4  
- IN4 → D5  
- ENA, ENB → 5V  
- VCC → Battery +  
- GND → Battery - and Arduino GND

---

## 💻 Arduino Code

<details>
<summary>Click to view code</summary>

```cpp
#define trigPin 9
#define echoPin 10
#define in1 2
#define in2 3
#define in3 4
#define in4 5

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  long duration, distance;
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.println(distance);

  if (distance < 15) {
    // Obstacle detected - turn
    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);
    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW);
    delay(500);
  } else {
    // Move forward
    digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);
    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW);
  }
}


👨‍💻 Created by
Sundram Savre
Electronics & Embedded Systems Enthusiast
📍 India
