---
layout: default
title: Week 2
parent: Weekly Progress
nav_order: 4
---

# Week 2

(31st May - 7th June)

- Placed order for hardware - Arduino mkr zero and breadboard.
- Implemented ``delay()`` and ``delayus()`` and tested with a Hello world example.
- Finalised upstream repo - [gsoc-2022-arduino-core](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core).
- The Licensing Conundrum:
    - Mentor Jonathan had discussed with the Zephyr TSC community long before starting GSOC, the licensing and goals of this project. We officially had their approval to use the GPL license. 
    - Perhaps due to some misunderstandings a few TSC members on discord channel said that it doesn’t make much sense for them as a project to sponsor a GSOC project with an incompatible license.
    - To clear this confusion we emailed Aveek from TLF who adviced all to brainstorm and conclude to something that works best for all on our discord channel.
    - After much discussion, it was concluded that static linking LGPL code from Apache 2.0 software does not infect the whole Apache 2.0 codebase.
    - However, a few TSC members are still not completely comvinced and this matter will still be firther discussed in upcoming TSC meetings
- Much time was spent trying to figure a ``Serial.println()`` equivalent in zephyr, initially thought it was ``printk()``. Later I started digging for UART examples and found the "echo UART" example useful.
- The echo UART example also did not make the arduino show up in as a serial device on my laptop. Finally had to use a Logic Analyzer to probe it's physical UART pins to see that there was indeed UART output there.
How to get this UART output from the USB cable is something that needs to be taken care of in the device tree of the ``arduino nano ble 33`` is my guess.
- Deciding to narrow down on the external library written for Arduino for the ADS1115 (IIC) ADC. Will discuss with mentors in upcoming meetings.
- MoM with Jonathan on Monday, 6th June 2022:
    - I had hit a road block with the soburi repo and couldn't find where he had made his Serial instance and thus I can't figure how we can implement println. Decided to stop that hunt for now and instead of referring to soburi's structure, we will be now referring to mbed (https://github.com/arduino/ArduinoCore-mbed) more from now.
    - Decided that the first ever library/ driver to implement using my project would be the ADS1115 driver (https://github.com/Wh1teRabbitHU/ADS1115-Driver) which basically works over IIC protocol. Hence I will first and foremost need to implement Wire.h in zephyr.
    - Will document my understanding of how they have implemented Wire.h but using mbed functions and an mbedI2C class whose object Wire is being used everytime we need to do something over IIC in mbed. I will be doing similar to this in zephyr.
    
    Thus in summary, my first task in this coding period will be to implement this I2C using zephyr as a ``class zephyrI2C: public HardwareI2C``