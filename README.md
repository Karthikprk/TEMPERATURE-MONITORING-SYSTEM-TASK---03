# TEMPERATURE-MONITORING-SYSTEM-TASK---03
Temperature Monitoring System – Task 03 measures and displays temperature in real-time using a digital sensor. Readings are shown on an LCD or serial monitor, with optional alerts if thresholds are exceeded. Ideal for learning sensor interfacing, display output, and automation basics.

# TEMPERATURE-MONITORING-SYSTEM-TASK-03

This project is an embedded system application that measures and monitors temperature in real-time using a digital temperature sensor. The measured temperature is displayed on an LCD screen (or serial monitor) and can trigger alerts if the temperature exceeds a predefined threshold.  

---

##  Project Overview
- **Microcontroller:** Arduino Uno R3  
- **Sensor:** DHT11 / LM35 (replace based on your setup)  
- **Display:** I2C 16x2 LCD (or Serial Monitor)  
- **Alert Output (optional):** LED or Buzzer  
- **Simulation:** [View on Wokwi](https://wokwi.com/projects/437828008599742465)  

---

##  Components Used

| Component          | Quantity | Description                                |
|--------------------|----------|--------------------------------------------|
| Arduino Uno R3     | 1        | Main microcontroller board                 |
| DHT11 / LM35       | 1        | Temperature sensor                         |
| I2C LCD 16x2       | 1        | Displays temperature readings              |
| LED / Buzzer       | 1 (opt)  | Alert indication                           |
| Jumper Wires       | ~6       | For wiring                                 |
| Breadboard         | 1        | For circuit assembly                       |

---

##  Circuit Connections

### **Sensor (DHT11 Example):**
- **VCC** → 5V  
- **GND** → GND  
- **DATA** → Digital Pin D2  

### **I2C LCD:**
- **VCC** → 5V  
- **GND** → GND  
- **SDA** → A4  
- **SCL** → A5  

### **Alert LED (Optional):**
- **Anode (+)** → Digital Pin D8 (via 220Ω resistor)  
- **Cathode (-)** → GND  

---

##  Example Code (DHT11 with I2C LCD)
```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <DHT.h>

#define DHTPIN 2
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);

LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  lcd.init();
  lcd.backlight();
  dht.begin();
  lcd.setCursor(0, 0);
  lcd.print("Temp Monitor");
}

void loop() {
  float temp = dht.readTemperature();
  if (isnan(temp)) {
    lcd.setCursor(0, 1);
    lcd.print("Sensor Error  ");
    return;
  }
  lcd.setCursor(0, 1);
  lcd.print("Temp: ");
  lcd.print(temp);
  lcd.print(" C   ");
  delay(1000);
}
