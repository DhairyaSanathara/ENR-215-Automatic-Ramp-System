const int dirPin = 2;

const int pulsePin = 3;

// New configuration (Full Step mode)

const long pulsesPerRev = 200;   // Full step = 200 pulses for 1 rev

int pulseDelay = 12;             // Faster movement

char command = 'S';   // default STOP

void setup() {

  pinMode(dirPin, OUTPUT);
  
  pinMode(pulsePin, OUTPUT);

  Serial.begin(9600);
  
  Serial.println("Enter F = Forward, R = Reverse, S = Stop");

  digitalWrite(dirPin, LOW);  // default forward
  
}

void loop() {

  // Read Serial Input
  
  if (Serial.available() > 0) {
  
   command = Serial.read();
    
  command = toupper(command);
  
  }

  // ----- STOP -----
  
  if (command == 'S') {
  
  return;   // do nothing → motor stops
  
  }

  // ----- FORWARD -----
  
  if (command == 'F') {
  
  digitalWrite(dirPin, LOW);
  
  }

  // ----- REVERSE -----
  
  else if (command == 'R') {
  
  igitalWrite(dirPin, HIGH);
  
  }

  // ----- RUN MOTOR -----
  
  for (long i = 0; i < pulsesPerRev; i++) {
  

  // If stop pressed mid-motion
  
  if (command == 'S') break;

  digitalWrite(pulsePin, HIGH);
    
  delayMicroseconds(pulseDelay);
    
  digitalWrite(pulsePin, LOW);
    
  delayMicroseconds(pulseDelay);
    
  }
  
}

