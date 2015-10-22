#include <Servo.h>

// Sonic wave control
#define echoPin 7 // Echo Pin
#define trigPin 18 // Trigger Pin

Servo myservo; // Create servo object to control a servo
               // a maximum of eight servo objects can be created
int pos = 0;  // variable to store the servo position
long duration, distance; // Duration used to calculate distance
int servotime = 150;
void setup(){
  myservo.attach(29);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(115200);      // initialize serial communication
  pinMode(YELLOW_LED, OUTPUT);      // set the LED pin mode
}

void loop(){
  servoL();
  sleep(servotime);
  Serial.println(scan());
  servoF();
  sleep(servotime);
  Serial.println(scan());
  servoR();
  sleep(servotime);
  Serial.println(scan());
  servoF();
  sleep(servotime);
  Serial.println(scan());
}

void servoR(){
  myservo.write(47);
}
void servoL(){
  myservo.write(147);
}
void servoF(){
  myservo.write(97);
}

int scan(){
  /* The following trigPin/echoPin cycle is used to determine the
  distance of the nearest object by bouncing soundwaves off of it. */
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
 //Calculate the distance (in cm) based on the speed of sound.
  distance = duration/58.2;
  return distance;
}
