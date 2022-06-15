---
layout: default
title: Week 3
parent: Weekly Progress
nav_order: 5
---

# Week 3

(7th June - 13th June)

- Studied about the Zephyr GPIO API.
- Implemented ``setup()`` and ``loop()`` to execute according to the Arduino flow.
- Implemented ``pinMode()`` and ``digitalWrite()`` after having a basic idea of how blink LED works in zephyr. As of now these functions only work for te onboard LED.
- Tested the Blink LED arduino-style example on the nano ble sense 33.
- Started working on I2C implementation. Taking inspiration from Mbed OS, Started writing a ``Wire.h`` in the ``libraries`` folder. This aims to implement all the necessary functions needed for using I2C via the Arduino API. In future, there are hopes to add support for the ADS1115-driver (written for arduino-env) which communicates via I2C.
- Created place holder functions in Wire.h and tested that everything builds successfully so far.