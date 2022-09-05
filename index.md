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
4. [Challenges Faced](#hurdles)
5. [Pull Requests](#pr)
6. [Future Scope](#scope)
7. [Benefit](#benefit)
8. [Additional Links](#ref)

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

Using west, the Zephyr meta tool, Arduino sketches can be compiled and flashed to your target board. Beyond core functions, the addition of an RTOS opens up the ability to use multiple threads in Arduino. A sample has been developed
in the project's repository [here: threads_arduino](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/tree/main/samples/threads_arduino)

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

## Challenges Faced <a name="hurdles"></a>

* Figuring out **West**. Although West: Zephyr's Meta tool is very powerful and robust, it still has it's own learning curve.
I had to study about how zephyr modules actually work. A module in Zephyr is sort of like installing an App on your mobile!
However, this "App" has a structure that needs to be carefully defined or else Zephyr might potentially not even find where
this app is/ not include it while building your project.
Secondly, How external modules are to be loaded and how code is to be written in these modules was something I had to deep dive into as well.
To summarize my findings, The two most important things for your module to work is the KConfig options and the ``CMakeLists.txt``'s.
Imagine CMakelists is like a huge spider web that helps the build system locate and go through wherever your source files are and automatically
link everything together! It really eases the build process because the Code can be very well abstracted in terms of the headers it uses, while
still not throwing a hundred header not found errors!
The Kconfig options help you enable all the features and libraries that you may need from Zephyr or in general, does the job of deciding which
libraries to statically compile when you build your projects.
However, having a different config for every sample again meant that we were making the end user's job more complicated and this might not be
most intuitive stuff to dive in especially for a newcomer.
Hence, the idea of a [module.conf](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/blob/main/module.conf) file was discussed
wherein all the required Kconfig options would be declared, thus eliminating the need to figuring out which KConfigs are needed to
successfully compile the module along with your project.

* **Device Trees** are one of the very unique features of Zephyr RTOS. Inorder to fully leverage the power of Zephyr, and re-use the boards that it already
supports, but in a more cleaner and elegant manner, my mentor Mike intrduced me to the concept of Device Tree Overlays in Zephyr.
Having worked briefly with DT Overlays in my previus GSOC I was mildly familiar with the concept, but far from writing entire Overlays on my own!
However, after looking at a sample device tree made by Mike, and understanding how they link with the connector DTSI files I was finally able to get a handle
on how device tree overlays work and why they should be used in this project.
Now, to save future contributors the trouble of figuring out how overlays work on their own, we have provided documentation in the project's repo along with
examples of multiple variants to refer to.

* **Locating DT OVerlays**. Well, great that you've added your own variant and written your own DT Overlay. But, now how does the compiler know what your
overlay you've written and where it is? To solve this issue, you can pass a commandline argument in Zephyr,
```sh
west build -b boardname -DDTC_OVERLAY_FILE=$(PATH_TO_OVERLAY)/boardname.overlay
```
But hey, the goal of this project was to make things simpler for the user and not burden them with all these details!
After a week of brainstorming and studying the Docs, I was finally able to come up with an elegant-enough [CMakeLists setting](https://github.com/zephyrproject-rtos/gsoc-2022-arduino-core/blob/main/samples/blinky_arduino/CMakeLists.txt#L6) that basically helped automatically locate the
overlay for the user without needing to specify along with the west command!

* Inorder to use the APIs, a good understanding of C++ OOPs concepts was essential. This is where my learnings
from my previous GSoC experience really came in handy as I was already well acquainted with Abstract Base classes
and virtual function. An example can be seen in the ``Wire`` library. Here, functions like ``virtual size_t write``,
``read()`` , ``peak()`` were already virtual inside the Arduino Core API. However the implementation is absent as is the
definition of the keyword virtual.
Inorder to get hints as to how to proceed with the implementation I took help of the [Arduino MBED](https://github.com/arduino/ArduinoCore-mbed)
This really gave me a good perspective on how I could maintain standardization by keeping the structure and methods similar. However,
the uniqueness was in the fact that all of this project's implementation were in the form of Zephyr APIs rather than MBed. This meant
digging through Zephyr Documentation for all the equivalent functions, figuring out things like ring buffers and how they are used, and
it was an overall deep dive into how I2C works in Zephyr as well as in general.

* The **scope** and "variable declared multiple times" errors.
It was very important to keep in mind the arduino namespace. Namespaces are used to organize code into logical groups and to prevent name collisions that can
occur especially when your code base includes multiple libraries like was the case in this project.
Coming to the issue of multiple declarations, this is where I truly learned the value of the "extern" keyword. Extern variable says to compiler  ” go outside my
scope and you will find the definition of the variable that I declared.”
For example, in ``Wire.h``
```C
extern arduino::ZephyrI2C Wire;
```
we declare Wire to be extern, and then in ``Wire.cpp`` we actually define it.
By using the extern keyword with a variable, we can use the variable anywhere in the program provided we include it's
declaration the variable is defined somewhere

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
- [GFG: extern in C](https://www.geeksforgeeks.org/understanding-extern-keyword-in-c/)