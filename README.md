# Using ST7789 with ESP8266 on Arduino Framework

This guide is for using ST7789 TFT display with ESP8266 using Arduino Framework. This will also work on chips ESP32 and STM32 using Arduino Framework.

## Requirements

  * VSCode with PlatformIO extension or ArduinoIDE
  * Arduino framework for ESP8266
  * TFT_eSPI library

## Installation

  **PlatformIO:** https://docs.platformio.org/en/latest/integration/ide/pioide.html#

  **TFT_eSPI:** Download using PlatformIO Library Manager or download it from: https://github.com/maditnerd/st7789_bitmap

## Setup

You need to examine UserSetup.h in library folders to find out/change used pins. Pins are defined in UserSetup.h, line 149-150 as:

```c
  #define TFT_DC   PIN_D1  
  #define TFT_RST  PIN_D0
```
Communication pins vary according to the chip.

## Usage

Source code could be found in /src folder. Usage is extremely simple as:

```c
#include <TFT_eSPI.h>
#include "bitmap.h"
    
TFT_eSPI tft = TFT_eSPI();

void setup() {
  Serial.begin(115200);
  tft.begin();     
  tft.setSwapBytes(true);
  
  tft.pushImage(0,0,240,240,image);
}

void loop() {
}
```
Following line corrects ordering of bytes (endianness):
```c
tft.setSwapBytes(true);
```
This line pushes image to ST7789 driver. 'image' variable is located in 'bitmap.h' folder and contains image data.
```c
tft.pushImage(0,0,240,240,image);
```

## How to create proper image data

To do this, we will use LCD image converter.You can find it here : https://sourceforge.net/projects/lcd-image-converter/

* Resize your image to the size of your screen (240x240)
* Click on New Image
* Go to Image / Import and choose your image
* Go to Options / Conversion
* Choose Preset : Color R5G6B5
* Go to the Image Tab
* Change Block Size to 16bit
* Click on Show Preview
* Copy all the code
* Paste it inside the array

```c
const uint16_t mercy [] PROGMEM = {// --> PASTE HERE};
```

Proper image array looks like image variable in /src/bitmap.h folder.

# References
*This guide originates from: https://www.hackster.io/148468/display-images-on-a-st7789-screen-fbb0d7* click for more info.
