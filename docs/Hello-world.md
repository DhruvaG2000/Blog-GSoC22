---
layout: default
title: Hello World example
parent: Documentation
nav_order: 4
---

# Overview
A simple sample that can be used with any supported board and prints “Hello World” to the console along with a demonstration of arduino loop with delay.

## Building and Running

1. First make sure you clone [this module](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core.git) into your ``<zephyr-root>/modules/lib/``

2. Copy the ``arduino_hello_world`` example into zephyr samples.

3. Finally, this example can be built and executed on QEMU as follows:
```sh
west build  -p -b qemu_x86 samples/arduino_hello_world -DZEPHYR_EXTRA_MODULES=/home/$USER/zephyrproject/modules/lib/Arduino-Core-Zephyr
west build -t run
```