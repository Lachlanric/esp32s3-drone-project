# ESP32 drone (quadcopter)

## Introduction

This repo contains a full suite of software/firmware to be able to program a quadcopter drone and an accompanying radio controller. Additionally an optional desktop client is available to tune PID parameters and visualise drone telemetry. The quadcopter and controller both run on ESP32 microcontrollers to be able to utilise the ESP-NOW radio protocol.

<img width="1733" height="426" alt="project-diagram" src="https://github.com/user-attachments/assets/83f901e9-6714-4d98-92b2-4c607c2490ae" />

## Cloning the repo and submodules

```bash
git clone https://github.com/Lachlanric/esp32s3-drone-project.git
cd ./esp32s3-drone-project
git submodule update --init
```

## Setting up VS Code environment

- Install ESP IDF - https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/index.html
- Install ESP IDF VS Code extension - https://marketplace.visualstudio.com/items?itemName=espressif.esp-idf-extension

## Building and flashing **drone-firmware**
- Open **drone-firmware** folder in VS Code
- Select ESP-IDF version, COM port, ESP32 target board
- Open SDK Configuration menager (menuconfig). Change the following settings:
  - Modify the parameters in Radio Configuration, MPU6050 Configuration and Motor Configuration to match your hardware
  - In Hardware settings > ESP PSRAM:
    - Enable "Support for external, SPI-connected RAM" (**SPIRAM**)
  - In Hardware settings > SPI RAM config:
    - Change “Mode of SPI RAM” (**SPIRAM_MODE**) to Octal
    - Set "Ram clock speed" (**SPIRAM_SPEED**) to 80MHz
  - In Camera configuration:
    - Disable support for all cameras except the one we are using (OV2640 2MP)
    - Set "I2C driver selection for SCCB" (**SCCB_HARDWARE_I2C_DRIVER_SELECTION**) to Legacy driver
    - Set "JPEG mode frame size option" (**CAMERA_JPEG_MODE_FRAME_SIZE_OPTION**) to Custom frame size
    - Set "Custom JPEG mode frame size (bytes)" (**CAMERA_JPEG_MODE_FRAME_SIZE**) to 8192.
- Build and flash the firmware

## Building and flashing **controller-firmware**
- Open **controller-firmware** folder in VS Code
- Select ESP-IDF version, COM port, ESP32 target board
- Open SDK Configuration menager (menuconfig). Modify the parameters in Radio Configuration, Serial Configuration and Joystick Configuration to match your hardware.
- Build and flash the firmware

## Running desktop client
Ensure you have Node.js installed
```bash
cd ./desktop-client
npm install
node ./index.js
```
Open a browser at `localhost:3000`