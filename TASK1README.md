# Arduino Temperature Monitoring System

## Project Overview

This project reads the temperature from a **DS18B20 digital temperature sensor** using an **Arduino UNO** and displays the current temperature on a **16x2 I2C LCD**. The temperature readings are also sent to the **Serial Monitor** for logging and debugging.


## Hardware Required

- Arduino UNO
- DS18B20 Temperature Sensor
- 16x2 I2C LCD
- Breadboard
- Jumper Wires


## Software Required

- Arduino IDE
- Wokwi Simulator
- DallasTemperature Library
- OneWire Library
- LiquidCrystal_I2C Library

---

## Wiring Diagram

| Component | Pin | Arduino UNO |
|----------|------|-------------|
| DS18B20 | VCC | 5V |
| DS18B20 | DATA | D2 |
| DS18B20 | GND | GND |
| LCD (I2C) | VCC | 5V |
| LCD (I2C) | GND | GND |
| LCD (I2C) | SDA | A4 |
| LCD (I2C) | SCL | A5 |

 **Note:** In Wokwi, the DS18B20 sensor already includes the required 4.7kΩ pull-up resistor internally.

---

## Circuit Diagram

```
                 Arduino UNO

              +-----------------+
              |                 |
        5V ---+-----------------+---- VCC (DS18B20)
              |                 |
       GND ---+-----------------+---- GND (DS18B20)
              |
        D2 ---+----------------------+ DATA (DS18B20)

        5V ---+----------------------+ VCC (LCD)
       GND ---+----------------------+ GND (LCD)
        A4 ---+----------------------+ SDA
        A5 ---+----------------------+ SCL
```
## Code
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <OneWire.h>
#include <DallasTemperature.h>

#define ONE_WIRE_BUS 2

OneWire oneWire(ONE_WIRE_BUS);
DallasTemperature sensors(&oneWire);

LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  Serial.begin(9600);

  sensors.begin();

  lcd.init();
  lcd.backlight();

  lcd.setCursor(0, 0);
  lcd.print("Temperature");
}

void loop() {

  sensors.requestTemperatures();

  float temp = sensors.getTempCByIndex(0);

  Serial.print("Temperature: ");
  Serial.print(temp);
  Serial.println(" C");

  lcd.setCursor(0, 1);
  lcd.print("                ");   // Clear line

  lcd.setCursor(0, 1);
  lcd.print(temp);
  lcd.print((char)223);
  lcd.print("C");

  delay(5000);
}


## Working Principle
1. The Arduino requests the current temperature from the DS18B20 sensor.
2. The sensor measures the temperature and sends the digital value to the Arduino through pin D2.
3. The Arduino displays the temperature on the 16x2 I2C LCD.
4. The same temperature value is printed on the Serial Monitor every second for monitoring and logging.



## Sample Output
### LCD

```
Temperature
25.50 °C
```

### Serial Monitor
```
Temperature: 25.50 °C
Temperature: 25.62 °C
Temperature: 25.75 °C
```

## Demostration
<img width="1910" height="912" alt="Screenshot 2026-07-26 181050" src="https://github.com/user-attachments/assets/82dab7c7-4148-4506-b667-6834da836e32" />


## Features
- Real-time temperature monitoring
- LCD display of current temperature
- Serial logging for debugging
- Easy to simulate using Wokwi
- Simple and beginner-friendly implementation

## Author
**NETHRAVATHI**
