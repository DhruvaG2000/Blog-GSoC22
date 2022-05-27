---
layout: default
title: Zephyr Modules
parent: Documentation
nav_order: 3
---

# [Modules (External projects)](https://docs.zephyrproject.org/latest/develop/modules.html)

To be classified as a candidate for being included in the default list of modules, an external project is required to have its own life-cycle outside the Zephyr Project, that is, reside in its own repository, and have its own contribution and maintenance workflow and release process. This is why this project aims to create the Ardiuno Core API as a zephyr module.

## Integrate modules in Zephyr build system

The build system variable ``ZEPHYR_MODULES`` is a CMake list of absolute paths to the directories containing Zephyr modules. These modules contain ``CMakeLists.txt`` and Kconfig files describing how to build and configure them, respectively. Module ``CMakeLists.txt`` files are added to the build using CMake’s ``add_subdirectory()`` command, and the _Kconfig_ files are included in the build’s Kconfig menu tree.

You can add additional modules to this list by setting the ZEPHYR_EXTRA_MODULES CMake variable or by adding a ``ZEPHYR_EXTRA_MODULES`` line to ``.zephyrrc``. 
This can also be given with ``-DZEPHYR_EXTRA_MODULES=/<path>/foo`` then the module given by the command line variable ``ZEPHYR_EXTRA_MODULES`` will take precedence. This allows you to use a custom version of FOO when building and still use other Zephyr modules provided by west. This can for example be useful for special test purposes.

### [Module yaml file description](https://docs.zephyrproject.org/latest/develop/modules.html#module-yaml-file-description)

A module can be described using a file named zephyr/module.yml. The format of zephyr/module.yml is described in the following:
