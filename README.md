#code forsimple traffic signalusing arduino


const int redLED = 5;
const int yellowLED = 4;
const int greenLED = 3;
const int button = 2;
bool pedestrianRequest = false;

void setup() {
    pinMode(redLED, OUTPUT);
    pinMode(yellowLED, OUTPUT);
    pinMode(greenLED, OUTPUT);
    pinMode(button, INPUT_PULLUP);  
    attachInterrupt(digitalPinToInterrupt(button), requestCrossing, FALLING);
}

void loop() {
    if (pedestrianRequest) {
        handlePedestrianCrossing();
        pedestrianRequest = false;
    } else {
        normalTrafficCycle();
    }
}

void normalTrafficCycle() {
    digitalWrite(greenLED, HIGH);
    for (int i = 0; i < 1500; i += 100) { 
        if (pedestrianRequest) {
            handlePedestrianCrossing();
            pedestrianRequest = false;
            return;
        }
        delay(400);
    }
    digitalWrite(greenLED, LOW);

    digitalWrite(yellowLED, HIGH);
    for (int i = 0; i < 1500; i += 100) { 
        if (pedestrianRequest) {
            handlePedestrianCrossing();
            pedestrianRequest = false;
            return;
        }
        delay(400);
    }
    digitalWrite(yellowLED, LOW);

    digitalWrite(redLED, HIGH);
    delay(1500);
    digitalWrite(redLED, LOW);
}

void handlePedestrianCrossing() {
    digitalWrite(greenLED, LOW);
    digitalWrite(yellowLED, LOW);
    digitalWrite(redLED, HIGH);
    delay(7000);
    digitalWrite(redLED, LOW);
}

void requestCrossing() {
    pedestrianRequest = true;
}


TINKERCAD LINK

https://www.tinkercad.com/things/ehSPeWAbRGD-traffic-light-circuit-124ei0012?sharecode=T7sj7eZNWDhkjL1r6IKxK4PdwEw3jL21mCaZ0izy-74
