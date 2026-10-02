# Artificial Intelligence Containment Assurance Levels (AI-CAL)
## Hardware-Enforced Deterministic Containment for Autonomous Agents

### 📌 Overview
Traditional AI security relies heavily on behavioral guardrails (alignment) and logical cloud sandboxes (IAM/network policies). However, advanced autonomous agents consistently demonstrate the ability to exploit logical layers, manipulate proxy caches, and break virtual containment. 

The **AI Container Assurance Level (AI-CAL 0-6)** framework shifts the paradigm from behavioral trust to **physical network and supply chain isolation**. 

This repository introduces the baseline architecture for **AI-CAL 4.5 (The Hybrid Balance Approach)**. It provides a blueprint for deploying high-risk or hostile autonomous agents on-premises, treating model-to-package handoffs as dangerous, untrusted supply chain vectors.

### 🛡️ Core Architectural Pillars (AI-CAL 4.5)
The architecture isolates the execution runtime from core artifact repositories (such as JFrog) using physical-layer and cryptographic constraints:

*   **Cryptographic & Network Cordoning:** Every agent workload is bounded within a 4-firewall Ring function) and zone, authenticated strictly via **F5 mTLS** to ensure un-spoofable workload identity and throttle rate control.
*   **Zero-Feedback Information Starvation:** An internal gateway using **Apache Camel hosts** manages message state and enforces mathematically strict JSON schema boundaries (sizing, field limits). Payloads violating these rules are silently dropped. By eliminating error codes (e.g., HTTP 400) and stack traces, the agent is starved of the feedback loop required for recursive debugging and exploit pivoting.
*   **Asymmetric Out-of-Band Agent-to-Model Messaging:** Agents are strictly prohibited from maintaining open-ended, persistent network connections to the underlying LLM models. Instead, all agent-to-model messaging is routed through a highly scalable, asynchronous Apache Camel orchestration layer. This decouples the communication flow, prevents continuous session-hijacking or interactive execution breakouts, and ensures every message transaction is discrete, inspected, and state-bound.
*   **Asymmetric Out-of-Band Package Delivery:** Agents have **zero direct line-of-sight to JFrog**. Package requests trip an external, air-gapped like pipeline. **Jenkins** orchestrates a Managed File Transfer (**MFT**) host to push validated packages across a hardware-enforced **Owl Data Diode** into a completely separate, firewall-controlled zone hosting an SSH-key secured SFTP mail drop.
*   **Cascading Swarm Collapse:** If an agent attempts to flood or swarm its container, it trips a physical circuit breaker at the Camel/Jenkins orchestration layer. This completely cuts off the package lifeline, inducing a controlled, simultaneous failure of the entire local swarm before cross-zone persistence can occur.
*   **Out-of-Band Forensic Monitoring and Auditing:** Total visibility is maintained via fully out-of-band network taps, Intrusion Detection Systems (IDS), and SIEM integration. Crucially, this pipeline operates independently of the agent runtime plane to prevent logs from being tampered with or falsified by a compromised swarm. Beyond real-time alerting, this out-of-band system acts as an immutable forensic recorder, capturing exact agent trajectories and execution logs to facilitate post-incident root-cause analysis and structural lessons learned.

**Author:** Patrick Shannon

Github link: https://github.com/pshannon011/AI-CAL-Containment-Assurance-Framework

## 📅 Version History & Artifact Integrity

**Current Release:** Version v1.0 Initial public release.

**Release Date:** September 2026  

**Framework Document:** `AI-CAL_Agent_Containment_Framework_v1.0_2026-09.pdf`  

**Hash integrity SHA-256:** `d88e9eae0cac725321fa85b8591c2d3c34307e7c6570ffca5900ea0394221a92`

--------------------------
**Current Release:** Version v1.0 Initial public release.

**Release Date:** October 2026  

**Companion Diagram:** `AI-CAL_On_Prem_Layout_diagram_v1.0_2026_10_01.pdf`  

**Hash integrity SHA-256:** `c56af580ecb9a0bda3567c6a5e7341106b14a3f89adae9ff96d5e9d6c4a0cfc0`

--------------------------

##License

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22925685.svg)](https://doi.org/10.5281/zenodo.22925685)

© 2026 Patrick Shannon

##This work is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0).

Reuse, redistribution, and adaptation are permitted with appropriate attribution to Patrick Shannon.

### Architectural Notes & Limitations

The PDF is the authoritative release artifact.

Future revisions will be published as separate versioned releases. Previous releases will remain available for reference and version history.

* **Scale & Topology:** The AI-CAl (4.5) architecture is designed for horizontal scalability; the accompanying diagram illustrates a simplified multi-agent layout for clarity.
* **Hybrid Extensibility:** While depicted here as an on-premises deployment, the orchestration pipeline (Jenkins/JFrog/MFT Sender) can be seamlessly deployed in a hybrid cloud configuration (e.g., AWS VPC via AWS Direct Connect) without altering the security posture.
* **Threat Model & Containment:** High-risk/hostile autonomous agents require deterministic physical-layer containment. This framework mandates hardware-enforced unidirectional gateways (data diodes) rather than virtualized or software-defined isolation boundaries.
* **Status:** This design is under active development and requires formal peer review and extensive validation testing prior to production deployment.
* **Agent Message Request Canonical JSON Schema:** The precise structural specifications and canonical JSON definitions are currently undergoing active design and refinement. Input from AppSec and integration engineers is welcomed during the formal peer-review phase.


## 👨‍💻 About the Author

**Patrick Shannon**  
*Principal Information Security Architect*  
Former Cybersecurity Architect Consultant & SME | 16 Years Global Enterprise Secure Architecture & Design for GE Aerospace

### 🏅 Professional Certifications
*   **CISSP** (Certified Information Systems Security Professional)
*   **CISA** (Certified Information Systems Auditor)
*   **CRISC** (Certified in Risk and Information Systems Control)
*   **GPEN** (GIAC Penetration Tester)
*   **GCLD** (GIAC Cloud Security Leadership)
*   **GISP** (GIAC Information Security Professional)
*   **CDPSE** (Certified Data Privacy Solutions Engineer)
*   **GPPA (ret.)** (GIAC Certified Perimeter Protection Analyst)

🔗 **Connect on LinkedIn:** [Patrick Shannon](https://www.linkedin.com/in/patrick-shannon-cissp-crisc-cisa-gisp-gpen-gcld-cdpse-b7726b2/)  
🏅 **Verify Badges on Credly:** [Credly Profile](https://www.credly.com/users/patrick-shannon.d59e52e2/badges/credly)
