# STM32 Robotic Rover Controller

A custom STM32F446-based embedded controller designed for a robotic rover.

The board is intended to integrate motor control, wheel encoder feedback, servo control, sensor interfaces, power management, safety inputs, and communication peripherals onto a single PCB.

## Project Goals

The controller is designed to support:

- Two brushed DC geared motors for differential-drive rover motion
- Quadrature encoders for closed-loop wheel speed and position control
- Multiple servo motors
- Analog sensors such as infrared distance sensors
- Digital sensors and limit switches
- UART-based sensors such as radar or ranging modules
- I2C and SPI sensor interfaces
- CAN communication for future expansion
- Emergency-stop and fault monitoring
- Onboard power regulation from a 12–18 V rover supply

## Main Controller

- STM32F446RET6
- ARM Cortex-M4 MCU
- SWD programming and debugging
- External 8 MHz crystal
- Reset and BOOT0 circuitry
- Status indicators

## Motor Control

The rover uses two independently controlled brushed DC geared motors.

A DRV8848 dual H-bridge motor driver is being integrated to provide:

- Independent left and right motor control
- PWM speed control
- Bidirectional motor operation
- Current regulation
- Driver fault detection

Wheel encoders are connected to STM32 timer-capable inputs for hardware-assisted quadrature decoding and future closed-loop control.

## Sensor and Peripheral Interfaces

The controller provides interfaces for:

- 4× analog sensor inputs
- 2× quadrature encoders
- 4× servo PWM outputs
- I2C
- SPI
- UART
- CAN
- Digital limit / safety inputs

These interfaces allow external sensors and modules to be changed without redesigning the main controller PCB.

## Power Architecture

The board is designed around a 12–18 V rover power input.

The input supply is distributed between:

- Motor power
- 5 V regulated peripherals and servos
- 3.3 V MCU and logic circuitry

## Current Development Status

The project is currently in the schematic design stage.

Completed or allocated sections include:

- STM32 core circuitry
- Clock, reset, and BOOT0
- SWD debugging interface
- MCU decoupling
- Encoder pin allocation
- Servo PWM allocation
- Analog inputs
- I2C, SPI, UART, and CAN pin allocation
- Safety / limit inputs
- DRV8848 dual motor-driver selection

Motor-driver support circuitry, power distribution, connectors, protection circuitry, and PCB layout are still under development.

## Tools

- KiCad
- STM32
- Git / GitHub
