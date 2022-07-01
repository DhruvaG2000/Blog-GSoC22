---
layout: default
title: Project Documentation
parent: Documentation
nav_order: 5
---

# Arduino Core API module Documentation

This module provides an abstraction layer that enables Arduino IDE style C++ code to use underlying zephyr OS to program an Arduino BLE Sense 33. This project is still under development stage.

## Arduino Nano ble sense 33

The pinout for the arduino board that I am testing this project on is given below: ![](https://docs.arduino.cc/static/4c1da40b06b866435315963ef6bdf488/ABX00030-pinout.png)

The reason for choosing this board is that it is widely available and the chip Nordic nRF52x supports zephyr natively in their SDK.

## GPIOs
TODO: Documentation

## Serial
TODO: implement

## I2C

I2C implementation needed me to dive into the basics of the protocol itself. Here's the live demo of a stream of X Y Z Co-ordinates coming from the ADXL345 connected to the arduino over I2C.

![](/assets/images/transparent-LA_FullView1.png)

We can see that there are 2 wires required in I2C - _SDA_ and _SCL_. The _SDA_ line carries data and _SCL_ carries  the clock pulse.  To understand better, here's what was actually going on at a logic level:

![](/assets/images/LA_i2c_view1.png)

- `Wire.beginTransmission(0x53)` stores the address `0x53` in a local variable `_address`.
- `Wire.write(0x2C)` and `Wire.write(0x08)` append data to be written to the `txBuffer` inside the arduino.
- Finally, `Wire.endTransmission();` actually transfers the data (contents of `txBuffer`) over _i2c_ to the ADXL345.

- `Wire.requestFrom(0x53, 1)` takes in the `address` (here, 0x53), and `len` which is the length of bytes needed. Data is then read over _i2c_ from the ADXL345 and appended/ stored in a ring buffer. A Ring Buffer is a Circular Buffer in Zephyr and can be used for applications where a fixed size array doesn't suffice.

- `Wire.read()` finally returns the first element stored in the ringbuffer and pops it from there.  In the waveform below, we can see the response coming from ADXL as `0x03`.

![](/assets/images/LA_i2c_view2.png)


**ADXL345** 
Testing Done.