# ACTOR_EVOLUTION.md

## Evolving the Agent Metadata Specification into a Unified Actor Metadata Specification

This document explains the evolution from an **agent-only** metadata model to a unified **actor** model that supports both AI agents and human actors.

It provides:
- a structural overview of the actor model,
- a conceptual JSON schema diff (`v1` agent root -> `v2` actor root),
- migration guidance for existing Agent Card users, and
- backward-compatibility notes.

> **Status note:** The repository already ships an actor-based schema (`schema/agent-metadata-schema.json`, title: "Actor Metadata Specification", version `0.3.0`). This document is intended as transition guidance for users coming from older agent-root payloads.

---

## 1) Structural Overview

The unified model uses a top-level `actor` object with a required type discriminator:

```json
{
  "actor": {
    "type": "agent" | "human",
    "identification": { "...common fields...": "..." },
    "configuration": { "...common fields...": "..." },
    "security": { "...common fields...": "..." },
    "relations": [ "..." ],
    "lifecycle": { "..." },
    "agent_profile": { "...agent-only fields...": "..." },
    "human_profile": { "...human-only fields...": "..." }
  }
}
```

This structure:
- unifies governance across humans and AI,
- supports mixed-initiative workflows,
- preserves room for future actor categories,
- and supports backward compatibility for legacy agent-root data.

---

## 2) JSON Schema Diff (Conceptual)

This section is a **conceptual diff** to illustrate the model transition. It is not a full normative schema.

### 2.1 Top-Level Object

**Before (`v1`)**

```json
{
  "agent": {
    "identification": { "...": "..." },
    "configuration": { "...": "..." },
    "security": { "...": "..." },
    "relations": [ "..." ],
    "lifecycle": { "...": "..." }
  }
}
```

**After (`v2`)**

```json
{
  "actor": {
    "type": "agent" | "human",
    "identification": { "...common...": "..." },
    "configuration": { "...common...": "..." },
    "security": { "...common...": "..." },
    "relations": [ "..." ],
    "lifecycle": { "...": "..." },
    "agent_profile": { "...agent-only...": "..." },
    "human_profile": { "...human-only...": "..." }
  }
}
```

### 2.2 Common Fields (Shared)

Typical shared governance fields include identity, ownership, environment, policies, and security controls:

```json
{
  "identification": {
    "id": "string",
    "name": "string",
    "role": "string",
    "owner": "string",
    "organization": "string"
  },
  "configuration": {
    "access_scope": "string | array",
    "policies": ["policy-id"]
  },
  "security": {
    "authentication": {
      "methods": ["password", "mfa", "pki"],
      "pki_certificates": [
        {
          "subject": "string",
          "issuer": "string",
          "serial_number": "string",
          "valid_from": "date-time",
          "valid_to": "date-time"
        }
      ]
    },
    "signing": {
      "supports_digital_signatures": true,
      "signature_schemes": ["XAdES", "PAdES", "JWS"],
      "key_management": "HSM | cloud_kms | local"
    }
  }
}
```

### 2.3 Agent-Only Fields

```json
{
  "agent_profile": {
    "model_info": {
      "name": "string",
      "version": "string"
    },
    "autonomy_level": "none | low | medium | high",
    "reasoning_model": "string",
    "memory_type": "string",
    "instructions": "string",
    "delegated_authority": [
      {
        "scope": "string",
        "delegated_by": "actor-id",
        "effective_from": "date-time",
        "effective_to": "date-time"
      }
    ]
  }
}
```

### 2.4 Human-Only Fields

```json
{
  "human_profile": {
    "employment_status": "employee | contractor | vendor",
    "department": "string",
    "job_title": "string",
    "training": [
      {
        "name": "string",
        "completed_at": "date"
      }
    ],
    "competencies": ["string"],
    "delegated_authority": [
      {
        "scope": "string",
        "limit": "string",
        "delegated_by": "actor-id",
        "effective_from": "date-time",
        "effective_to": "date-time"
      }
    ]
  }
}
```

### 2.5 Delegation Chains

**Static delegation context (actor metadata):**

```json
{
  "actor": {
    "relations": [
      { "type": "delegates_to", "target_actor_id": "actor-123" },
      { "type": "delegated_by", "target_actor_id": "actor-456" }
    ]
  }
}
```

**Dynamic execution context (event metadata):**

```json
{
  "event": {
    "performed_by_actor_id": "actor-123",
    "on_behalf_of_actor_id": "actor-456"
  }
}
```

---

## 3) Migration Guide for Existing Agent Card Users

### 3.1 Minimal Migration (Drop-In Compatibility)

Legacy agent cards can be wrapped with actor typing:

**Before**

```json
{
  "agent": { "...": "..." }
}
```

**After**

```json
{
  "actor": {
    "type": "agent",
    "identification": { "...mapped fields...": "..." }
  }
}
```

### 3.2 Recommended Migration (Full v2 Adoption)

| Old Path | New Path |
|---|---|
| `agent.identification.*` | `actor.identification.*` |
| `agent.configuration.*` | `actor.configuration.*` |
| `agent.security.*` | `actor.security.*` |
| `agent.relations` | `actor.relations` |
| `agent.lifecycle` | `actor.lifecycle` |
| *(new)* | `actor.type` |
| *(new)* | `actor.agent_profile.*` / `actor.human_profile.*` |

### 3.3 Human Actors (New)

```json
{
  "actor": {
    "type": "human",
    "identification": {
      "id": "EMP-001",
      "name": "Example User"
    },
    "human_profile": {
      "employment_status": "employee"
    }
  }
}
```

### 3.4 Deprecation Policy

- The legacy `agent` root object is **deprecated** and remains accepted for transition scenarios.
- New implementations should publish `actor` as the canonical root.
- Removal of legacy `agent` acceptance should occur only in a future major version with explicit migration notice.

---

## 4) Recommended Repository Artifacts

To support adoption, maintain:

1. **README.md**
   - Explain why actor governance extends beyond semantic mapping.
   - Clarify regulatory alignment boundaries (EU AI Act / ISO 42001 support vs full compliance).

2. **Enhancing_A2A_Protocol.md**
   - Keep mixed-initiative and delegation-chain guidance explicit.

3. **Examples**
   - AI actor example (`examples/AI Agent - Actor Format.json`)
   - Human actor example (`examples/Human Actor - Employee Card.json`)
   - Mixed delegation example (`examples/Mixed Delegation - Human and Agent.json`)

4. **Schema Versioning Notes**
   - Track migration milestones and deprecation timelines.

---

## 5) Summary

This evolution:
- unifies governance across human and AI actors,
- enables mixed-initiative attribution and delegation-chain reconstruction,
- strengthens accountability through identity/security/signing metadata,
- preserves backward compatibility while setting a clear forward path.

It shifts the standard from an agent card into a broader actor-governance model suitable for enterprise-scale oversight.
