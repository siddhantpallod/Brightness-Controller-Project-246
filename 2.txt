const byte led_gpio = 18; // the PWM pin the LED is attached to
   // how many points to fade the LED by
#define POTENTIOMETER_PIN  15


// the setup routine runs once when you press reset:
void setup() {
  Serial.begin(9600);

  pinMode(POTENTIOMETER_PIN, INPUT);
  ledcAttachPin(led_gpio, 0); // assign a led pins to a channel

  // Initialize channels
  // channels 0-15, resolution 1-16 bits, freq limits depend on resolution
  // ledcSetup(uint8_t channel, uint32_t freq, uint8_t resolution_bits);
  ledcSetup(0, 4000, 8); // 12 kHz PWM, 8-bit resolution
}

// the loop routine runs over and over again forever:
void loop() {
  int analogValue = analogRead(POTENTIOMETER_PIN);
  int brightness = map(analogValue, 0, 4095, 0, 255);
  ledcWrite(0, brightness); // set the brightness of the LED
  // wait for 30 milliseconds to see the dimming effect
  Serial.println(brightness);
  delay(30);
}
