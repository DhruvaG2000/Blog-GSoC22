---
layout: default
title: Week 4
parent: Weekly Progress
nav_order: 6
---

# Week 4

(14th June - 20th June)

MoM with @jberi, @Mike Szczys and @alvaro on Tuesday 14th June:
- I showed the progress so far about how I had implemented the ``setup()`` and ``loop()`` flow, the Blink LED (pinMode implementation), also discussed that I am thinking of implementing ``Wire.h`` in zephyr so as to support the arduino _ADS1115_ driver.
- Further discussed the GPIO implementation for pinMode and other funcs. An approach to generalize the code instead of hardcode everything would be to use the DT aliases. I will be exploring this option in the coming week and perhaps be able to generalise the GPIO implementation for the arduino API to be able to use all the GPIOs on the nano ble sense 33. @Mike Szczys explained further how the aliases are defined in the device tree here . For example in the function ``gpio_pin_configure(const struct device *port, gpio_pin_t pin, gpio_flags_t flags``)  (documentation here) we can pass the parameters ``arduino_nano_header`` , ``0,1,2....21`` , ``GPIO_OUTPUT/ INPUT`` as per whatever the user dictates from the arduino style code.

A lot of important links and info has been shared in [chats on slack channel](https://join.slack.com/t/arduino-module-zephyr/shared_invite/zt-19j4cvbad-YuuDXUNPlEYF4sdpj3zyzw) for reference.

- Worked on GPIO implementations, first replaced the hardcoded ``LED_BUILTIN`` to generalise the code to accept any pin number.
- Added an arduino style blink LED example and tested on board as well as externally connected LEDs via the digital pins.
- Realised a big corner case while trying to blink multiple LEDs: The fact that there is only 1 ``static struct gpio_dt_spec pin;`` in our ``Comon.cpp`` means that one can only blink one Digital Pin at a given time. Meaning whichever is the last ``pinMode()`` is the pin which will work. The previous pinMode setups will just be override.
- Solution: Replaced the ``_dt`` functions with the leacy non-dt ones. This eliminates the need for a ``static struct gpio_dt_spec pin;`` altogether thus saving the memory that multiple objects of ``struct gpio_dt_spec`` might have otherwise used up.
- Added ``digital read`` as well as ``Write`` support to these gpios.
- Made the input GPIOs to be pulled down by default.
- Tested all the above using another simple example where a push button is connected externally to an input pin to get digital input and an LED is turned on when button is pressed and vice versa. The code compiles and executes as expected without any issues.
