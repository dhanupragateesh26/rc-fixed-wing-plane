# ESP32 ELRS Fixed Wing RC Plane

An ESP32-based flight control interface for a fixed-wing RC airplane using **ELRS (ExpressLRS) CRSF protocol**.

The ESP32 reads RC commands from an ELRS receiver via the CRSF protocol and directly drives control surfaces and ESC using PWM.

## Features

* ExpressLRS CRSF receiver support
* Direct servo control using ESP32 PWM
* ESC throttle control
* Arm/Disarm safety switch
* Failsafe when signal is lost
* Simple architecture for custom RC aircraft

## Hardware Used

* ESP32 Dev Board
* ExpressLRS Receiver
* 4x Servos / ESC
* Fixed Wing Airframe
* LiPo Battery
* BEC / Power module

## Channel Mapping

| Channel | Function         | Output  |
| ------- | ---------------- | ------- |
| CH1     | Aileron (Roll)   | Servo 1 |
| CH2     | Elevator (Pitch) | Servo 2 |
| CH3     | Throttle         | ESC     |
| CH4     | Rudder (Yaw)     | Servo 4 |
| CH5     | Arm Switch       | Safety  |

## Pin Mapping

| ESP32 Pin | Device         |
| --------- | -------------- |
| GPIO12    | Aileron Servo  |
| GPIO13    | Elevator Servo |
| GPIO14    | ESC (Throttle) |
| GPIO15    | Rudder Servo   |
| GPIO16    | ELRS RX        |
| GPIO17    | ELRS TX        |

## Safety System

The aircraft includes an **arming system**.

When:

* ELRS link is lost
* Arm switch is OFF

The system automatically:

* Cuts throttle
* Centers control surfaces

This prevents accidental motor spin.

## Firmware

Located in:

```
firmware/esp32_elrs_airplane.ino
```

Libraries required:

* ESP32Servo
* AlfredoCRSF

Install using Arduino Library Manager.

## Installation

1. Install Arduino IDE
2. Install ESP32 board package
3. Install required libraries
4. Upload firmware to ESP32
5. Connect ELRS receiver and servos
6. Power the system

## Wiring Diagram

See:

```
hardware/wiring_diagram.png
```

## System Overview

ESP32 receives CRSF packets from the ELRS receiver and converts them into PWM signals for servos and ESC.

```
Radio TX
   │
ELRS Receiver
   │ CRSF
ESP32 Controller
   │
Servos + ESC
   │
Control Surfaces
```

## Failsafe Behavior

When signal is lost:

* Throttle → 1000 µs
* Aileron → 1500 µs
* Elevator → 1500 µs
* Rudder → 1500 µs

## Future Improvements

* Flight stabilization (PID)
* Gyroscope integration
* Telemetry feedback
* Auto-pilot modes
* GPS navigation

## License

MIT License

## Author

Your Name
