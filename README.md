Requriements:
  1.Pycharm
  2.Open CV module
  3.numpy module
  4.arduino ide
  5.arduino nano board
  6.servo motor-1
  7.bread board



Here arduino ide code for your reference:
CODE:
#include <Servo.h>
Servo doorLockServo; // Create servo object to control the door lock
int lockPosition = 0; // Initial position of the lock
void setup() {
doorLockServo.attach(9); // Attach the servo to pin 9
Serial.begin(9600); // Start serial communication
}
void loop() {
// Check for signal from Python code
if (Serial.available() > 0) {
char command = Serial.read(); // Read the incoming command
// If command is 'o', unlock the door
if (command == 'o') {
unlockDoor();
}
// If command is 'c', lock the door
else if (command == 'c') {
lockDoor();
}
}
}
void unlockDoor() {
// Rotate the servo to unlock the door
for (lockPosition = 0; lockPosition <= 90; lockPosition += 1) {
doorLockServo.write(lockPosition);
delay(15); // Delay to allow the servo to reach the desired position smoothly
}
}
void lockDoor() {
// Rotate the servo to lock the door
for (lockPosition = 90; lockPosition >= 0; lockPosition -= 1) {
doorLockServo.write(lockPosition);
delay(15); // Delay to allow the servo to reach the desired position smoothly
}
}
