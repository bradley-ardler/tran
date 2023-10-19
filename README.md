const int thermalSensorPin = A0;  // Analog pin connected to the thermal sensor
const int signalPin = 2;        // Digital pin to which the signal is sent

void setup() {
  pinMode(signalPin, OUTPUT);
  Serial.begin(115200);
}

void loop() {
  // Read the analog value from the thermal sensor
  int sensorValue = analogRead(thermalSensorPin);

  // Convert the analog value to temperature (assuming linear relationship)
  float temperature = sensorValue * 0.48876;  // Adjust this scaling factor based on your sensor

  // Print the temperature to the serial monitor
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" Degrees Celsius");

  // Check if temperature crosses a threshold (adjust as needed)
  if (temperature > 26.3) {
    // Trigger the signal on pin 2
    digitalWrite(signalPin, HIGH);
    delay(1000);  // Keep the signal high for 1 second (adjust as needed)
    digitalWrite(signalPin, LOW);
  }

  delay(1000);  // Adjust the delay based on your desired reading frequency
}
