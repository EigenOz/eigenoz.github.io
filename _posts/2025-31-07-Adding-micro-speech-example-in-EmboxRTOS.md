---
title: Adding `Micro-Speech` (Sine Wave) Example to Embox RTOS  
date: 2025-07-31  
categories: [OSPP'25]  
tags: [OSPP'25]  
---

# OSPP Week 4 Progress

---

## Integrating "Hello World" as an Embox Module

I have successfully integrated the "hello world" model (from TensorFlow Lite Micro) into Embox RTOS as a new project module. The executable compilation completes as expected; however, I encountered challenges embedding it into the final system image for QEMU-based testing. Following the Embox documentation for application modules, the executable is built, but the image build process is not correctly sourcing the binary for inclusion in the EmBox image.

At this stage, I am focusing on resolving this integration hurdle. Completing this will be foundational for deploying any additional models, as it establishes a clear pipeline from model development to in-system testing on EmBox—first in virtual environments (QEMU), and later on actual hardware.

---

## Building the Micro-Speech Model

Building on the "hello world" example, the next step was to tackle a more advanced scenario: integrating the Micro-Speech model. This example demonstrates a simple speech recognition application suitable for edge devices and involves two main sub-models:

1. **Audio Preprocessing Model**  
   This provides a classic digital signal processing front-end: converting raw PCM audio into a time-frequency spectrogram suitable for ML input. Audio is segmented into overlapping 30ms windows (with 20ms stride) at 16kHz mono, 16-bit signed, generating either int8 or float32 outputs to feed the next stage.

2. **Micro Speech Model**  
   This is a compact (sub-20kB) neural network that recognizes two spoken keywords—"yes" and "no"—from the computed spectrogram. It outputs classification probabilities for these categories.

The audio preprocessing and speech recognition models are pre-generated and provided in the models directory, ready for direct use.

#### Model Training

I trained the micro-speech model using the official TensorFlow Lite Micro notebook:

[Micro-Speech Training Notebook](https://colab.research.google.com/github/tensorflow/tflite-micro/blob/main/tensorflow/lite/micro/examples/micro_speech/train/train_micro_speech_model.ipynb#scrollTo=_DBGDxVI-nKG)

---

After gathering the necessary signal processing source code from the upstream TFLM repository and integrating it into my build, I verified the entire "micro-speech" pipeline on a standard Linux host—successfully running the model and confirming correct operation.

![Micro-Speech Output](assets/op_ms.png)

---

I then ported the same setup to Embox RTOS. The binary compiles without issue, but once again, inclusion in the final EmBox image (and consequently QEMU testing) is hindered by the same integration error encountered with "hello world." This seems to be related to how the generated executable or object is incorporated into the Embox build system.

---

### Plans for Next Week

1. **Documentation:**  
   Prepare end-to-end instructions for building, integrating, and testing the `micro_speech` example, including all setup steps and build pipeline specifics.

2. **Module Inclusion & Testing:**  
   Diagnose and resolve the build/packaging error that prevents both "hello world" and "micro_speech" modules from appearing in the final EmBox system image. Complete functional validation in QEMU, and (if time allows) carry the same to real hardware, targeting the STM32F2 series MCUs.

---

**If you’re interested in ML on microcontrollers or contributing to Embox RTOS, stay tuned: once the build system issue is solved, adding future models or ML use cases will become much easier for everyone!**
