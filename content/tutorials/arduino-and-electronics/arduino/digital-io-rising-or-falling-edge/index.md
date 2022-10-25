---
title: "Digital Input: Falling or Rising Edge"
bookCollapseSection: false
p5js-widget: true
draft: false
weight: 102
---

# Digital Input: Falling or Rising Edge

---

In most cases, it’s not enough just to know if the signal changed. You often need to also know if your signal changed from on to off or vice versa.

The change from LOW to HIGH is called Rising Edge
The change from HIGH to LOW is called Falling Edge

The code below does the following:

- Read the state of a digital input pin
- Check if the state has changed from the previous loop
- Prints out a different result depending on if the signal went from LOW to HIGH or vice versa
- Turns the LED on if the input went from LOW to HIGH
- Turns the LED off if the input went from HIGH to LOW
- Keeps a count of how many times the button has been pressed
- Save the current state to a variable called prevBtnState for the next loop

```c
int btnPin = 2;
int ledPin = 9;
int btnState = false;
int prevBtnState = false;
int counter = 0;

void setup() {
  // Open the serial port
  Serial.begin(9600);
  // set the button pin to be an input
  pinMode(btnPin, INPUT);
  // set the LED pin to be an OUTPUT
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // read the button pin
  btnState = digitalRead(btnPin);

  // check if the button state has changed
  if(btnState != prevBtnState){
    // print the changed state
    Serial.print("Button state changed to: ");
    Serial.println(btnState);
    if(btnState == HIGH){
      Serial.println("Rising edge!");
      digitalWrite(ledPin, HIGH);
      // increase the counter
      counter++;
      Serial.print("Count: ");
      Serial.println(counter);
    }
    if(btnState == LOW){
      Serial.println("Falling edge!");
      digitalWrite(ledPin, LOW);
    }
  }

  // save the previous button state for the next loop
  prevBtnState = btnState;
}
```
