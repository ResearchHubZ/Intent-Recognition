# SAM-LIR: Self-adaptive Multi-agent Collaborative Reasoning for Open-domain Latent Intent Recognition

[![Paper Status](https://img.shields.io/badge/Paper-Under_Review-yellow.svg)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

This repository contains the core reproducible components—including **Prompt Templates**, **Fuzzy System Configurations**, and **Sanitized Data Samples**—for the paper *"SAM-LIR: Self-adaptive Multi-agent Collaborative Reasoning for Open-domain Latent Intent Recognition"*, which is currently under review at *IEEE Transactions on Fuzzy Systems*.

## 🚀 Overview

Open-domain latent intent recognition faces extreme challenges due to vague user expressions and dynamically emerging intents. **SAM-LIR** tackles this by seamlessly integrating Large Language Models (LLMs) with formal mathematical Fuzzy Logic through a sequential multi-agent collaborative framework. 

Due to privacy restrictions associated with the real-world hotline data used in our experiments, the full raw dataset cannot be publicly released. To support **transparency and reproducibility**, this repository provides the exact inference configurations, the complete set of prompts used by our agents, and a strictly de-identified subset of the data.

---

## 🧠 Neuro-Symbolic Architecture: Bridging LLM Prompts and Fuzzy Math

SAM-LIR adopts a **Neuro-Symbolic paradigm**, decoupling semantic perception from mathematical fuzzy inference:

1. **The LLM as a Semantic Sensor (Prompt Layer):** Large Language Models are excellent at zero-shot semantic understanding but can be unreliable at formal mathematical calculations. Therefore, the Expert Prompts in our system require the LLM to output **raw heuristic signals** in JSON format (e.g., semantic `confidence_score` and `ambiguity_level`).
2. **The Mathematical Fuzzy Inference Layer (Code Layer):** Once the LLM outputs the JSON, the system extracts these raw numerical and categorical signals and feeds them into explicitly defined membership functions. For example:
   - The raw `confidence_score` acts as the input variable $x$, which is mathematically transformed into the final similarity-based membership degree $\mu^{(\text{sim})}_m(q)$ via a **Sigmoid function**.
   - The `ambiguity_level` triggers the **Exponential function** $\mu_{\text{unc}}(q)$ to compute the uncertainty penalty.
   - The Decision-Making Agent's aggregated outputs are ultimately subjected to the formal **Maximum-Membership Defuzzification** and a **Rejection Rule** ($\eta$) within the inference engine. 
   - Additionally, the system employs a **confidence-aware update strategy** to filter highly uncertain predictions before updating the dynamic Intent* Library.

By combining the semantic reasoning power of LLMs with the mathematical formulation of Fuzzy Systems, SAM-LIR ensures high open-domain adaptability and supports theoretical interpretability.

---

## 📂 Repository Structure

### 1. `prompts/`
Contains the exact prompt templates used for driving the multi-agent system:
- `1_intent_initialization_prompt.txt`: Generates abstract intent prototypes based on K-Means++ clusters.
- `2_expert_agent_generation_prompt.txt`: Dynamically generates expert agent profiles (domain, role, specific analytical recommendations).
- `3_expert_sequential_reasoning_prompt.txt`: Instructs experts to generate structured fuzzy evidence (`confidence_score`, `ambiguity_level`).
- `4_decision_maker_aggregation_prompt.txt`: Instructs the decision-making agent to perform confidence-weighted aggregation.

### 2. `configs/`
Contains the core hyperparameters used in our experiments:
- `sam_lir_config.yaml`: Explicitly maps the experimental parameters to the paper's mathematical formulation (e.g., Sigmoid slope $\alpha$, Gaussian diffusion $\sigma$, and the rejection threshold $\eta$). *Note: Parameters under `fuzzy_inference` correspond to the formal fuzzy inference layer in the manuscript; `system_parameters` are implementation-level settings used in the reported experiments.*

### 3. `data_sample/`
- `help_dataset_sanitized_sample.json`: A representative, de-identified subset of the private "Help" dataset. All Personal Identifiable Information (PII) has been removed or masked to demonstrate the data structure and our privacy-preserving mechanisms.

