# Enhancing Google Agent2Agent (A2A) Protocol with Actor Metadata

The Google [Agent2Agent (A2A)](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/) is an open protocol that provides a standard way for agents to collaborate with each other. Agents advertise their capabilities using an "Agent Card" in JSON format.

The **Actor Metadata Specification** seeks to enhance the Google Agent Card by generalizing it to support both AI Agents and Human Actors, ensuring unified governance in mixed-initiative workflows.

### Unified Identity and Attribution

In an AI-driven enterprise, actions are often the result of collaboration between humans and agents. This specification enables:
- **Identity Binding:** Linking actions to verified identities (human or AI) using digital signatures and PKI.
- **Granular Attribution:** Tracking who initiated, performed, and approved every event.
- **Workflow Context:** Providing the necessary context for actions within complex delegation chains.

### Key Examples

See examples for the Actor Metadata Specification implemented for:
- [AI Agent - Actor Format](./examples/AI%20Agent%20-%20Actor%20Format.json)
- [Human Actor - Employee Card](./examples/Human%20Actor%20-%20Employee%20Card.json)
- [Mixed Delegation Chain](./examples/Mixed%20Delegation%20-%20Human%20and%20Agent.json)

### Backwards Compatibility

For existing Agent-only implementations, the specification maintains a deprecated `agent` root object. New implementations should adopt the `actor` root with the appropriate `type` discriminator.
