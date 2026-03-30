# Robotics-
#include <Servo.h>

Servo myServo;

int trigPin = 7; 
int echoPin = 6;

int greenLED = 5;
int orangeLED = 4;
int redLED = 3;

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  pinMode(greenLED, OUTPUT);
  pinMode(orangeLED, OUTPUT);
  pinMode(redLED, OUTPUT);

  myServo.attach(9);   // Servo signal pin
  Serial.begin(9600);
}

void loop() {
  // Send ultrasonic pulse
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Read echo
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  Serial.println(distance);

  // Distance conditions
  if (distance > 20) {
    digitalWrite(greenLED, HIGH);
    digitalWrite(orangeLED, LOW);
    digitalWrite(redLED, LOW);
    myServo.write(0);   // Closed
  }
  else if (distance > 10 && distance <= 20) {
    digitalWrite(greenLED, LOW);
    digitalWrite(orangeLED, HIGH);
    digitalWrite(redLED, LOW);
    myServo.write(90);  // Half open
  }
  else {
    digitalWrite(greenLED, LOW);
    digitalWrite(orangeLED, LOW);
    digitalWrite(redLED, HIGH);
    myServo.write(180); // Open
  }

  delay(500);
}
