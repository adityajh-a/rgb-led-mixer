### [download project report pdf!](https://github.com/adityajh-a/rgb-led-mixer/blob/main/RGB%20LED%20Color%20Mixer%20using%20Arduino.pdf)

# RGB LED Controller with Button Toggle and Potentiometers

This Arduino project lets you control an RGB LED using three potentiometers (for red, green, and blue brightness) and a single push-button that toggles the LED on or off. It demonstrates the use of PWM, analog inputs, and simple state-based button logic.

---

## 🔧 Hardware Components

- Arduino Uno (or compatible board)
- Common cathode RGB LED
- 3 × 10kΩ Potentiometers
- 3 × 220Ω Resistors (for RGB pins)
- 1 × Push Button
- 1 × 10kΩ Resistor (pull-down for button)
- Breadboard and jumper wires

---

## 🔌 Pin Connections

| Component       | Arduino Pin |
|----------------|-------------|
| Red LED        | D11         |
| Green LED      | D10         |
| Blue LED       | D9          |
| Red Pot        | A0          |
| Green Pot      | A1          |
| Blue Pot       | A2          |
| Button         | D12         |

*Note: Use PWM-capable pins for LED (D9, D10, D11 on Uno).*

---

## 🧠 How It Works

- Each potentiometer controls one color channel (R, G, B) by mapping analog input (0–1023) to PWM output (0–255).
- The push-button toggles the LED output ON or OFF using edge-detection logic.
- The LED color updates in real-time only when the state is ON.

---

## 🧾 Arduino Code

```cpp
int blue = 9;
int green = 10;
int red = 11;

int redPot = A0;
int greenPot = A1;
int bluePot = A2;

const int BUTTON = 12;
int state = 0;
int val = 0;
int old_val = 0;

void setup() {
  pinMode(red, OUTPUT);
  pinMode(green, OUTPUT);
  pinMode(blue, OUTPUT);
  pinMode(BUTTON, INPUT);
}

void loop() {
  val = digitalRead(BUTTON);
  
  if (val == HIGH && old_val == LOW) {
    state = 1 - state;
    delay(10);
  }

  old_val = val;

  int redVal = analogRead(redPot) / 4;
  int greenVal = analogRead(greenPot) / 4;
  int blueVal = analogRead(bluePot) / 4;

  if (state == 1) {
    analogWrite(red, redVal);
    analogWrite(green, greenVal);
    analogWrite(blue, blueVal);
  } else {
    analogWrite(red, 0);
    analogWrite(green, 0);
    analogWrite(blue, 0);
  }

  delay(50);
}
