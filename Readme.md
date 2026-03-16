# Actor Metadata Specification

## Introduction

Both AI agents and human actors are multiplying across the enterprise, taking actions that affect systems and data. While AI agents often create "shadow actions" due to a lack of visibility, human actions are often fragmented across multiple disparate systems (IAM, HR, SSO, etc.).

The **Actor Metadata Specification** provides a unified, cross-platform, event-level record of what an actor—whether human or AI—actually did, with the same granularity and governance standards.

<p align="center">
  <img src="./assets/images/Silent%20Proliferation.png" alt="Silent Proliferation" width="600">
  <br>
</p>

## Unified Actor Governance

AI agents and human actors share several governance needs:
- Both take actions that affect systems and data.
- Both can have privileges, scopes, and access rights.
- Both can cause harm, errors, or fraud.
- Both need to be monitored for compliance and auditability.
- Both operate across multiple systems and platforms.
- Both require identity, provenance, and accountability metadata.

By unifying human and agent metadata, organizations can bridge the gap between traditional identity systems and the new world of autonomous agents.

## Why Actor Metadata Matters

1. **Mixed-Initiative Workflows** – Real-world workflows involve humans prompting agents, agents acting on behalf of humans, and humans reviewing agent outputs. Unified logging allows for full reconstruction of who initiated, approved, and executed an action.
2. **Delegation Chains** – Agents can act on behalf of humans or other agents. Actor metadata allows organizations to reconstruct complex delegation chains (e.g., Human → Agent A → Agent B → System Action).
3. **Symmetry in Accountability** – Governance collapses if AI is held to a higher standard of traceability than humans. This specification ensures event-level accountability for all actors.

## Why This Is Not Just a Semantic Mapping Problem

Traditional ERP and data-integration standards (XBRL GL, SAF-T, ISO 21378, AICPA ADS) remain critical for interoperability, but they solve a different class of problem: **data meaning and exchange**.

Actor governance addresses what semantic standards were not designed to capture:

1. **New governance objects** – AI agents are autonomous actors with goals, decision policies, and execution privileges.
2. **Digital insider risk** – agents can take high-impact actions with broad system access.
3. **Shadow action visibility gaps** – organizations may not know which agents exist, who owns them, or where they run.
4. **Lifecycle metadata requirements** – governance needs creator, owner, deployment, version, policy, and monitoring metadata.
5. **Non-deterministic behavior** – model-driven outputs require behavioral traceability and audit context.
6. **Cross-platform operation** – actors span SaaS, hyperscalers, APIs, and chained agent ecosystems.
7. **Risk-oriented controls** – enterprises need risk scoring, privilege analysis, and continuous monitoring.
8. **Dynamic runtime governance** – behavior can change with retraining, re-prompting, model updates, and auto-deployment.
9. **Explicit accountability metadata** – responsible owners, policy owners, and stewards must be encoded.
10. **New audit evidence categories** – prompt logs, model versions, action traces, guardrails, and execution context are first-class evidence artifacts.

In short: semantic standards explain **what data means**; actor metadata explains **who acted, with what authority, under which controls, and with what outcome**.


## Regulatory Alignment and Compliance Boundaries

### Does this specification satisfy the EU AI Act by itself?

**No, not by itself.** The Actor Metadata Specification is a foundational control that provides evidence, traceability, and accountability metadata needed to operationalize compliance. Legal compliance still requires organizational controls, governance processes, risk treatment, testing, and conformity activities beyond metadata alone.

### EU AI Act Alignment (supporting control layer)

The specification is designed to support key obligations commonly associated with high-risk AI governance, including:
- **Documentation and system identification** (technical file inputs such as purpose, ownership, architecture context, model/version details).
- **Logging and traceability** (event-level action logs, execution traces, access and privilege metadata).
- **Risk management and monitoring** (inputs for risk scoring, incident analysis, and ongoing oversight).
- **Human oversight and accountability** (clear owner/steward mapping and delegated-responsibility chains).
- **Lifecycle governance** (deployment context, change history, and version-aware control evidence).

### ISO/IEC 42001 Alignment (AIMS enablement)

The specification also supports implementation of an AI Management System by enabling:
- inventory-level visibility of actors and deployed systems,
- explicit role and ownership metadata,
- operational monitoring evidence, and
- change-management/audit artifacts.

### Additional compliance requirements for Human/AI hybrid work

Organizations running mixed human+AI workflows typically need controls beyond AI-specific frameworks, for example:
- **Privacy and data protection** (e.g., GDPR/UK GDPR, data minimization, lawful basis, retention, data-subject rights).
- **Identity and access governance** (least privilege, separation of duties, privileged access monitoring).
- **Security and resilience** (e.g., ISO 27001, NIS2/DORA where applicable, incident response and business continuity).
- **Model risk and third-party risk management** (provider due diligence, model change governance, validation).
- **Sector-specific obligations** (financial services, healthcare, critical infrastructure, and public-sector regulations).

In practice, this specification should be implemented as a **cross-platform metadata backbone** that feeds legal, risk, security, and audit control processes rather than replacing them.

## Enhancing Google Agent2Agent (A2A) Protocol

The Google [Agent2Agent (A2A)](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/) provides a standard for agent collaboration. The Actor Metadata Specification enhances this by adding business context, risk management, and human-in-the-loop governance.

While the original proposal focused on AI agents, this specification generalizes to an **Actor Metadata Specification** covering:
- Actor identity (human or AI)
- Actor privileges
- Actor actions
- Actor lifecycle
- Actor accountability and provenance

## Importance of Actor Metadata Standards

By implementing this robust specification, enterprises gain:
- **Unified Enterprise-Wide View:** A consolidated, holistic view of all actors (human and AI) across the organization.
- **Enhanced Accountability:** Rigorous capture of ownership and delegation, ensuring clear accountability.
- **Automated Risk Management:** Systematic risk analysis applied across all business processes.
- **Digital Signatures and Integrity:** Utilizing digital signatures for non-repudiation and identity binding.

## Actor Metadata Producers and Consumers

A wide range of platforms produce or consume actor metadata, including Hyperscalers, LLM Providers, HR Systems, IAM/SSO platforms, and GRC (Governance, Risk, and Compliance) platforms.

---

### Legacy Support
*Note: The `agent` root object is still supported for backwards compatibility but is deprecated in favor of the `actor` object.*


### Evolution Guide
For schema transition details, see [`ACTOR_EVOLUTION.md`](./ACTOR_EVOLUTION.md), including conceptual diffs and migration paths from legacy `agent` roots to canonical `actor` roots.
