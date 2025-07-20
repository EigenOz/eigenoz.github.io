---
title: Integrating TensorFlow Lite with Embox RTOS  
date: 2025-07-15  
categories: [OSPP'25]  
tags: [OSPP'25]  
---

#  Porting TensorFlow Lite to a New Platform!

Ever wondered what it takes to get **TensorFlow Lite Micro (tflite-micro)** running on a fresh, unexplored platform like *Embox RTOS*? Here’s the ride – bumpy, fun, and definitely enlightening!

## Why Port TensorFlow Lite Micro to Embox RTOS?

While exploring how platforms like **Zephyr RTOS**, **ESP-IDF**, **Arduino**, and **Adafruit** brought tflite-micro aboard (mostly back in 2021, when it was still part of the original TensorFlow repo), I stumbled upon a twist—TensorFlow Lite Micro spun off as its own project! Suddenly, Makefile support was deprecated, and it’s now *Bazel* and *CMake* everywhere.


## The DIY Porting Recipe

To port tflite-micro onto Embox, here’s what I had to do:

1. **Source the Dependencies:**  
   Grab all the essential third-party libs from GitHub as standalone packages:  
   - `gemmlowp`  
   - `ruy`  
   - `kissfft`  
   - `flatbuffers`

2. **Build Like a Boss:**  
   - Bundle these dependencies straight into the Makefile  
   - Wire everything up within Mybuild so all source files and executables go into a temporary build folder.

3. **Create the Static Library:**  
   - Wrap all those object files into a slick static library: `libtflm.a`  
   - Now, compiling any ML model for Embox is as easy as linking with `libtflm.a`.

## Hurdles Along the Way


- **Linking Maze:**  
  Figuring out how to link files and executables in both the Makefile and Mybuild was way trickier than expected.
- **Script Snafus:**  
  A few scripts in the official porting guide just weren’t playing nice. The guide wasn’t exactly a north star either when it came to picking out the right files and steps.

## Testing Triumphs 

To test the port, I whipped up a tiny Hello World app that simply prints “TensorFlow ported successfully.” And guess what? My very first PR got merged! Check it out here: [tflite-for-embox](https://github.com/embox/embox/pull/3692)

A big THANK YOU to **Anton Bondarev** and **Aleksey Zhmulin** for reviewing and merging my PR.

##  What’s Next? (Week 3 Goals)

- Build and test Hello World and Linear Regression models under EmboxRTOS in the QEMU shell
- Dive into implementing the Micro Speech model

Stay tuned for more edge-AI adventures on Embox – and cross your fingers for fewer Makefile headaches!
