---
title: Porting Micro Speech model to Zephyr RTOS 
date: 2025-04-10
categories: [Embedded-ML]
tags: [Embedded-ML]     # TAG names should always be lowercase
---
# Introduction to micro_speech model from TFLite 

The Micro speech program analyzes an audio input with a voice recognition model that can detect 2 keywords - yes and no. The recognized keywords are then printed into a serial interface. The voice recognition model is implemented using TensorFlow Lite for Microcontrollers.

Micro Speech demonstrates how to use the processor and peripheral abstraction layers to preprocess the data and 
demonstrating the usecase of basic signal processing APIs of the Operating system of hardware.

## Model architecture : 
![netron image](assets/arch_micro_speech.png)

---

## Coding this model for Zephyr RTOS :
- There are numerous implementations of micro_speech available online, including those for Particle, ESP, and Arduino platforms. Therefore, it makes practical sense to port a similar codebase to Zephyr by adapting the necessary APIs and syntax in accordance with Zephyr’s documentation.

- This proved to be a good learning opportunity, helping me understand both the utility of APIs for model-specific operations and the inner workings of the TFLite codebase in great detail. 

- An analysis of existing TFLite-Micro examples within Zephyr reveals a common code structure inspired by the Arduino programming model, typically utilizing setup() and loop() functions in main.c. This template serves as a foundation, with only the model-specific source files being modified or added accordingly. And I would recommend to use the same CMakeLists.txt and sample.yaml file as that of hello_world in zephyr samples so that we do not change any directory path unintentionally which might cause silly CMake errors! 

### This is the basic code structure of the implementation of micro-speech 

![code structure](assets/code_str_micro_speech.webp)

You can find the code here :  [**Micro_Speech**](https://github.com/Herculoxz/zephyr/tree/main/samples/modules/tflite-micro/micro_speech)

- When porting TensorFlow Lite (TFLite) code—whether generated by a program generator or sourced from another platform—to Zephyr, the following APIs are frequently used:

1. zephyr/kernel.h

2. zephyr/log.h

3. zephyr/drivers/i2s.h (used when the model involves I2S-specific hardware interactions)

- Zephyr provides a wide range of APIs to support various use cases. Depending on the model's requirements, you can choose the appropriate APIs from this extensive set. For more details, refer to the Zephyr API documentation, which is helpful in matching the model’s feature requirements with available system capabilities.

- Currently my code is only limited to yes , no keywords for inference. But this can be extended to several other keywords if the model is provided with the features of that keyword. 

output of the model is expected as : 
![output image](assets/micro_speech_op.png)

