# STM32 Robotic Rover Controller

A custom STM32F446-based embedded controller designed for a robotic rover.

The board is intended to integrate motor control, wheel encoder feedback, servo control, sensor interfaces, power management, fault monitoring, and communication peripherals onto a single PCB.

## Project Goals

The controller is designed to support:

- Two brushed DC geared motors for differential-drive rover motion
- Quadrature encoders for closed-loop wheel speed and position control
- Four servo motor outputs
- Analog sensors such as infrared distance sensors
- UART-based sensors such as radar or ranging modules
- I2C and SPI sensor interfaces
- CAN communication for future expansion, including communication with a Raspberry Pi using a CAN adapter
- Motor-driver fault monitoring and software-controlled motor enable
- Onboard power regulation from a 12–18 V rover supply

The initial hardware demonstration will use **one 12 V N20 geared DC motor with an encoder**. The second motor channel remains available for future expansion. A dedicated external E-stop and limit switches are not part of this prototype design.

## Main Controller

- STM32F446RET6
- ARM Cortex-M4 MCU
- SWD programming and debugging using an external ST-LINK
- External 8 MHz crystal
- Reset and BOOT0 circuitry
- 3.3 V power indicator and MCU-controlled status LED

## Motor Control

The controller is designed to support two independently controlled brushed DC geared motors using a **DRV8848 dual H-bridge motor driver**.

The motor-driver circuit includes:

- Independent left and right motor control
- PWM speed control
- Bidirectional motor operation
- Current-sense / current-regulation circuitry
- `nSLEEP` control from the STM32
- `nFAULT` output connected to the STM32 for fault monitoring

Each motor connection combines the motor terminals, encoder power, ground, and quadrature encoder A/B signals into a **6-pin connector** intended for an N20 motor with a JST-ZH 1.5 mm interface. Final connector mating, pin orientation, and current ratings still need verification.

Wheel encoders connect to STM32 timer-capable inputs for hardware-assisted quadrature decoding and future PID speed control.

## Sensor and Peripheral Interfaces

The controller provides interfaces for:

- 4× analog sensor inputs
- 2× motor/encoder connections
- 4× servo PWM outputs with 5 V and GND pins
- I2C
- SPI
- UART
- CAN through a TCAN332 transceiver, with a CANH/CANL connector and selectable 120 Ω termination

These interfaces allow external sensors and modules to be connected without redesigning the main controller PCB. Servo power demand and peripheral compatibility will be reviewed before manufacturing.

## Power Architecture

The board is designed around a 12–18 V rover power input, with **12 V planned for the first bench demonstration**.

The input supply passes through a fuse and reverse-polarity protection stage, then is distributed between:

- Protected motor power for the DRV8848
- 5 V regulated peripherals and servo connectors using an LM2596 buck converter
- 3.3 V MCU and logic circuitry using an LM1117-3.3 LDO from the 5 V rail

The regulator component values, power budget, servo current demand, and thermal performance have not yet been fully calculated or verified.

## Current Development Status

The project has reached the **schematic review stage**. The planned functional blocks have been drawn in KiCad, but the electrical design has not yet been fully validated.

Schematic sections added include:

- Power regulation and reverse-polarity protection
- STM32 core circuitry and decoupling
- Clock, reset, and BOOT0
- SWD programming/debugging interface
- DRV8848 dual H-bridge, motor enable, and fault monitoring
- Two combined 6-pin motor and encoder connectors
- Four servo PWM connectors
- Four analog sensor connectors
- I2C, SPI, and UART interfaces
- CAN transceiver and selectable termination
- Power and programmable status LEDs

Remaining work:

- Full schematic and datasheet review
- Power, current-limit, and thermal calculations
- ERC (Electrical Rules Check) and correction of any errors
- Connector pinout and current-rating verification
- Footprint assignment
- PCB layout and DRC (Design Rules Check)
- PCB manufacturing, assembly, and hardware testing
- Firmware bring-up, motor PWM, encoder feedback, and PID speed-control demonstration

## Tools

- KiCad
- STM32CubeIDE / STM32CubeProgrammer
- ST-LINK / NUCLEO-F446RE for SWD programming
- Bench power supply, multimeter, and oscilloscope for testing
- Git / GitHub
