---
layout: default
title: Week 5
parent: Weekly Progress
nav_order: 7
---

# Week 5

(21st June - 27th June)

- Had weekly meeting with Alvaro on June 21, 2022. We discussed the following:
    - Whether an ADS1115 driver exists in zephyr. a driver does exist for `adc_ads1x1x` which gave us hints on which functions to use where.
    - Alvaro made several comments on my i2c PR which will help me implement all the wrapper funcs.
    - Also discussed how printk works in zephyr and came to know why the print logs were displaying over the physical UART pins rather than USB. USB requires some special configuration and so for debugging I2C I will just make do with a logic analyzer to analyze the logs.
    - Alvaro will get back to me later on how to work on the Serial.println wrapper as I could not locate how they have done it in mbed.
- Add a GPIO press button to glow LED example in [PR#8](https://github.com/DhruvaG2000/Arduino-Core-Zephyr/pull/8)
- Studied the `MBed` as well as _Zephyr_ implementation of I2C, tried writing a few wrapper functions and tried compiling. Everything builds so far.
- Tested the [ADS1115 Driver](https://github.com/Wh1teRabbitHU/ADS1115-Driver) and there was no output on the Serial terminal (The arduino does not even show up) and there is no I2C activity when I checked with my logic analyzer as well. This might mean that the driver is outdated and also the fact that it is not very popular makes it non ideal to work further on.
- There exists an [official Adafruit ADS1115 driver](https://github.com/adafruit/Adafruit_ADS1X15) written in accordance with Arduino syntax which is more popular and supported. However this relies on another Arduino lib called `Adafruit_I2CDevice` which resides in [Adafruit_BusIO](https://github.com/adafruit/Adafruit_BusIO) which is a helper library to abstract away I2C & SPI transactions and registers. So this means I will have to go through `Adafruit_I2CDevice` source code and figure which functions it uses and write wrappers for it accordingly in my project's `Wire` library.
- Also started writing documentation for this project in Project Documentation section this week and will be updating it with all the wrapper functions and their supported features.