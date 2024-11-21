# temperature
hello this repository will help you to find the temperature

![image](https://github.com/user-attachments/assets/b98d311c-7152-4e3f-a919-4fe4e4f1e602)

![image](https://github.com/user-attachments/assets/e97281c1-5ebf-4a24-ad56-051c071fb3c2)

exemple:

#include <Arduino.h>
#include "Thermistor.h"

// Thermistor Configuration Parameters
// Define reference resistance for precise temperature calculation
const double Rref = 2000;     // Reference resistance in ohms
const double R0 = 2200;       // Resistance at 25°C in ohms
const double Beta = 3750;     // Beta coefficient for temperature sensitivity

// ADC (Analog-to-Digital Converter) Configuration
const unsigned samplingBits = 10;  // Resolution of analog reading (10-bit = 0-1023 range)
const int thermistorPin = A1;       // Analog input pin for thermistor readings

// Create a Thermistor object with predefined parameters
Thermistor thermistor(Rref, R0, Beta, samplingBits);

void setup() {
    // Initialize serial communication for data output
    Serial.begin(9600);  // Set baud rate to 9600 for data transmission

    // Configure thermistor pin as input for analog readings
    pinMode(thermistorPin, INPUT);
}

void loop() {
    // Read raw analog value from the thermistor
    // analogRead() converts voltage to a digital value (0-1023)
    int adcValue = analogRead(thermistorPin);

    // Convert ADC reading to temperature in Celsius
    // Uses predefined thermistor characteristics for accurate conversion
    double tempC = thermistor.getTemperature(adcValue, 'C');

    // Display measurement results on serial monitor
    Serial.print("ADC Value: ");
    Serial.println(adcValue);
    Serial.print("Temperature: ");
    Serial.print(tempC);
    Serial.println(" °C");

    // Pause between measurements to reduce processing load
    // Provides a 5-second interval between temperature readings
    delay(5000);
}
