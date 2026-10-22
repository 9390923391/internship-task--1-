const int TEMP_PIN = A0;
const int LED_PIN = 8;
const float THRESHOLD_C = 30.0;

void setup() {
  Serial.begin(9600);
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  int adcValue = analogRead(TEMP_PIN);

  float voltage = adcValue * (5.0 / 1023.0);

  // Convert TMP36 voltage to temperature in Celsius
  float temperatureC = (voltage - 0.5) * 100.0;

  Serial.print("Temperature: ");
  Serial.print(temperatureC, 1);
  Serial.println(" C");

  if (temperatureC >= THRESHOLD_C) {
    digitalWrite(LED_PIN, HIGH);
    Serial.println("ALERT: Temperature threshold exceeded!");
  } else {
    digitalWrite(LED_PIN, LOW);
  }

  delay(1000);
}
