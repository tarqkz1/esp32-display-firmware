name: Build ESP32 Firmware

on:
  push:
    branches: [ "main" ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Setup Arduino CLI
      uses: arduino/setup-arduino-cli@v1

    - name: Install ESP32 Platform
      run: |
        arduino-cli config init
        arduino-cli config add board_manager.additional_urls https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
        arduino-cli core update-index
        arduino-cli core install esp32:esp32

    - name: Install Libraries
      run: |
        arduino-cli lib install "LVGL"
        arduino-cli lib install "GFX Library for Arduino"

    - name: Compile Sketch
      run: |
        arduino-cli compile --fqbn esp32:esp32:esp32s3 --output-dir ./build ./src

    - name: Upload Artifact
      uses: actions/upload-artifact@v3
      with:
        name: esp32-firmware
        path: ./build/*.bin
