

![https://ci.appveyor.com/api/projects/status/github/wheeler-microfluidics/SoftSpi?branch=master&svg=true](https://ci.appveyor.com/api/projects/status/github/wheeler-microfluidics/SoftSpi?branch=master&svg=true)
# ArduinoSoftSpi
Soft Spi output for the Arduino. This is useful for those trying to read from an sd card while trying to write an APA102 led strip on the Teensy 3.1. Other platforms are likely supported but haven't been verified with this codebase.

This solution addresses a major pain point for LED artists that are trying to run video from an SD card on a Teensy 3.1. This soft spi library is estimated to have 30 frame per second performance with 14 meters of 144 pixel density led strips.

The underlying library appears to support SPI input as well and this can easily be enabled by the developer. However it seems suspect that software spi input could work very well due to a lack of a hardware input buffer.

Usage:

    void spi_send(uint8_t data);

This library initializes on first run.

Recommended hardware/software stack.

    Recommended Hardware:
      Teensy 3.1
      Adafruit 5v Ready SD Card Breakout
      APA102 leds
    Recommended Software
      SdFat library

Example - paint one pixel violet:

      spi_send(0xff);  // control byte.
      spi_send(0x00);  // green
      spi_send(0xff);  // blue
      spi_send(0xff);  // red
      
      // Four zeros triggers color latch in the pixel.
      spi_send(0);
      spi_send(0);
      spi_send(0);
      spi_send(0);
