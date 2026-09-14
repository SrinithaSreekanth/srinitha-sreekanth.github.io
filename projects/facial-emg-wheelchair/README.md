# Facial EMG-Controlled Wheelchair – A Mobility Assistance for Quadriplegia

A hands-free, cost-effective smart wheelchair designed for individuals with quadriplegia using facial surface Electromyography (EMG) signals for real-time directional control.

---

## Overview

This project presents the hardware and software architecture of a hands-free, cost-effective smart wheelchair designed for individuals with quadriplegia.

The system captures and translates surface Electromyography (EMG) signals from specific facial muscles into real-time directional commands. By bypassing the need for upper limb functionality, the system provides an alternative to traditional joystick-operated assistive devices.

![Project Introduction](01-introduction.png)

---

## Key Features

- **Non-Invasive Control:** Utilizes surface electrodes placed on the cheeks to capture intentional facial gestures.
- **Real-Time Signal Processing:** Implements a 30 Hz to 500 Hz bandpass filter to eliminate physiological artifacts and electronic noise.
- **Wireless Transmission:** Employs an HC-05 Bluetooth module to send digital command signals to the hardware chassis.
- **Custom Threshold Mapping:** Uses digital stair plots, statistical parameters, and wavelet transform analysis to classify distinct facial movements.
- **Hands-Free Mobility:** Enables wheelchair directional control without requiring upper-limb movement.

---

## Hardware & Software Environment

### Hardware

| Component | Description |
|---|---|
| **BIOPAC MP45** | EMG signal acquisition |
| **Arduino UNO** | Microcontroller and command processing |
| **HC-05 Bluetooth Module** | Wireless command transmission |
| **L298N Motor Driver** | DC motor control |
| **12V 1.3AH SLA Battery** | Power supply |
| **DC Motors** | Wheelchair actuation |

### Software

- MATLAB Simulink
- Arduino IDE
- C++

---

## Movement Classification

| Muscle Activated | Target Gesture | Wheelchair Command |
|---|---|---|
| Left Buccinator | Left Cheek Movement | **Left Turn** |
| Right Buccinator | Right Cheek Movement | **Right Turn** |
| Zygomaticus Major | Smiling | **Forward Movement** |
| Zygomaticus Major | Strained Expression | **Backward Movement** |

---

## System Workflow

### 1. Signal Acquisition

Surface electrodes detect microvolt-level electrical activity from the targeted facial muscles.

### 2. Processing & Digitization

The analog EMG signals are amplified, filtered, and digitized through the BIOPAC MP45 system.

### 3. Feature Extraction

The system calculates statistical parameters including:

- Peak-to-peak amplitude
- Kurtosis
- Skewness
- Signal area
- Wavelet coefficients

### 4. Threshold Evaluation

The extracted features are compared against predefined threshold boundaries statistically validated using the **Kruskal-Wallis test**.

### 5. Actuation

When a feature falls within the active threshold range, a directional command is transmitted through Bluetooth to the Arduino UNO.

The Arduino then controls the DC motors through the L298N motor driver.

---

## System Workflow Diagram

![System Workflow](02-workflow.png)

---

## Results & Validation

### Statistical Significance

The Kruskal-Wallis test confirmed that extracted features, including peak-to-peak amplitude and signal area, significantly differentiate between distinct facial gestures, helping minimize misclassification.

### Hardware Execution

The 4WD prototype successfully demonstrated smooth and accurate mobility in all four directions without noticeable latency.

### Stability Improvements

High-torque motors and dedicated L298N motor drivers helped resolve early prototype issues related to jerky movements and load management.

![Final Prototype Results](03-final-results.png)

---

## Publications & Presentations

### CoaCoNS 2025

Accepted for presentation at the **Conference on Advances in Communication Networks & Systems (CoaCoNS 2025)**, SRM Institute of Science and Technology.

### NCRTAS 2024

Presented at the **2nd National Conference on Recent Trends in Artificial Intelligence and Soft Computing (NCRTAS 2024)**, Bannari Amman Institute of Technology.

---

## Project Significance

The project demonstrates how facial EMG signals can be used as an alternative human-machine interface for assistive mobility.

By translating intentional facial muscle activity into directional wheelchair commands, the system aims to provide hands-free mobility for individuals who cannot rely on conventional joystick-based control.

---

## Citation

If you use or reference this project, please cite:

```bibtex
@bachelorsthesis{srinitha2025facialemg,
  author       = {Srinitha S and Nivedha E and Ramya Bharathi S},
  title        = {Facial EMG controlled Wheelchair – a Mobility Assistance for Quadriplegia},
  school       = {Vels Institute of Science, Technology and Advanced Studies (VISTAS)},
  year         = {2025},
  type         = {B.E. Biomedical Engineering Project Phase II Report}
}
