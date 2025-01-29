
# SmartKnob Project

A **haptic feedback rotary knob** that uses a BLDC motor, a magnetic encoder, and a microcontroller to simulate dynamic resistance, detents, and end-stops. This repository contains the hardware schematics, firmware, and any software tooling needed to build a SmartKnob capable of providing programmable tactile feedback.

## Features

- **Brushless DC Motor (BLDC) Actuation**  
  Provides smooth, programmable torque for simulating detents, stops, and variable friction.
- **Magnetic Encoder**  
  High-resolution angle sensing ensures precise readings of knob position for responsive haptic effects.
- **Microcontroller-Based Control**  
  Real-time control loop to modulate motor torque based on the current knob position and configured haptic profile.
- **Configurable Haptic Profiles**  
  Switch between profiles like soft detents, hard stops, free spin, and others at runtime.
- **Integrated IMU (Optional)**  
  Measures orientation or additional movement data if advanced features are needed (e.g., inertia simulation).

## Hardware Overview

1. **Microcontroller**  
   - **ESP32-S3** (or your chosen MCU) running the main control loop, reading encoder data, and driving the motor driver via PWM signals.

2. **Motor Driver**  
   - **TMC6300** (or equivalent) controlling the 3-phase BLDC gimbal motor. Capable of precise torque modulation at low voltages.

3. **Magnetic Encoder**  
   - **AS5600** or similar to read the knob position.  
   - Offers contactless angle measurement with 12–14 bits of resolution.

4. **Motor**  
   - A gimbal-style BLDC motor (e.g., GB2208) for low cogging torque and smooth rotation.

5. **Power Supply**  
   - A 5V supply or battery pack, regulated down to 3.3V for the microcontroller.  
   - Make sure your motor driver supply is sized for peak current demands.

6. **Optional IMU**  
   - An MPU6050 or another IMU for advanced inertial-based haptic effects.

<!-- ## Firmware Structure

- **Encoder Reading**  
  Reads magnetic encoder via I2C/SPI to get current angle.  
- **Torque Control**  
  Uses PWM signals to drive the BLDC motor. Basic approach might be trapezoidal commutation or a custom approach; advanced setups can use FOC (Field-Oriented Control).  
- **Haptic Profiles**  
  Different modes (e.g., detents, end-stops, friction) defined in code. The firmware calculates desired torque based on the current angle and active profile.  
- **Main Loop**  
  Runs at a suitable update rate (e.g., 1–2 kHz) to read the angle, compute desired motor torque, and send PWM outputs to the motor driver.

<!-- ## Getting Started -->

<!-- 1. **Clone this repository**  
   ```bash
   git clone https://github.com/<your-username>/SmartKnob.git
   cd SmartKnob
   ```

2. **Hardware Assembly**  
   - Solder or assemble the PCB, including the motor driver, microcontroller, encoder, and any connectors.  
   - Mount the BLDC motor and magnet for the encoder so they align properly.

3. **Firmware Deployment**  
   - Open the firmware folder in your preferred IDE (e.g., PlatformIO, Arduino IDE).  
   - Adjust pin mappings in `config.h` for your specific wiring.  
   - Upload the firmware to your MCU.

4. **Configuration**  
   - In `config.h`, set motor parameters, encoder offsets, or other constants.  
   - If using an IMU, enable and configure it in `imu.h`.

5. **Testing**  
   - Power on the system and turn the knob.  
   - Observe motor feedback. If configured with a detent profile, you should feel discrete steps. --> 

## Usage

- **Change Haptic Mode**  
  By default, the firmware might start in free-spin. Use serial commands or a button (if implemented) to cycle through modes like detent, friction, or fixed end-stops.

- **Calibrate Encoder**  
  Ensure the knob is at a known reference angle if your system requires zero-position alignment. Some code might handle offset automatically.

- **Safety Notes**  
  - The motor driver can produce torque. Be cautious of pinch points.  
  - Avoid over-current situations by setting current limits if your driver supports it.

## Contributing

1. **Fork the repository** and create your branch from `main`.  
2. **Commit your changes** and push to your fork.  
3. **Open a Pull Request** detailing your modifications or improvements.

## License

This project is licensed under the [MIT License](LICENSE.md) — you are free to modify and distribute with attribution. See the LICENSE file for details.