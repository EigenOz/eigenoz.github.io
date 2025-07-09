---
title: Getting started with core integration of tflite-micro
date: 2025-07-07
categories: [OSPP'25]
tages: [OSPP'25]
---
<!--
# Getting started with OSPP @ Embox 

So the results were announced on 28th of June. I got selected to complete the project titled : `To integrate ML framework into Embox and add ML models for inferencing`. It's an amazing project in the domain of Embedded-ML to learn how to integrate several machine learning functions to RTOS and perform ML-inferencing on edge using contraiend resources. 

## Revisiting my proposal and comunity bonding. 

The first task I took as the community bonding period started is to revisit my proposal and confirm all the milestones and appraoch with my mentor `Anton Bondarev`. We decided on moving forward as per the proposal submitted and get started with the task of core integration of tfite-micro to EmboxRTOS.

EmboxRTOS is a modular RTOS , highly configurable supporting multiple platforms. We can configure which features to add or remove while building an image as per our SBC. So to integrate TFLM , it must be a third party support and must be installed and configured while building process. Embox supports Mybuild style to configure and add modules to build process. So I started to code Mybuild and Makefile to include tflite-core files for vanilla testing.

# Understanding tflite-micro porting to a new platform 
![tflite-micro](assets/tflite-micro.png) 
![embox](assets/embox.png)

Although , they have provided the official guide to port tflite-micro to any platform , but we need a complete understanding of the platform and its make style before we port core files. They have provided a python  script to generate a minimal tree with examples and their essential core files needed to compile the examples. The core files including third party dependencies (gemmlowp , ruy , kissfft) are compiled into a static lib: 'libtflm.a' which is utilised for running each example.

Hence , before I directly jump into testing this on EmboxRTOS , I tried to compile this tree on linux first and test on my PC to understand what all core files are included and how is the process happening using custom makefile. I tried compiling hello world example and it worked. 
Following is the successful output expected :

![test](assets/tflm_tree_test.png)

# TFLM on Embox 

Before full integration of TFLM core files , My first task is to replicate a similar result of the hello world test while compiling all the files in embox build process. 

I am still understanding Embox code-structure and testing tflm tree using extbld. 

## Expectation in the coming week

I hope to achieve the following goals in the coming week :
- Test TFLM core tree withing Embox build process
- Integrate hello world (sine wave) and linear regression model from    
scratch.


Thank you!

 -->


<!-- ---
title: OSPP Week 1: Kicking Off TFLite-Micro Integration into Embox
date: 2025-08-07
categories: [OSPP'25]
tags: [OSPP'25, Embedded-ML, RTOS, TFLM, Embox]
--- -->

# 🚀 OSPP Week 1: Kicking Off TFLite-Micro Integration into Embox

The results for the **Open Source Promotion Plan (OSPP) 2025** were announced on **June 28**, and I’m thrilled to share that I’ve been selected to work on the project:

> **"Integrate ML framework into Embox and add ML models for inferencing."**

This is a fantastic opportunity to dive deep into the **intersection of machine learning and embedded systems**, particularly exploring how to enable **on-device inferencing** on resource-constrained platforms using **TFLite Micro (TFLM)** and **Embox RTOS**.

---

## 🔍 Project Overview

- **Organization**: [Embox RTOS](https://github.com/embox/embox)
- **Mentor**: [Anton Bondarev](https://github.com/bondarev)
- **Goal**: Integrate the core of TensorFlow Lite Micro (TFLM) into Embox, enabling ML model inferencing directly on embedded targets. This includes supporting multiple lightweight models (e.g., sine wave, linear regression).

---

## 🧠 Community Bonding & Project Kickoff

During the community bonding phase, I:

- Revisited my original proposal and aligned timelines, milestones, and strategies with my mentor.
- Finalized that we’ll **stick closely to the proposed plan**, starting with the core integration of TFLM as a third-party module in Embox.
- Began exploring **Embox’s modular Mybuild system**, which is used to integrate external libraries during the build.

---

## ⚙️ First Dive into TFLite Micro

Before integrating TFLM directly into Embox, I wanted to understand **how TFLM is structured and built independently**.

TFLM provides an official [project generation script](https://github.com/tensorflow/tflite-micro/tree/main/tensorflow/lite/micro/tools/project_generation) to create a minimal project tree containing:

- Core files (`micro`, `kernel`, `core`)
- Third-party dependencies (`ruy`, `gemmlowp`, `kissfft`)
- Build files (Makefiles)
- Examples like `hello_world`, `magic_wand`, etc.

### ✅ I successfully:

- Generated the minimal `hello_world` example.
- Built and ran it on my local Linux machine using a **custom Makefile**.
- Verified that the static library `libtflm.a` is properly created and linked.

Here's a snapshot of the successful build:

![test](assets/tflm_tree_test.png)

---

## 🧩 Understanding Embox Integration

Embox is a highly configurable RTOS that allows modular integration through its `Mybuild` and `Makefile` structure.

To begin porting TFLM into Embox:

- I started writing `Mybuild` rules to include the TFLM tree.
- Ensured both `tensorflow/` and `third_party/` directories are handled properly.
- Set up an initial test integration for the `hello_world` example.

I’m currently testing this using **`extbld`**, Embox's extension build system for external projects.

---

## 🧗 Challenges Faced

Here are some early hurdles and how I’m tackling them:

| Challenge | Strategy |
|----------|----------|
| Understanding Embox’s internal build system | Reading through `src`, `mk`, and example modules like `libpng`, `mbedtls` |
| Linking `libtflm.a` inside Embox’s linker setup | Experimenting with `extbld` Makefiles, simplifying dependency tree |
| Avoiding redundant dependencies during build | Manually listing only essential `.cc` files and trimming unused ops |

---

## 💡 Key Learnings

- The **project generation script** for TFLM is a goldmine—provides clean structure for new platform porting.
- **Embox’s build system** is flexible but requires understanding its modular compilation pipeline.
- Importance of minimizing included source files to reduce build time and binary size.
- Static linking in embedded environments comes with its own quirks—especially with nested third-party dependencies.

---

## 🎯 Goals for Week 2

Here’s what I aim to achieve next week:

- ✅ Complete integration of the **TFLM core tree** into Embox’s build system.
- 🔄 Test full compilation of **hello_world** from within Embox.
- 📈 Add support for additional lightweight models like **linear regression**.
- 🧪 Set up a repeatable workflow for compiling and testing inference models.

---

## 🙏 Thank You!

Thanks to my mentor Anton and the Embox team for their guidance this week. The journey ahead is exciting, and I look forward to making meaningful progress.

Stay tuned for Week 2!

Feel free to share your thoughts, feedback, or suggestions in the comments or reach out via [GitHub](https://github.com/Herculoxz).

---

📚 **Resources**:

- [TFLite Micro GitHub](https://github.com/tensorflow/tflite-micro)
- [Embox GitHub](https://github.com/embox/embox)
- [My Proposal](#)
