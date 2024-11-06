const int trig = 11;
const int echo = 10;
const int potPin = A4;  // Potentiometer connected to A4

const int greenLEDPin = 3;  // Green LED connected to pin 3
const int yellowLEDPin = 4; // Yellow LED connected to pin 4
const int redLEDPin = 5;    // Red LED connected to pin 5

long time;
int distance;

void setup() {
  pinMode(trig, OUTPUT);
  pinMode(echo, INPUT);
  pinMode(greenLEDPin, OUTPUT);
  pinMode(yellowLEDPin, OUTPUT);
  pinMode(redLEDPin, OUTPUT);
  
  Serial.begin(9600);
}

void loop() {
  // Read potentiometer value
  int potValue = analogRead(potPin);
  
  // Map potentiometer value to a range for adjusting distance thresholds (e.g., between 5 and 50)
  int rangeAdjustment = map(potValue, 0, 1023, -20, 20);
  
  // Adjusted thresholds based on potentiometer value
  int greenThreshold = 20 + rangeAdjustment;  // Default 20 cm, adjustable
  int yellowThresholdLower = 10 + rangeAdjustment;  // Default 10 cm, adjustable
  int yellowThresholdUpper = greenThreshold;  // Upper bound for yellow LED
  int redThreshold = yellowThresholdLower;  // Upper bound for red LED
  
  // Display threshold values for debugging
  Serial.print("Green LED Threshold: > ");
  Serial.println(greenThreshold);
  Serial.print("Yellow LED Threshold: ");
  Serial.print(yellowThresholdLower);
  Serial.print(" - ");
  Serial.println(yellowThresholdUpper);
  Serial.print("Red LED Threshold: < ");
  Serial.println(redThreshold);
  
  // Trigger the sensor with a 10-microsecond pulse
  digitalWrite(trig, LOW);
  delayMicroseconds(2);
  digitalWrite(trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(trig, LOW);
  
  // Measure the time for the echo
  time = pulseIn(echo, HIGH);
  
  // Calculate the distance in cm
  distance = time * 0.034 / 2;
  
  // Print the distance
  Serial.print("Distance: ");
  Serial.println(distance);
  
  // Control LEDs based on the distance and thresholds
  if (distance > greenThreshold) {
    // Green LED for distances greater than the green threshold
    digitalWrite(greenLEDPin, HIGH);
    digitalWrite(yellowLEDPin, LOW);
    digitalWrite(redLEDPin, LOW);
  } else if (distance > yellowThresholdLower && distance <= yellowThresholdUpper) {
    // Yellow LED for distances between yellow thresholds
    digitalWrite(greenLEDPin, LOW);
    digitalWrite(yellowLEDPin, HIGH);
    digitalWrite(redLEDPin, LOW);
  } else if (distance <= redThreshold) {
    // Red LED for distances less than or equal to red threshold
    digitalWrite(greenLEDPin, LOW);
    digitalWrite(yellowLEDPin, LOW);
    digitalWrite(redLEDPin, HIGH);
  }
  
  // Wait 1 second before the next reading
  delay(1000);
}
