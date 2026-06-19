# Obstacle-avoiding-robot
 A arduino project which avoids obstacles 
<img width="1536" height="1024" alt="5c757c0d-ca61-4d84-9ae2-d0d4e6bcea60" src="https://github.com/user-attachments/assets/942ca1ab-9df5-48ef-b203-0382f74442c8" />

the following code helps to test our motors 
[motor_test.ino.txt](https://github.com/user-attachments/files/29134791/motor_test.ino.txt)
/*
  L298N Motor Test - Arduino Uno
  ---------------------------------------------------
  Run this BEFORE uploading the full robot code, to confirm your
  wiring matches the pin layout used in the obstacle-avoidance and
  Bluetooth sketches.

  It runs each motor one at a time, forward then backward, with
  short pauses between each step and a message printed to the
  Serial Monitor (open it at 9600 baud) so you know exactly what
  the robot SHOULD be doing at each moment.

  Wiring (same as the other sketches):
    ENA -> D5   IN1 -> D6   IN2 -> D7    (left motor)
    ENB -> D10  IN3 -> D11  IN4 -> D12   (right motor)

  IMPORTANT: Place the robot on a stand or hold it up with the
  wheels off the table before running this, so it doesn't drive
  off the bench while you're testing.
*/

const int ENA = 5;   // Left motor speed (PWM)
const int IN1 = 6;   // Left motor direction
const int IN2 = 7;

const int ENB = 10;  // Right motor speed (PWM)
const int IN3 = 11;  // Right motor direction
const int IN4 = 12;

const int TEST_SPEED = 180;   // 0-255
const int RUN_TIME   = 1500;  // ms each direction runs
const int PAUSE_TIME = 1000;  // ms pause between steps

void setup() {
  pinMode(ENA, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(ENB, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);

  Serial.begin(9600);
  stopMotors();

  Serial.println("=== L298N Motor Test ===");
  Serial.println("Make sure wheels are off the ground!");
  delay(3000);
}

void loop() {
  Serial.println("\n--- LEFT MOTOR ---");

  Serial.println("Left motor FORWARD");
  leftMotor(TEST_SPEED, true);
  delay(RUN_TIME);
  stopMotors();
  delay(PAUSE_TIME);

  Serial.println("Left motor BACKWARD");
  leftMotor(TEST_SPEED, false);
  delay(RUN_TIME);
  stopMotors();
  delay(PAUSE_TIME);

  Serial.println("\n--- RIGHT MOTOR ---");

  Serial.println("Right motor FORWARD");
  rightMotor(TEST_SPEED, true);
  delay(RUN_TIME);
  stopMotors();
  delay(PAUSE_TIME);

  Serial.println("Right motor BACKWARD");
  rightMotor(TEST_SPEED, false);
  delay(RUN_TIME);
  stopMotors();
  delay(PAUSE_TIME);

  Serial.println("\n--- BOTH MOTORS (forward) ---");
  leftMotor(TEST_SPEED, true);
  rightMotor(TEST_SPEED, true);
  delay(RUN_TIME);
  stopMotors();

  Serial.println("\nCycle complete. Pausing 5s before repeating...");
  delay(5000);
}

// ---------- Helpers ----------
void leftMotor(int speed, bool forward) {
  digitalWrite(IN1, forward ? HIGH : LOW);
  digitalWrite(IN2, forward ? LOW : HIGH);
  analogWrite(ENA, speed);
}

void rightMotor(int speed, bool forward) {
  digitalWrite(IN3, forward ? HIGH : LOW);
  digitalWrite(IN4, forward ? LOW : HIGH);
  analogWrite(ENB, speed);
}

void stopMotors() {
  analogWrite(ENA, 0);
  analogWrite(ENB, 0);
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
}
------------------------------------------------------------------------------------------------------------------------------------------
