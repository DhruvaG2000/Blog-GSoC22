---
layout: default
title: The Mbed OS Way
parent: Documentation
nav_order: 4
---

# Arduino Core for mbed enabled devices

[This repo](https://github.com/arduino/ArduinoCore-mbed) contains an implementation of Arduino style classes and methods but using mbed OS underneath. This is something very similar to what we are trying to do with Zephyr.

## UART/ Serial Implementation

- Inside [Arduino.h](https://github.com/arduino/ArduinoCore-mbed/blob/master/cores/arduino/Arduino.h#L108) there is a ``#define`` that leads to an object ``_UART1_`` inside [Serial.h](https://github.com/arduino/ArduinoCore-mbed/blob/master/cores/arduino/Serial.h).

- Here, we can see from ``extern arduino::UART _UART1_;`` that the object is of ``class UART`` which is defined just above.

- The implementations of the functions inside this class are then found in [Serial.cpp](https://github.com/arduino/ArduinoCore-mbed/blob/master/cores/arduino/Serial.cpp).

Similar structure can be followed for this project by simply replacing the implementations of all the functions with zephyr style functions.

## I2C Implementation

There is a file in the arduino API, ``HardwareI2C.h`` which contains the virtual prototypes of all the methods related to IIC. However as the class HardwareI2C is virtual we can not implement these methods as a part of this class and hence will need our own library / class definition that inherits from this _virtual base class_ .

To demostrate what I mean above in the form of pseudo code,

We have ``api/HardwareI2C.h`` that has the contents:
```c++
class HardwareI2C : public Stream
{
    public:
        virtual void begin() = 0;
        virtual void beginTransmission(uint8_t address) = 0;
        .
        .
        .   // other IIC methods
}
```

Now, inorder to implement all the above methods, we can then create our own class like in the case of mbed, they have ``libraries/Wire``
```c++
class MbedI2C : public HardwareI2C
```
where the custom ``class MbedI2C`` inherits these method names from the arduino api. These functions and then implemented inside ``Wire.cpp``.

Inorder to access all these functions, we have the object called ``Wire`` which is standard and used in many arduino libraries, using ``extern arduino::MbedI2C Wire;`` inside ``Wire.h``.