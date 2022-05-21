
---
layout: default
title: Pre Selection
parent: Weekly Progress
nav_order: 2
---

# Pre Selection

A video conference was held with my mentors @Jonathan Beri and @alvaroviebrantz, where we discussed the following:


1. Arduino API (https://github.com/arduino/ArduinoCore-API)  would basically need to be included as a module in zephyr project, meaning that zephyr would essentially expand to support Arduino Style code.
2. Then we discussed the actual time length of this project as gsoc has 2 options this time, 

> Medium size projects should take about 175 hours to complete while large projects should take about 350 hours to complete

Since I may be having other commitments from July 15 onwards, I think it will be wise to plan this project in a 175 hour period. The essential and major outcomes were discussed as below,

 - Hardcode and figure out one board (most probably an ESP32 as it has good community support) how we can use zephyr framework with arduino style code. (writing basic stuff like blink LED at first but in an arduino sketch format but using zephyr in the lower level)
 - After doing this, figure out how custom libraries built for arduino platform can be used with underlying zephyr.
 - Then write basic examples demonstrating how to implement arduino API but really using zephyr underneath hence to support all boards that zephyr supports with Arduino / C++ sketch .

- After this I drafted my proposal and asked for review.
- After making necessary corrections and approval I submitted my proposal on GSoC website.
