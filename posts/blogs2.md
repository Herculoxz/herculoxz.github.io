---
title: Getting started with core integration of tflite-micro
date: 2025-07-07
Author: Abhinav Ananthu
tags: tflite , C , RTOS , EdgeAI
---

#  OSPP Week 1: Kicking Off TFLite-Micro Integration into Embox

The results for the **Open Source Promotion Plan (OSPP) 2025** were announced on **June 28**, and I’m thrilled to share that I’ve been selected to work on the project:

> **"Integrate ML framework into Embox and add ML models for inferencing."**

This is a fantastic opportunity to dive deep into the **intersection of machine learning and embedded systems**, particularly exploring how to enable **on-device inferencing** on resource-constrained platforms using **TFLite Micro (TFLM)** and **Embox RTOS**.

---

##  Project Overview

- **Organization**: [Embox RTOS](https://github.com/embox/embox)
- **Mentor**: [Anton Bondarev](https://github.com/bondarev)
- **Goal**: Integrate the core of TensorFlow Lite Micro (TFLM) into Embox, enabling ML model inferencing directly on embedded targets. This includes supporting multiple lightweight models (e.g., sine wave, linear regression).

---

##  Community Bonding & Project Kickoff

During the community bonding phase, I:

- Revisited my original proposal and aligned timelines, milestones, and strategies with my mentor.
- Finalized that we’ll **stick closely to the proposed plan**, starting with the core integration of TFLM as a third-party module in Embox.
- Began exploring **Embox’s modular Mybuild system**, which is used to integrate external libraries during the build.

---

##  First Dive into TFLite Micro

Before integrating TFLM directly into Embox, I wanted to understand **how TFLM is structured and built independently**.

TFLM provides an official [project generation script](https://github.com/tensorflow/tflite-micro/tree/main/tensorflow/lite/micro/tools/project_generation) to create a minimal project tree containing:

- Core files (`micro`, `kernel`, `core`)
- Third-party dependencies (`ruy`, `gemmlowp`, `kissfft`)
- Build files (Makefiles)
- Examples like `hello_world`, `magic_wand`, etc.

###  I successfully:

- Generated the minimal `hello_world` example.
- Built and ran it on my local Linux machine using a **custom Makefile**.
- Verified that the static library `libtflm.a` is properly created and linked.

Here's a snapshot of the successful build:

![test](assets/tflm_tree_test.png)

---

##  Understanding Embox Integration

Embox is a highly configurable RTOS that allows modular integration through its `Mybuild` and `Makefile` structure.

To begin porting TFLM into Embox:

- I started writing `Mybuild` rules to include the TFLM tree.
- Ensured both `tensorflow/` and `third_party/` directories are handled properly.
- Set up an initial test integration for the `hello_world` example.

I’m currently testing this using **`extbld`**, Embox's extension build system for external projects.

---

##  Challenges Faced

Here are some early hurdles and how I’m tackling them:

| Challenge | Strategy |
|----------|----------|
| Understanding Embox’s internal build system | Reading through `src`, `mk`, and example modules like `libpng`, `mbedtls` |
| Linking `libtflm.a` inside Embox’s linker setup | Experimenting with `extbld` Makefiles, simplifying dependency tree |
| Avoiding redundant dependencies during build | Manually listing only essential `.cc` files and trimming unused ops |

---

##  Key Learnings

- The **project generation script** for TFLM is a goldmine—provides clean structure for new platform porting.
- **Embox’s build system** is flexible but requires understanding its modular compilation pipeline.
- Importance of minimizing included source files to reduce build time and binary size.
- Static linking in embedded environments comes with its own quirks—especially with nested third-party dependencies.

---

##  Goals for Week 2

Here’s what I aim to achieve next week:

-  Complete integration of the **TFLM core tree** into Embox’s build system.
-  Test full compilation of **hello_world** from within Embox.
-  Add support for additional lightweight models like **linear regression**.
-  Set up a repeatable workflow for compiling and testing inference models.

---

##  Thank You!

Thanks to my mentor Anton and the Embox team for their guidance this week. The journey ahead is exciting, and I look forward to making meaningful progress.

Stay tuned for Week 2!

Feel free to share your thoughts, feedback, or suggestions in the comments or reach out via [GitHub](https://github.com/Herculoxz).

---

 **Resources**:

- [TFLite Micro GitHub](https://github.com/tensorflow/tflite-micro)
- [Embox GitHub](https://github.com/embox/embox)
- [My Proposal](#)