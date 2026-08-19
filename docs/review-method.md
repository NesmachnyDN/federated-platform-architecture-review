# Architecture review method

This case uses a reusable review lens for distributed enterprise platforms. The method intentionally evaluates architecture operability, not only functional completeness.

## 1. Validate architecture intent against operating reality

Questions:

- Is the system actually one platform, or several installations with similar software?
- What must remain globally consistent?
- What may be local?
- Which functions must survive loss of central connectivity?

## 2. Separate control from execution

Check whether management responsibilities are explicit and distinct from business processing.

Control-plane concerns typically include:

- node registration and trust;
- desired state;
- policy/configuration delivery;
- compatible-version rules;
- lifecycle transitions;
- rollout/rollback;
- topology and compliance state;
- centralized audit/observability aggregation.

Execution-plane concerns include:

- business processing;
- API/service execution;
- data/content operations;
- event exchange;
- local buffering;
- local persistence required by the node profile.

## 3. Review node taxonomy and profiles

For every node type, define:

- purpose;
- mandatory capabilities;
- optional capabilities;
- data categories;
- trust boundary;
- connectivity assumptions;
- autonomy constraints;
- operations owner.

A node type is not useful if it is only a box name on a deployment diagram.

## 4. Review lifecycle and version governance

A distributed platform needs an explicit lifecycle:

- plan;
- register;
- establish trust;
- provision/connect;
- configure;
- assign services;
- update;
- verify;
- roll back when required;
- change operating mode;
- retire and revoke trust.

## 5. Review partition and autonomy semantics

Define what happens if a node temporarily cannot reach:

- the management node;
- another execution node;
- an external dependency.

For each condition, determine which local operations are allowed, which are blocked, what is buffered, and what reconciliation is required afterward.

## 6. Review data authority and synchronization

For each replicated data class or event stream define:

- authoritative source;
- replication direction;
- version semantics;
- idempotency rules;
- delivery acknowledgement;
- tolerated synchronization delay;
- conflict-resolution rule;
- recovery/replay behavior.

Avoid unspecified or universal "last write wins" conflict handling for business-significant state.

## 7. Review observability and audit

A distributed architecture should provide:

- local telemetry collection;
- buffering during disconnection;
- centralized consolidation;
- configuration/version drift detection;
- topology/connectivity state;
- explicit audit of administrative actions and autonomous periods.

## 8. Review operational responsibility

Separate responsibilities of:

- platform owner/operator;
- local infrastructure operator;
- security administration;
- application administration;
- incident response.

Architecture should make escalation boundaries visible before implementation.

## 9. Review failure containment

Ask whether failure of the management plane automatically causes failure of already-running business services.

A resilient platform usually requires:

- high availability for critical management services; and
- bounded independence of execution nodes using the last confirmed safe state.

## 10. Review change scalability

The final question is operationally simple:

> Can dozens or hundreds of nodes be safely upgraded, monitored and reconciled without turning every change into a manual local project?

If not, federation has not yet been fully designed.
