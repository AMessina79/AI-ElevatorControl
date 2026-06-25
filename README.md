\# AI-ElevatorControl



A 3-stop hydraulic elevator controller integrating industrial PLC control with AI/ML-powered anomaly detection and predictive maintenance. Built as a resume project demonstrating the hardware-software bridge between industrial automation and modern data science.



\## Project Overview



This project combines a Rockwell Micro820 PLC for real-time elevator control with a Raspberry Pi data pipeline, MQTT communication layer, and machine learning model trained on operational data to detect anomalies and predict maintenance needs.



\## Hardware



\- \*\*Micro820 PLC\*\* (2080-LC20-20QBB) — core control logic via EtherNet/IP

\- \*\*Hydraulic pump\*\* — up/down control via 24V relay outputs

\- \*\*3x Shelly smart switches\*\* — call button relay inputs

\- \*\*3x LilyGO 4.7" e-ink touchscreens\*\* — per-floor UI via WiFi/MQTT

\- \*\*2x limit switches\*\* — upper and lower travel limits

\- \*\*Raspberry Pi\*\* — MQTT broker, data pipeline, ML inference

\- \*\*Metal enclosure\*\* — 24V and 12V power supplies, fused outputs



\## System Architecture



Physical Layer



├── Micro820 PLC (core control logic)



├── Hydraulic pump outputs (up/down)



├── 2x Limit switches



├── 3x Shelly smart switches (call inputs)



└── 3x LilyGO e-ink screens (floor UI)



↓



Communication Layer



├── PLC → EtherNet/IP → Raspberry Pi



├── Shelly → WiFi → MQTT broker



└── LilyGO → WiFi → MQTT broker



↓



Edge / Data Layer



├── MQTT broker (Mosquitto)



├── Data logger (Python/pycomm3)



└── Time-series data store



↓



ML Layer



├── Feature engineering (cycle times, dwell, call frequency)



├── Anomaly detection (Isolation Forest → LSTM)



└── Model inference on Raspberry Pi



↓



Presentation Layer



├── Dashboard (Grafana)



└── Alert system



\## Tech Stack



\- \*\*PLC Programming:\*\* Connected Components Workbench (CCW), Ladder Logic

\- \*\*Communication:\*\* EtherNet/IP, MQTT (Mosquitto), WiFi

\- \*\*Data Pipeline:\*\* Python, pycomm3, paho-mqtt

\- \*\*ML:\*\* scikit-learn, TensorFlow/Keras

\- \*\*Dashboard:\*\* Grafana

\- \*\*Embedded:\*\* Arduino/ESP32 (LilyGO displays)



\## Project Status



\- \[x] Hardware wired and powered

\- \[x] PLC communication established via CCW

\- \[x] GitHub repository and folder structure initialized

\- \[ ] Ladder logic — elevator sequencing

\- \[ ] MQTT communication layer

\- \[ ] LilyGO display firmware

\- \[ ] Raspberry Pi data pipeline

\- \[ ] ML model training and inference

\- \[ ] Dashboard



\## Background



Built by an industrial electrician and controls technician with 10 years of experience (Allen Bradley SLC 5, 500, ControlLogix 5000, Cognex vision systems, VFDs) and a graduate of an AI/ML bootcamp. This project bridges industrial automation with modern data science.

