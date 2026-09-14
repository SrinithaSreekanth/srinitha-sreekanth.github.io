# Facial EMG-Controlled Wheelchair – a Mobility Assistance for Quadriplegia

## Overview
This repository details the hardware and software architecture for a hands-free, cost-effective smart wheelchair designed for individuals with quadriplegia. The system captures and translates surface Electromyography (EMG) signals from specific facial muscles into real-time directional commands. By bypassing the need for upper limb functionality, this project provides a reliable alternative to traditional joystick-operated assistive devices.

## Key Features
* **Non-Invasive Control:** Utilizes surface electrodes placed on the cheeks to capture intentional facial gestures.
* **Real-Time Signal Processing:** Implements a 30Hz to 500Hz bandpass filter to eliminate physiological artifacts and electronic noise.
* **Wireless Transmission:** Employs an HC-05 Bluetooth module to send digital command signals to the hardware chassis[cite: 1].
* **Custom Threshold Mapping:** Leverages Digital Stair Plots, statistical parameters, and wavelet transform analysis to classify distinct facial movements[cite: 1].

## Hardware & Software Environment
* **Acquisition System:** BIOPAC MP45[cite: 1]
* **Microcontroller:** Arduino UNO[cite: 1]
* **Motor Control:** L298N Motor Driver Module, 12V 1.3AH SLA Battery, DC Motors[cite: 1]
* **Software Stack:** MATLAB Simulink, Arduino IDE (C++)[cite: 1]

## Movement Classification Mapping
| Muscle Activated | Target Gesture | Wheelchair Command |
| :--- | :--- | :--- |
| Left Buccinator | Left Cheek Movement | Left Turn[cite: 1] |
| Right Buccinator | Right Cheek Movement | Right Turn[cite: 1] |
| Zygomaticus Major | Smiling | Forward Movement[cite: 1] |
| Zygomaticus Major | Strained Expression | Backward Movement[cite: 1] |

## System Workflow
1. **Signal Acquisition:** Surface electrodes detect microvolt-level electrical activity from the targeted facial muscles[cite: 1].
2. **Processing & Digitization:** Analog signals are amplified, filtered, and digitized via the BIOPAC MP45 system[cite: 1].
3. **Feature Extraction:** The system calculates specific statistical parameters, including peak-to-peak amplitude, kurtosis, skewness, and signal area, alongside wavelet coefficients[cite: 1].
4. **Threshold Evaluation:** Features are compared against predefined threshold boundaries statistically validated by the Kruskal-Wallis test[cite: 1].
5. **Actuation:** If a feature falls within the active threshold range, a directional command is transmitted via Bluetooth to the Arduino UNO, which actuates the DC motors via the L298N driver[cite: 1].

## Results & Validation
* **Statistical Significance:** The Kruskal-Wallis test confirmed that extracted features (e.g., peak-to-peak, signal area) significantly differentiate between distinct facial gestures, minimizing misclassification[cite: 1].
* **Hardware Execution:** The 4WD prototype successfully demonstrated smooth, accurate mobility in all four directions without noticeable latency[cite: 1].
* **Stability Improvements:** High-torque motors and dedicated L298N motor drivers resolved early prototype issues related to jerky movements and load management[cite: 1].

## Publications & Presentations
* **CoaCoNS 2025:** Accepted for presentation at the Conference on Advances in Communication Networks & Systems, SRM Institute of Science and Technology[cite: 1].
* **NCRTAS 2024:** Presented at the 2nd National Conference on Recent Trends in Artificial Intelligence and Soft Computing, Bannari Amman Institute of Technology[cite: 1].

## Citation
```bibtex
@bachelorsthesis{srinitha2025facialemg,
  author       = {Srinitha S and Nivedha E and Ramya Bharathi S},
  title        = {Facial EMG controlled Wheelchair – a Mobility Assistance for Quadriplegia},
  school       = {Vels Institute of Science, Technology and Advanced Studies (VISTAS)},
  year         = {2025},
  type         = {B.E. Biomedical Engineering Project Phase II Report}
}
