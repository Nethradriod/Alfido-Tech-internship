## Motor Control with PWM & Obstacle Detection using Arduino Uno

## Project Overview

This project demonstrates PWM-based DC motor speed control integrated with obstacle detection using an Arduino Uno. An HC-SR04 ultrasonic sensor continuously measures the distance between the system and nearby objects. The measured distance is processed by the Arduino, which controls the DC motor through an L298N motor driver. When an obstacle is detected within a predefined threshold of **20 cm**, the Arduino immediately stops the motor by setting the PWM value to zero. Once the obstacle is removed, the motor automatically resumes operation at the predefined speed. This project illustrates the practical implementation of PWM motor control, ultrasonic sensing, and real-time embedded system decision-making.

---

## Project Simulation

> *(Insert your simulation screenshot here)*

---

## Hardware Components

- Arduino Uno
- L298N Motor Driver Module
- DC Motor
- HC-SR04 Ultrasonic Sensor
- External Power Supply (6–12V)
- Jumper Wires

---

## Circuit Connections

### Arduino Uno → L298N Motor Driver

| Arduino Pin | L298N Pin |
|-------------|-----------|
| D5 | ENA (PWM) |
| D6 | IN1 |
| D7 | IN2 |
| GND | GND |

### Arduino Uno → HC-SR04 Ultrasonic Sensor

| Arduino Pin | HC-SR04 Pin |
|-------------|-------------|
| D9 | TRIG |
| D10 | ECHO |
| 5V | VCC |
| GND | GND |

### L298N → DC Motor

- OUT1 → Motor Terminal 1
- OUT2 → Motor Terminal 2
- 12V → External Power Supply (+)
- GND → External Power Supply (−)

---

## Working Principle

The HC-SR04 ultrasonic sensor continuously measures the distance to nearby objects using ultrasonic waves. The Arduino calculates the distance from the sensor's echo pulse. If the detected distance is greater than **20 cm**, the Arduino sends a PWM signal (value 180) to the L298N motor driver, allowing the DC motor to rotate at a controlled speed. If an obstacle is detected within **20 cm**, the PWM signal is set to zero, causing the motor to stop immediately. Once the obstacle is removed, the motor resumes operation automatically.

---

## Arduino Code

```cpp
#define TRIG_PIN 9
#define ECHO_PIN 10

#define ENA 5
#define IN1 6
#define IN2 7

long duration;
int distance;

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);

  pinMode(ENA, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);

  Serial.begin(9600);
}

void loop() {

  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);

  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);

  digitalWrite(TRIG_PIN, LOW);

  duration = pulseIn(ECHO_PIN, HIGH);

  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance <= 20 && distance > 0) {
    analogWrite(ENA, 0);
    Serial.println("Obstacle Detected! Motor Stopped");
  }
  else {
    analogWrite(ENA, 180);
    Serial.println("Motor Running");
  }

  delay(200);
}
```



## Test Results

| Distance (cm) | Motor Status |
|---------------|--------------|
| 50 | Running |
| 35 | Running |
| 25 | Running |
| 20 | Stopped |
| 15 | Stopped |
| 10 | Stopped |
| 30 | Running |

## Demonstration
<img width="1917" height="1016" alt="Screenshot 2026-08-02 190359" src="https://github.com/user-attachments/assets/4da01ca4-a3d8-432a-8ba9-14e5d6293563" />




##  Conclusion

This project successfully demonstrates the integration of PWM-based motor speed control with ultrasonic obstacle detection using Arduino Uno. The system continuously monitors the surroundings and automatically stops the DC motor when an obstacle is detected within the predefined safety distance. The implementation showcases the use of embedded systems, sensor interfacing, motor control, and real-time automation, making it suitable for robotics, autonomous vehicles, and industrial safety applications.



**Author:** Nethravathi P


