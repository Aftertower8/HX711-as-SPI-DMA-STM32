
# HX711 as SPI + DMA on STM32

An embedded systems project implementing non-blocking data acquisition from an HX711 24-bit ADC using SPI and DMA on an STM32 microcontroller.

Originally developed as a recruitment project for the KNR Rover Team Embedded Section, the project explores low-level peripheral configuration, efficient sensor data acquisition, and UART-based communication.

## Overview

The system reads measurements from a 1 kg load cell connected to an HX711 precision ADC. Instead of manually generating clock pulses using bit-banging, it leverages the STM32 SPI peripheral and DMA to acquire measurement data with minimal CPU intervention.

The firmware provides a serial interface for displaying measurements and supports taring through a keyboard command.

## Features

- **HX711 data acquisition** — reads 24-bit measurements from a load cell.
- **SPI + DMA** — hardware-assisted clock generation and data transfer without continuously polling the peripheral.
- **UART communication** — transmits measurement data to a serial terminal and accepts user input.
- **Tare functionality** — resets the measurement offset using the `t` key.
- **Embedded firmware** — peripheral configuration and application logic implemented using STM32 HAL.
- **Load cell support** — designed for measurements up to 1000 g, with a target resolution of 0.1 g.

## Hardware

| Component | Description |
|---|---|
| Microcontroller | STM32 Nucleo-F103RB |
| ADC / Amplifier | HX711 |
| Sensor | 1000 g load cell |
| Data acquisition | SPI + DMA |
| Serial interface | UART |

## How It Works

### 1. HX711 Data Acquisition

The HX711 amplifies the differential signal from the load cell and converts it into a digital measurement.

The microcontroller reads the resulting 24-bit signed value and processes it to obtain the measurement used by the application.

### 2. SPI and DMA

The HX711 does not implement a standard SPI interface. This project adapts the STM32 SPI peripheral to communicate with the device by using the MOSI signal to generate the clock pulses required by the HX711.

DMA (Direct Memory Access) transfers data between the peripheral and memory without requiring the CPU to handle every individual data transfer.

This approach reduces processor overhead and allows the firmware to perform other operations while acquisition is in progress.

### 3. UART Communication

UART provides a simple interface between the microcontroller and a computer.

The serial interface is used to:
- Display measurement results.
- Send commands to the firmware.
- Trigger the tare operation by entering `t`.

A serial terminal can be used to interact with the running application.

### 4. Tare Operation

Pressing `t` resets the measurement offset, allowing the system to establish a new zero reference.

Accurate weight measurements depend on proper calibration and the characteristics of the load cell.

## Getting Started

### Requirements

- STM32 Nucleo-F103RB development board
- HX711 module
- Compatible 1000 g load cell
- USB connection for programming and serial communication
- STM32CubeIDE
- Serial terminal application

### Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/Aftertower8/HX711-as-SPI-DMA-STM32.git
   ```

2. Open STM32CubeIDE.

3. Import the project into your workspace.

4. Build the firmware and flash it to the STM32 Nucleo-F103RB board.

5. Open a serial terminal connected to the board's configured UART interface.

6. Observe the measurement output and enter `t` to tare the scale.

Check the project configuration for the appropriate UART settings and peripheral pin assignments before running the firmware.

## Technologies

- C
- STM32 HAL
- STM32CubeIDE
- SPI
- DMA
- UART

## References

- [HX711 Datasheet](https://www.sparkfun.com/datasheets/Sensors/ForceFlex/hx711_english.pdf)
- [Reference implementation: HX711 with STM32 SPI + DMA](https://github.com/ufnalski/hx711_non_blocking_spi_g431kb)

## Project Context

This project was developed as part of the recruitment process for KNR (Student Robotics Research Club) at Warsaw University of Technology.
