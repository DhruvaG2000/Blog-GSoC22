---
layout: default
title: zephyr-basics
parent: Documentation
nav_order: 2
---

# Ubuntu Zephyr Setup and Basic Usage

Follow the guide given by zephyr [here](https://docs.zephyrproject.org/latest/develop/getting_started/index.html)

Build the Blinky with ``west build``, changing ``<your-board-name>`` appropriately for your board:

```sh
cd ~/zephyrproject/zephyr
west build -p auto -b <your-board-name> samples/basic/blinky
```

Then flash the sample using ``west flash``
