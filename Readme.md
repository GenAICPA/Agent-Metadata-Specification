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
