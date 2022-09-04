---
layout: default
title: Home
nav_order: 1
description: "Official Blog for Google Summer of Code 2022 to maintain Documentation, progress logs and research"
permalink: /
has_children: false
---

# GSoC'22- Arduino module based on Zephyr

![im](assets/images/website_header.png)

The project idea was to create a Zephyr module that leverages the Arduino Core API so that a developer can use Zephyr as the underlying OS while they keep using the Arduino framework on Arduino-compatible devices.

## About
- _Student Name:_ [Dhruva Gole](https://dhruvagole.tech)
- _Mentors:_ Jonathan Beri, Alvaro Viebrantz, Mike Szczys
- _GSoC Entry link:_ [Program Project Page](https://summerofcode.withgoogle.com/programs/2022/projects/CLdtJiEB)
- _Wiki:_ [Github Issues on zephyr](https://github.com/zephyrproject-rtos/zephyr/issues/32621)
- _Blog Link:_ [Arduino Module based on Zephyr](https://dhruvag2000.github.io/Blog-GSoC22/) <br>

## Table of Contents
1. [Introduction](#intro)
2. [Documentation](#docs)
3. [Achieved Milestones](#milestones)
4. [Pull Requests](#pr)
5. [Future Scope](#scope)
6. [Benefit](#benefit)
7. [Additional Links](#ref)

## Introduction <a name="intro"></a>

The [Zephyr RTOS](https://docs.zephyrproject.org/latest/introduction/index.html) is based on a small-footprint kernel designed for use on resource-constrained and embedded systems: from simple embedded environmental sensors and LED wearables to sophisticated embedded controllers, smart watches, and IoT wireless applications.

Zephyr intends to provide all components needed to develop resource-constrained and embedded or microcontroller-based applications. This includes, but is not limited to:
- A small kernel
- A flexible configuration and build system for compile-time definition of required resources and modules
- A set of protocol stacks (IPv4 and IPv6, Constrained Application Protocol (CoAP), LwM2M, MQTT, 802.15.4, Thread, Bluetooth Low Energy, CAN)
- A virtual file system interface with several flash file systems for non-volatile storage (FatFs, LittleFS, NVS)
Management and device firmware update mechanisms.

This in union with the Arduino Ecosystem unlocks a whole new platform for engineers and DIY enthusiasts alike to
do rapid prototyping but still use a robust and advanced RTOS like zephyr without getting into too much specific
implementation details.

## Project Preview

The basic goal is to have almost any top of the shelf arduino tutorial/ libaries to work with zephyr. We have many
samples which almost completely resemble the code that you would write inside the Arduino IDE. Shown below is a code
snippet of a basic press a button to turn on LED sample,

<pre class="hljs" style="display: block; overflow-x: auto; padding: 0.5em; background: rgb(240, 240, 240); color: rgb(68, 68, 68);"><span class="hljs-comment" style="color: rgb(136, 136, 136);">/*
 * SPDX-License-Identifier: Apache-2.0
 */</span>

<span class="hljs-comment" style="color: rgb(136, 136, 136);">/* Button Press turns on inbuilt LED example */</span>

<span class="hljs-meta" style="color: rgb(31, 113, 153);">#<span class="hljs-meta-keyword" style="font-weight: 700;">include</span> <span class="hljs-meta-string" style="color: rgb(77, 153, 191);">&lt;Arduino.h&gt;</span></span>

<span class="hljs-keyword" style="font-weight: 700;">const</span> <span class="hljs-keyword" style="font-weight: 700;">int</span> buttonPin = D9; <span class="hljs-comment" style="color: rgb(136, 136, 136);">// the number of the pushbutton pin</span>
<span class="hljs-keyword" style="font-weight: 700;">const</span> <span class="hljs-keyword" style="font-weight: 700;">int</span> ledPin = <span class="hljs-number" style="color: rgb(136, 0, 0);">13</span>;    <span class="hljs-comment" style="color: rgb(136, 136, 136);">// the number of the LED pin</span>

<span class="hljs-comment" style="color: rgb(136, 136, 136);">// variables will change:</span>
<span class="hljs-keyword" style="font-weight: 700;">int</span> buttonState = <span class="hljs-number" style="color: rgb(136, 0, 0);">0</span>; <span class="hljs-comment" style="color: rgb(136, 136, 136);">// variable for reading the pushbutton status</span>

<span class="hljs-keyword" style="font-weight: 700;">void</span> <span class="hljs-built_in" style="color: rgb(57, 115, 0);">setup</span>() {
  <span class="hljs-comment" style="color: rgb(136, 136, 136);">// initialize the LED pin as an output:</span>
  <span class="hljs-built_in" style="color: rgb(57, 115, 0);">pinMode</span>(ledPin, <span class="hljs-literal" style="color: rgb(120, 169, 96);">OUTPUT</span>);
  <span class="hljs-comment" style="color: rgb(136, 136, 136);">// initialize the pushbutton pin as an input:</span>
  <span class="hljs-built_in" style="color: rgb(57, 115, 0);">pinMode</span>(buttonPin, <span class="hljs-literal" style="color: rgb(120, 169, 96);">INPUT</span>);
}

<span class="hljs-keyword" style="font-weight: 700;">void</span> <span class="hljs-built_in" style="color: rgb(57, 115, 0);">loop</span>() {
  <span class="hljs-comment" style="color: rgb(136, 136, 136);">// read the state of the pushbutton value:</span>
  buttonState = <span class="hljs-built_in" style="color: rgb(57, 115, 0);">digitalRead</span>(buttonPin);

  <span class="hljs-comment" style="color: rgb(136, 136, 136);">// check if the pushbutton is pressed. If it is, the buttonState is HIGH:</span>
  <span class="hljs-built_in" style="color: rgb(57, 115, 0);">if</span> (buttonState == <span class="hljs-literal" style="color: rgb(120, 169, 96);">HIGH</span>) {
    <span class="hljs-comment" style="color: rgb(136, 136, 136);">// turn LED on:</span>
    <span class="hljs-built_in" style="color: rgb(57, 115, 0);">digitalWrite</span>(ledPin, <span class="hljs-literal" style="color: rgb(120, 169, 96);">HIGH</span>);
  } <span class="hljs-built_in" style="color: rgb(57, 115, 0);">else</span> {
    <span class="hljs-comment" style="color: rgb(136, 136, 136);">// turn LED off:</span>
    <span class="hljs-built_in" style="color: rgb(57, 115, 0);">digitalWrite</span>(ledPin, <span class="hljs-literal" style="color: rgb(120, 169, 96);">LOW</span>);
  }
}</pre>

For more samples, just visit the ``sample/`` folder on the project's [github page](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core)

External libraries like ``Wire`` has also been developed for I2C which enables usage of any sensor that communicates over
IIC! This way you can literally pick any library out there for your sensor and it will fit right in with your zephyr
development flow.

## Documentation <a name="docs"></a>

This project can be roughly abstracted in the form of a block diagram shown below,

<p align="center">
  <img src="assets/images/main_flow.png" />
</p>

As seen, we have used the Arduino Core APIs as an abstraction layer to the actual zephyr APIs. However the build process
used is [Zephyr's meta-tool: west](https://docs.zephyrproject.org/latest/develop/west/index.html).
West is a very easy to use command line tool which aids in almost everything from multiple repository management system,
to building applications, flashing and debugging them.

Using west, the Zephyr meta tool, Arduino sketches can be compiled and flashed to your target board. Beyond core functions, the addition of an RTOS opens up the ability to use multiple threads in Arduino. Dhruva has includes an excellent threading demonstration by blinking multiple LEDs asynchronously.

The entire project has been documented in the project's README as well as [Documentation folder](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/tree/main/documentation).

Additionally, A short youtube video covers how to use this module. Do check it out [here](https://www.youtube.com/watch?v=0Byv6X1sKrk).

## Achieved Milestones <a name="milestones"></a>

The milestones reached in the project thus far include:

- Arduino Digital GPIO functions (e.g.: pinmode, digitalRead, digitalWrite)
- Arduino time functions (e.g.: delay, millis)
- I2C support via the Wire library API (works with external Arduino libraries)
- A DeviceTree framework for mapping Arduino header pins to any Zephyr boards
- Serial.println and print support

## Pull Requests <a name="pr"></a>

1. [gpio: adds basic digital i/o support](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/pull/7)
2. [restructure: use variants folder](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/pull/17)
3. [Add multithreading sample](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/pull/18)
4. [Add Documentation](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/pull/20)
5. [start writing Serial wrapper](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/pull/30)
6. [Update cmakelists in all samples](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/pull/31)
7. [Add I2C Support in the form of Wire Library](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/pull/34)
8. [zephyrSerial: Add more print variants](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/pull/39)
9. [zephyrCommon: Implement yield()](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/pull/41)

Other than the above merged PRs, there are pending PRs to add more boards/variants support. Please visit the project's
[Pull Requests](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/pulls) to view them and/or add your own
variants to the list!

## Future Scope <a name="scope"></a>

The heavy lifting of integrating the Arduino core with Zephyr has already been completed and is working well. But to use
this, you must already have a Zephyr workspace installed (and know how to use it). Sure, Zephyr Documentations has a
quickstart that helps install Zephyr, but the ability to use this project from the Arduino IDE is desirable for existing
Arduino users.

Unfortunately, there isn’t time left to work this level of integration. But contributions to the program are welcome and
hope that future contributors will take on this task.

There is also low-hanging fruit when it comes to implementing the most-used Arduino functions. For instance, random
numbers, bits and bytes, and math functions should all be trivial to get working. More ambitious contributors may
consider mapping the Zephyr ADC system to ``analogRead()`` and ``analogWrite()``.

## Benefit <a name="benefit"></a>

Quoting [Jonathan Beri](https://github.com/beriberikix),

> Arduino's popularity is renowned as a popular framework for providing a simplified interface to program embedded devices. Recently, Arduino adopted mbed OS as the base RTOS for some of their newer devices. With that work, they separated out Arduino Core as an independent abstraction layer from Arduino Core for mbed. This opens up the possibility for leveraging Arduino Core on other OSes.


Essentially,
- This project starts an effort to use Arduino APIs as well as advanced Zephyr capabilities. 
- It enables a broader set of devices than the standard Arduino ecosystem thanks to Zephyrs' device support.
- In future perhaps we will also have the ability to re-use Arduino tools like the Arduino IDE and wealth of libraries that it offers.

## Additional Links <a name="ref"></a>

- [Golioth Blog: Zephyr + Arduino: a Google Summer of Code story](https://blog.golioth.io/zephyr-arduino-a-google-summer-of-code-story/)
- [Original GSoC Project idea - Zephyr issue # 32621](https://github.com/zephyrproject-rtos/zephyr/issues/32621)
- [Discussion: Supporting the Arduino ecosystem](https://github.com/zephyrproject-rtos/zephyr/issues/22247).
- [Installing Zephyr on linux](https://learn.adafruit.com/blinking-led-with-zephyr-rtos/installing-zephyr-linux)
- [Arduino on Zephyr project](https://github.com/soburi/arduino-on-zephyr).
- [Arduino core API](https://github.com/arduino/ArduinoCore-API)
- [Arduino core mbed](https://github.com/arduino/ArduinoCore-mbed)
