# Sky Cipher: Drone Resilience & Mission Prediction

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Reinforcement Learning](https://img.shields.io/badge/RL-Reinforcement_Learning-red?style=for-the-badge)
![PyBullet](https://img.shields.io/badge/Simulation-PyBullet-green?style=for-the-badge)
![Streamlit](https://img.shields.io/badge/Dashboard-Streamlit-FF4B4B?style=for-the-badge&logo=Streamlit&logoColor=white)

Sky Cipher is a simulation and predictive analytics framework engineered to evaluate autonomous UAV navigation and mission resilience under Electronic Warfare (EW) and GPS-denied conditions. Combining Deep Reinforcement Learning (DRL) with PyBullet rigid-body physics, the platform simulates localized radio-frequency interference and assesses adaptive flight control strategies in contested airspace.

---

## Overview

In contested operational domains, unmanned aerial systems face severe signal degradation, spoofing, and loss of Global Navigation Satellite Systems (GNSS). Sky Cipher provides a framework to:

- Model spatial RF interference, communication degradation, and directional GPS-jamming patterns.
- Quantify mission completion probability using trained neural policy models.
- Evaluate autonomous evasive trajectories and alternate vision-based dead-reckoning routines when satellite telemetry drops.

---

## Core Architecture

### Simulation & Kinematics
- **Physics Engine:** Implemented with PyBullet to model 6-DOF (Degrees of Freedom) quadrotor aerodynamic behavior, thrust dynamics, and external disturbances.
- **Reinforcement Learning:** Continuous control policies trained to optimize trajectory planning and minimize signal attenuation exposure.
- **Flight Corpus:** Includes the labeled `SkyCipher Dataset`, cataloging telemetry records and state vectors classified across discrete flight states (nominal, evasive maneuver, and critical loss).

### Visual Navigation & Threat Identification
The `Vision_Detection` module uses **YOLOv8** to maintain autonomous visual tracking and obstacle avoidance. When electronic interference severs RF and satellite uplinks, visual odometry and object detection act as primary navigational fallback mechanisms.

### Automation Pipeline
Predictive outcomes interface with an **n8n** automation engine to route telemetry data and trigger alert payloads whenever the simulation detects path divergence or active jamming vectors.

![n8n Automation Workflow](https://github.com/user-attachments/assets/969b5561-5c8a-4876-a885-e6b8220c1b37)

---

## Directory Layout

```text
├── environment.py                    # PyBullet simulation environment and interference modeling
├── train.py                          # DRL model training loop
├── test.py                           # Policy evaluation and trajectory scoring
├── Vision_Detection/                 # YOLOv8 pipeline and AirSim integration routines
├── mission_control.py                # Streamlit dashboard for real-time telemetry tracking
├── threat_automation_pipeline.json   # Exported n8n workflow for telemetry alerts
├── dataset_images/                   # Multi-class labeled simulation frame sequence
└── drone_assets/                     # URDF descriptors and quadrotor mesh configurations
