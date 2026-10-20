## 🚒 Autonomous Fire Fighting Robot
An ESP32-based robotics project that uses flame sensors to detect the direction of a flame, controls a mobile robot with an L298N motor driver, and activates a water pump through a MOSFET driver. The firmware uses a state-machine approach to manage sensing, movement, extinguishing, and cooldown behavior.

## ✨ Features
- 🔥 Three-direction flame detection using left, center, and right sensors
- 🤖 Directional movement control using an ESP32 and L298N motor driver
- 💧 Pump control through a MOSFET driver
- 🧭 State-machine operation for searching, turning, extinguishing, and cooldown
- 🛡️ Safety timing with a startup delay, pump run-time limit, and cooldown period
- 📟 Serial monitoring for sensor readings, system state, and pump status
  
## 🧰 Hardware Requirements
- ESP32 DevKit / ESP32-WROOM-32 development board
- Three digital flame sensor modules with 3.3 V-safe outputs
- L298N motor driver
- Two DC geared motors and a robot chassis
- Water pump with a suitable MOSFET driver or relay module
- Suitable battery and voltage regulation
- Connecting wires and mounting hardware
  
Use components with compatible voltage and current ratings. The pump and motors must use an appropriate power supply and driver rather than being powered directly from ESP32 GPIO pins.

## 💻 Software Requirements
- Arduino IDE
- ESP32 board support package
- USB data cable
- Serial Monitor
The firmware is written in Arduino C++ and uses the Arduino core for ESP32.

## ⚙️ Working Principle
1. The three flame sensors monitor the left, center, and right directions.
2. The ESP32 samples sensor signals and applies a short debounce window to reduce brief signal fluctuations.
3. When a flame is detected on the left or right, the robot turns toward that direction.
4. When the center sensor detects a flame, the robot stops and activates the pump.
5. The pump switches off when the center flame signal clears or when the maximum pump run time is reached.
6. After a safety cooldown, the controller returns to its search state.
The sensor modules' output polarity may vary. The firmware currently treats a LOW sensor output as flame detected; adjust FLAME_DETECTED_LEVEL if your modules use active-HIGH outputs.

## 🔌 GPIO Pin Configuration
Function	ESP32 GPIO
Left flame sensor	32
Center flame sensor	33
Right flame sensor	35
Motor driver ENA	14
Motor driver IN1	18
Motor driver IN2	19
Motor driver IN3	25
Motor driver IN4	26
Motor driver ENB	27
Pump MOSFET control	23
Status LED	2


GPIO 35 is input-only and does not have an internal pull-up or pull-down resistor, so the connected sensor must provide a defined logic level.

## 🚀 Setup and Usage
1. Clone or download this repository.
2. Open src/autonomouus.ino in the Arduino IDE.
3. Install ESP32 board support if it is not already installed.
4. Select the correct ESP32 board and port.
5. Connect the sensors, motor driver, pump driver, and power supply according to the pin table and your verified circuit.
6. Review the sensor output polarity and confirm that the motor and pump drivers are suitable for the connected loads.
7. Upload the sketch to the ESP32.
8. Open the Serial Monitor at 115200 baud to view system status and sensor telemetry.
Before operating the assembled robot, test the motors and pump separately and keep the pump disabled during initial wiring checks.

## 🧠 Control States
- STARTUP_HOLD: Keeps motors and pump off during startup stabilization.
- SEARCHING: Checks sensor inputs and decides whether to turn or extinguish.
- TURNING_LEFT / TURNING_RIGHT: Turns toward a directional flame signal.
- EXTINGUISHING: Stops the motors and activates the pump.
- COOLDOWN: Keeps the pump off for a defined recovery period.
- SAFETY_FAULT: Safe fallback state that stops the motors and pump.
  
## 📂 Project Structure
Autonomous-Fire-Fighting-Robot/
├── README.md
├── src/
│   └── autonomouus.ino
└── docs/
    └── autonomous fire fighting robot.png
    
## 🔮 Future Improvements
- Add obstacle detection and avoidance.
- Calibrate sensor sensitivity for different environments.
- Add battery-level monitoring and low-voltage protection.
- Include more detailed wiring diagrams and test results.
- Add remote monitoring or alerts if required.
  
## ⚠️ Safety Notes
- Never connect motors or a water pump directly to ESP32 GPIO pins.
- Verify wiring, voltage levels, and current ratings before powering the circuit.
- Keep water away from batteries, exposed wiring, and the ESP32 board.
- Test in a controlled environment with supervision.
- This is an educational prototype, not a replacement for certified fire-safety equipment. Never rely on it to fight a real fire.
  
## 🤝 Contributing
Suggestions and improvements are welcome. When contributing, describe hardware changes clearly and include relevant wiring details or test results.

