# From Sensor to Server: Deployable Lightweight ML for IoT Intrusion Detection Across Network Layers

_Ariel J. N. Panopio, Hamza A. Abushahla, Ali Reza Sajun, Sameer Alawnah, Fadi Aloul, and Imran Zualkernan_

This repository contains code and resources for the paper: "[From Sensor to Server: Deployable Lightweight ML for IoT Intrusion Detection Across Network Layers](https://ieeexplore.ieee.org/abstract/document/11474516)".

<div align="center">
  <img src="figures/pipeline.jpg" height="350px" alt="E2E" />
</div>
<p align="center"><em>Figure 1: Proposed framework of the deployable ML-based IDS. The pipeline illustrates all stages—from data preprocessing to deployment of the models on selected hardware platforms. The hardware section is separated by a line to indicate the deployment level (edge, fog, cloud). Another line distinguishes classical ML models from DL models. Asterisks (*) denote stages where the models are utilized, including hyperparameter tuning, training & evaluation, and quantization.</em></p>


## 📌 Overview

This work presents a **deployable, lightweight machine learning (ML) framework for Intrusion Detection Systems (IDS)** designed to operate across **edge, fog, and cloud layers** of the IoT stack. Our key contributions are summarized as follows:

- We design a **multi-class, multi-tier anomaly-based IDS** that couples lightweight ML and DL models with the modern **RT-IoT2022 dataset**.
- We provide an **open and reproducible pipeline** that handles data cleaning, hyperparameter optimization, quantization, and cross-device testing, providing a baseline for future work.
- We conduct a **comprehensive hardware study** across edge, fog, and cloud nodes, mapping the trade-offs between speed, accuracy, energy, and memory.
- We perform an **end-to-end deployment comparison** of ONNX-based runtimes versus native C/C++ code generation, quantifying the *“convenience vs. performance”* trade-off across devices.
- We conduct a **comprehensive statistical analysis** that tests model superiority and the impact of quantization, utilizing appropriate paired comparisons and multiple-comparison control.
- We critically examine **inference time and space complexity analyses**, highlighting where asymptotic counts can be misleading on real hardware and providing practical caveats to align theory with measured latency and energy.
- We offer **evidence-based recommendations** on when training neural networks is warranted over classical ML for edge IDS, given accuracy, latency, and energy constraints.
- We analyze the **effects of quantizing already-small neural networks**, showing cases where INT8 can *increase* latency or power consumption despite memory savings.
- We propose **practical guidelines** for selecting window length, sampling rate, and flows per second (FlPS) to sustain reliable detection under live traffic.

---

## Dataset

We use the **RT-IoT2022 dataset**, released in 2024, which contains over 200,000 labeled network flows from real IoT devices such as Amazon Alexa, smart bulbs, MQTT sensors, and ThingSpeak modules. The traffic includes both benign communication (MQTT, HTTP, DNS, SSL) and eight attack types (SSH brute force, SYN Flood, Slowloris, ARP poisoning, and multiple Nmap scans). Data was captured in PCAP format with Wireshark and processed using Zeek with the Flowmeter plugin to extract 83 flow-level features for intrusion detection research.

## Models and Training
We formulate intrusion detection as a multi-class classification problem, aiming to detect attacks and identify their type. To cover a broad spectrum of approaches, we evaluated four classical ML models (SVM, Random Forest, XGBoost, LightGBM) and two lightweight DL models (a Fully Connected Neural Network and an AutoEncoder-Classifier). The classical models provide diverse strengths in regularization, ensembles, and efficiency, while the DL models enable compact yet expressive baselines with feature learning. All models were trained in FP32 using a standardized pipeline with automated hyperparameter tuning via Optuna to ensure fair and optimized comparisons.


## Quantization and Deployment
Deep learning models were quantized using **Quantization-Aware Training (QAT)** with the TensorFlow Model Optimization Toolkit (TFMOT). After cross-validation, each model was fine-tuned with annotated dense layers and fully converted to **INT8 precision** (weights, activations, inputs, and outputs). Both fold-specific and best-performing models were saved for deployment on resource-constrained edge hardware.


## Citation & Reaching out
If you use our work for your own research, please cite us with the below: 

```bibtex
@article{panopio2026sensor,
  title={From Sensor to Server: Deployable Lightweight ML for IoT Intrusion Detection Across Network Layers},
  author={Panopio, Ariel Justine N and Abushahla, Hamza A and Sajun, Ali Reza and Alawnah, Sameer and Aloul, Fadi and Zualkernan, Imran},
  journal={IEEE Internet of Things Journal},
  year={2026},
  volume={13},
  number={14},
  pages={30483-30517},
  publisher={IEEE},
  doi={10.1109/JIOT.2026.3680712}
}
```

You can also reach out through email to: 
- Hamza Abushahla - b00090279@alumni.aus.edu
- Ariel J. N. Panopio - b00088568@alumni.aus.edu
