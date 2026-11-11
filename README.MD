# AI Containment Assurance Levels (AI-CAL)

AI-CAL is an **AI agent containment framework and security reference architecture** for autonomous AI systems. It helps architects choose a containment level for a workload, design boundaries that limit what an agent can reach or do, and identify the evidence needed to support an assurance claim.

The core question: **If an agent or a control inside one zone is compromised, what can the agent still reach, and what keeps the failure from spreading?**

## Current release: AI-CAL v2.0

**November 2026** · [View the AI-CAL v2.0 framework PDF](./AI-CAL_Agent_Containment_Framework_v2.0_2026-11.pdf)

**SHA-256:** `ba8b916d0b883847ab25993c0608757effbc2a8e4949e022eb82dec5217f5ba2`

The versioned PDF is the authoritative release artifact. Compare its SHA-256 digest with the value above to verify the downloaded file. See [GitHub Releases](https://github.com/pshannon011/AI-CAL-Containment-Assurance-Framework/releases) for release history.

## Containment assurance levels and reference architecture

AI-CAL proposes containment assurance levels from **0 to 6**. The appropriate level depends on the workload, its exposure, and the consequences of a failure. The framework uses **AI-CAL 4.5** as an intermediate reference profile: separate physical host pools for agent execution and trusted mediation, narrowly authorized crossings, and hardware data diodes for defined one-way paths.

The v2.0 reference architecture defines:

- **Containment rings and tollgates.** Each crossing permits only an approved operation. Where a protocol break is required, the receiving side starts a separate, authenticated exchange. Assess shared administration and other dependencies before counting two boundaries as independent.
- **Brokered model access.** F5 terminates the agent's mutual TLS (mTLS) session. Apache Camel #2 records admission before F5 releases the request; Camel #1 verifies the signed request after the forward transfer. Camel #2 verifies the signed model result and binds it to the original agent and transaction before release.
- **Controlled package delivery.** Agents request packages through an approved catalog. Jenkins and JFrog handle acquisition; managed file transfer (MFT) sends approved artifacts through a separately governed one-way service to a scoped SFTP landing. Pickup uses SSH public-key authentication only. Per-agent mailboxes on a shared host do not establish containment if that host can modify or relay files across cells.
- **Fail-closed enforcement and monitoring.** Block forwarding when required admission or verification is unavailable. Define how to stop active and queued work, and use independent monitoring to assess whether each boundary and cutoff worked.

## Verification and related security guidance

AI-CAL distinguishes the containment required for a workload from the level and capacity demonstrated by a deployment. Version 2.0 shows how the CSA AI Controls Matrix (AICM) and OWASP AISVS can inform control selection and verification tests. It also identifies CSA STAR for AI self-assessments as a source for reviewing which controls a provider reports for a hosted service and who is responsible for them. For example, test that a tool broker denies actions outside the agent's authorization, then check that the agent has no direct path to the tool.

The reference architecture is conceptual. A limited prototype exercised part of the F5 and Camel message sequence with simulated components. A deployment claim requires evidence for the actual boundaries, shared dependencies, failure conditions, and workload capacity.

## Previous release

- [AI-CAL v1.0 framework PDF](./AI-CAL_Agent_Containment_Framework_v1.0_2026-09.pdf) · September 2026
- **SHA-256:** `d88e9eae0cac725321fa85b8591c2d3c34307e7c6570ffca5900ea0394221a92`
- [GitHub release v1.0.1](https://github.com/pshannon011/AI-CAL-Containment-Assurance-Framework/releases/tag/v1.0.1) · [Zenodo record for the earlier publication](https://doi.org/10.5281/zenodo.22925685)

## Companion materials

These diagrams and slide decks retain their original versions and publication dates. Use the v2.0 framework PDF for the current requirements.

| Artifact | Date | SHA-256 |
| --- | --- | --- |
| [On-premises containment architecture diagram v1.0](./AI-CAL_Agent_On_Prem_Layout_diagram_v1.0_2026_10_01.pdf) | October 2026 | `c56af580ecb9a0bda3567c6a5e7341106b14a3f89adae9ff96d5e9d6c4a0cfc0` |
| [Containment diagram walkthrough v1.0](./AI_CAL_Containment_Diagram_Presentation_v1.0_2026_10_08.pdf) | October 2026 | `55cb65caac22b4114509793eaf0b3899ac170d69605a54fb54d00e231af33a69` |
| [AI-CAL controls presentation v1.0](./AI-CAL_controls_presentation_v1.0_2026-11.pdf) | November 2026 | `cb4f67ed4f85272935077f8c39af9777e560b9db3b7562e72ae06f1aacb16d00` |

## License

© 2026 Patrick Shannon. Licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](./LICENSE). Reuse, redistribution, and adaptation are permitted with appropriate attribution.

## About the author

**Patrick Shannon** is a Principal Information Security Architect. He spent 16 years supporting global enterprise security architecture and design for GE Aerospace as a cybersecurity architecture consultant and subject matter expert.

**Certifications:** CISSP, CISA, CRISC, GPEN, GCLD, GISP, CDPSE, and GPPA (ret.).

[Patrick Shannon on LinkedIn](https://www.linkedin.com/in/patrick-shannon-cissp-crisc-cisa-gisp-gpen-gcld-cdpse-b7726b2/) · [Verify professional badges on Credly](https://www.credly.com/users/patrick-shannon.d59e52e2/badges/credly)
