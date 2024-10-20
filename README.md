# Current-Voltage-and-Power-Measurement-of-load

GOOGLE DRIVE VIDEO LINK:-
https://drive.google.com/file/d/1aIBvuy895vCPonfeRO-8kRLY6sMmDxkE/view?usp=drivesdk

ARDUINO UNO CODE:-

#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// Define LCD address and pins
LiquidCrystal_I2C lcd(0x27, 16, 2);

// Define current and voltage sensor pins
const int CURRENT_SENSOR_PIN = A0;
const int VOLTAGE_SENSOR_PIN = A1;

// Calibration factors
const float CURRENT_CALIBRATION_FACTOR = 0.185; 
const float VOLTAGE_CALIBRATION_FACTOR = 0.004887; 

void setup() {
  Wire.begin();
  lcd.init();
  lcd.backlight();
  lcd.clear();
  Serial.begin(9600);
}

void loop() {
  // Read current sensor value
  int currentRaw = analogRead(CURRENT_SENSOR_PIN);
  float current = (currentRaw * CURRENT_CALIBRATION_FACTOR) / 1000.0; 

  // Read voltage sensor value
  int voltageRaw = analogRead(VOLTAGE_SENSOR_PIN);
  float voltage = (voltageRaw * VOLTAGE_CALIBRATION_FACTOR); 

  // Calculate power
  float power = current * voltage; 

  // Display data on LCD
  lcd.setCursor(0, 0);
  lcd.print("Current: ");
  lcd.print(current, 2);
  lcd.print("A");

  lcd.setCursor(0, 1);
  lcd.print("V: ");
  lcd.print(voltage, 2);
  lcd.print(" V, P: ");
  lcd.print(power, 2);
  lcd.print("W");

  // Print data to serial monitor
  Serial.print("Current: ");
  Serial.print(current, 2);
  Serial.println("A");

  Serial.print("Voltage: ");
  Serial.print(voltage, 2);
  Serial.println("V");

  Serial.print("Power: ");
  Serial.print(power, 2);
  Serial.println("W");

  delay(1000); 
}
