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