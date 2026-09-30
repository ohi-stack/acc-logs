# acc-logs

ACC Logs provides structured logging, observability, audit-event, trace, and monitoring support for the canonical ACC™ control plane.

## ACC V2 correlation model

Every provider-independent execution record should preserve correlation across:

```text
project_id
→ responsibility_id
→ work_order_id
→ workflow_id / task_id
→ provider
→ executor_ref
→ execution_id
→ approval_id
→ verification_id
→ deployment_id
```

This allows one operational objective to be reconstructed even when work crosses multiple agents, providers, tools, repositories, or human approval gates.

## Required logging principles

- Provider identity and maturity must be explicit.
- Reserved/non-executable providers must never generate false successful-execution records.
- Human decisions must remain attributable.
- Privileged actions must preserve approval and authority metadata.
- Execution outcome and verification outcome are separate fields.
- Merge, deployment, and production verification are separate events.
- Credential material must never be written to durable logs.

`openai-dot` is currently a reserved compatibility identifier. Any future Dot integration must emit the same work-order, provider, authority, verification, and audit correlation fields before it can be represented as operational in ACC.

**Synchronization target:** ACC `2.0.0-alpha.1` delegation foundation.
