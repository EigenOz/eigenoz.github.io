---
title: Adding `hello_world` (Sine Wave) Example to EmboxRTOS  
date: 2025-07-23  
categories: [OSPP'25]  
tags: [OSPP'25]  
---

# Ospp Week 3: Sine Wave Prediction Using a Neural Network

![Model Architecture](assets/arch_micro_speech.png)

The `hello_world` example provided by TensorFlow Lite Micro (TFLM) serves as a minimal reference model to validate integration on new platforms. It implements a simple neural network that predicts sine wave values for a set of input values. This example is commonly used to verify that the TFLM interpreter, operator resolution, memory allocation, and inference all function correctly in an embedded environment.

While TensorFlow still provides a training script to generate the sine model, the structure of the example has changed significantly since the 2023 update. Previously, it included multiple files such as `output_handler.cc`, `main.cc`, and `constants.cc`. These have now been consolidated into a single file: `hello_world_test.cc`.

### Integration with EmboxRTOS

To integrate this example with EmboxRTOS:

- I made a minor addition in the `main()` function to call the neural network and print the predicted values.
- No Embox-specific modifications were necessary; the integration worked directly with the existing logic in `hello_world_test.cc`.

This exercise was helpful in understanding:

- How to compile and link TFLM models within Embox’s external build system.
- How to integrate and source the executable from a new example module and include it in the final image.

I chose to use an **external Makefile** instead of Embox’s `Mybuild` system, as I had already used it to test the model on Linux beforehand.

---

### Goals for Next Week

1. Add complete documentation for the `hello_world` example, including setup and reproduction steps.
2. Port the `micro_speech` example with test audio inputs and verify its functionality on Embox.

