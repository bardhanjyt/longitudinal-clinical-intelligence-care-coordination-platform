# Meridian

**Longitudinal Clinical Intelligence and Care Coordination**  
Governed agentic operating model · principal AI architecture

Meridian is not a clinical chatbot and not a workflow wrapper around a model. It is a versioned decision system. Longitudinal context, evidence, policy, model output, human authority, and external effects reconstruct as one governed chain.

The architectural unit is the `CareCoordinationDecisionRecord`, not a model turn.

**Architect:** Jyotirmoy Bardhan  
**Position:** deterministic workflow spine · bounded probabilistic reasoning · policy-mediated tools · immutable decision lineage · explicit abstention · accountable humans retain authority

Client, facility, and tenant names are omitted. Episode identifiers, release hashes, and people in the walkthrough are illustrative. They show the operating model. They are not production metrics.

---

## Walkthrough

Narrated decision-console film, **4 minutes 22 seconds**, 1600×900.

[Meridian-Care-Coordination.mp4](docs/Meridian-Care-Coordination.mp4)

The film is one post-discharge transition, played as a real console: cursor, clicks, and the gates a coordinator actually sees. It is the vertical slice of the architecture, not a tour of cloud products.

| What you see | What the architecture is enforcing |
| --- | --- |
| Signed release `REL-2026.09.18-E4`, hash `7f3ac91e4b28` | Compile once. Serve an alias. Models, prompts, policies, features, indexes, and agents move as one release. |
| Episode `EP-4418`, subject `sub_7f3a91`, discharged 14 hours ago | The episode was compiled without the outreach menu in view, so the queue cannot close itself. |
| Voice follow-up within 48 hours, `DRAFT_FOR_REVIEW` | Identity, consent, and eligibility passed. Policy passed. A person still has to approve the exact draft. |
| SMS nudge, `CONSENT_ABSENT` | Channel consent is absent, so the action is not ranked. A missing consent axis cannot be outvoted by a useful draft. |
| Close the transition, `ABSTAIN` | No scheduling receipt. A portal sentence is a contradiction, not a completed visit. |
| Clinical note write, `PROHIBITED` | The chart stays with the record of truth. Coordination does not author clinical documentation. |
| Opened policy gate | Pass, fail, or withheld is returned by deterministic policy. Nothing is ranked before identity, consent, and eligibility. |
| Rank beside calibration | Rank `0.74` is not a probability. Calibration sits beside it. Consent and safety are excluded from ranker features. |
| Evidence unit `EU-19802` | Retrieval keeps a contradiction quota. The disagreeing portal message stays in the dossier. |
| Path template `PT-TRN-FOLLOW-01` | The graph is a governed projection. Retrieval may walk only an approved template, inside hop and time budgets. A model may narrate the path. It may not invent one. |
| Late-event reconciler added in shadow | Workload identity, read-only authority, typed supersession set, token/step/time/cost caps, cycle detection. EHR write and open web stay locked. It can challenge a stale outreach. It cannot send one. |
| Human interrupt, decision `DR-2041` | Reason code, signer, release hash, and gate artifacts are appended. The click is not training data. A later correction supersedes the line. It does not erase it. |
| Handoff `HO-4418` | Outcome labels wait for the maturity window, deviations, and adjudication. Timeout after a mutation is `COMMIT_UNCERTAIN`, then an idempotency query, not a blind retry. |
| Alias rollback to `REL-2026.08.02-E2` | Rollback moves the serving alias. It is not an in-place migration and it does not delete either release. |

The same console is interactive. Command, Decisions, Evidence, Graph, Agents, Snapshots, Reconciliation, Records, and Autonomy are the surfaces. **Download MP4** in the header is this film.

---

## What this is, and what it is not

This repository publishes the architecture and a decision-console walkthrough of one consequential path.

It does **not** claim a measured ROI, a live EHR connection, or that the browser is the production substrate. The architecture is explicit on this point: capacity numbers come from measured arrival distributions, and no fabricated operational result is asserted.

Production, as specified, is a multi-tenant Azure platform. The console demonstrates the authority model those services have to enforce.

The platform coordinates, reminds, summarizes, and routes under approved content. It does not diagnose, prescribe, change treatment, or replace licensed judgement.

---

## Problem

Patient-facing and staff-facing work is fragmented across calls, messages, schedules, referral packets, discharge events, the EHR, care-gap files, and manual queues. Those sources disagree on identity, event time, authority, and completion.

A ticketing layer can route a task. It cannot decide whether the action is still applicable, whether consent permits it, whether a later event supersedes it, or whether an external write actually committed.

That is why rules-only automation fails, and why a chatbot fails differently:

| Failure | What the system has to do | Hard control |
| --- | --- | --- |
| Unstructured, multilingual input | Speech, extraction, entity resolution, grounded generation | Every extracted fact carries source, confidence, temporal scope, and validation |
| Incomplete, out-of-order longitudinal state | Temporal features and correction | Event time, availability time, and processing time stay distinct |
| Asymmetric risk | Models may recommend or draft | Identity, consent, safety, eligibility, and side effects are not prompt decisions |
| Labels that mature late | Exposure logs, point-in-time datasets, maturity windows | Future data and unexposed candidates cannot become labels |
| Conflicting evidence | Hybrid retrieval and bounded graph traversal | Retrieval score is not truth. Unsupported claims abstain |

### Non-negotiable constraints

- No foundation model owns canonical clinical, consent, identity, safety, or workflow state.
- The EHR remains authoritative for clinical documentation. The platform owns coordination workflow and reconciliation.
- Every external effect is typed, idempotent, attributable, policy-authorized, and recoverable from an uncertain commit.
- Autonomy is earned per tenant, intent, language, and action class, and it can decrease automatically.
- Models, prompts, agents, schemas, features, policies, indexes, and tools are versioned independently and can roll back.
- Patient and tenant isolation is enforced in identity, network, store, index, cache, feature, and telemetry. Not in prompts.

---

## Platform shape

Six bounded coordination products share one control plane, one durable workflow spine, one longitudinal state, one feature platform, and one governance plane. Shared intelligence does not mean shared mutable state. No agent becomes the system of record.

| Context | Aggregate | AI may contribute | Authority stays with |
| --- | --- | --- | --- |
| Call | Session, utterance, intent, disposition | Streaming ASR, language ID, extraction, grounded response | Telephony session and disposition policy |
| Visit | Slot, hold, appointment, confirmation | Constraint-aware ranking and clarification | Scheduling service and EHR reconciliation |
| Care gap | Measure instance, evidence status, outreach | Extraction, prioritization, response classification | Measure engine and source evidence |
| Transitions | Admission or discharge episode and follow-up | Event correlation and next-action proposal | Transition state machine and a human reviewer |
| Referral | Packet, checklist, destination, closure | Extraction, requirement analysis, destination ranking | Referral workflow and acknowledgement |
| Care management | Episode, tasks, goals, touchpoints | Longitudinal summary, task priority, draft outreach | A human-owned plan, with constrained automation |

| Plane | Owns | Substrate | Invariant |
| --- | --- | --- | --- |
| Edge | Ingress and protection | Front Door Premium, WAF, API Management, Communication Services | Identity, consent, and admission precede processing |
| Workflow | Timers, retries, waits, compensations | Durable Functions, Service Bus, Event Grid | Workflow history is authoritative |
| Agentic | Bounded planning and tool choice | Microsoft Foundry Agent Service, capability routes | Agents propose. Policy and tools authorize |
| State | Aggregates, idempotency, outbox, projections | PostgreSQL, Cosmos DB, Redis | One writer per aggregate. Versioned mutation |
| Knowledge and features | FHIR, corpus, graph, temporal features | Azure Health Data Services, Azure AI Search, ADLS Gen2 | Every projection rebuilds from canonical sources |
| Model and eval | Training, registry, endpoints, scorecards | Azure Machine Learning, MLflow, Foundry evaluations | Promotion requires linked evidence and a rollback target |
| Security and SRE | Identity, secrets, network, operations | Entra ID, Managed Identity, Key Vault, Private Link, Sentinel | No agent-held secret. Every PHI path is observable |

### Build versus rent

Differentiated control is built: timeline, decision record, autonomy policy, context compiler, tool contracts, feature semantics, evaluation sets, workflow state machines, EHR reconciliation, typed domain errors, and point-in-time learning.

Managed substrate is rented: identity, private network, model hosting, search, speech, storage, Durable Functions, Service Bus, API Management, Azure Machine Learning, and monitoring.

Workflows call capability names (`grounded-summary`, `outreach-draft`, `appointment-rank`). They never call deployment IDs. The gateway resolves capability, risk, region, data class, latency, and budget onto an already evaluated route. Model churn does not rewrite durable workflow.

---

## One decision

Ingress is normalized before it enters durable workflow. The model receives a signed, minimum-necessary context. Side effects run only in deterministic services, through policy-mediated tools, and are reconciled with the external source of truth.

```text
channels
  → Front Door / WAF → API Management → channel adapters
  → PostgreSQL + outbox → Event Grid / Service Bus → Durable Functions
  → policy + context compiler → Foundry agent task → APIM tool gateway
  → EHR / scheduling / outreach / referral
  → receipt + reconciliation
```

1. Authenticate the workload. Derive tenant, subject, purpose, channel, consent, and trace.
2. Deduplicate the envelope. Persist the source pointer and canonical fingerprint.
3. Load the aggregate at the expected version. Reject a stale command.
4. Compile eligible actions, required evidence, autonomy class, and permitted tools.
5. Compile exact facts, filtered retrieval, graph paths, and features into a signed context manifest.
6. Invoke the capability route with a deadline, schema, and token budget. Validate syntax, semantics, grounding, and policy.
7. If a person is required, create a durable interrupt. Revalidate on callback.
8. Invoke an idempotent tool. Persist request hash, external receipt, and commit state.
9. Reconcile the external authority. Append the decision. Mature outcomes without rewriting history.

Compile mode publishes immutable releases for model, prompt, policy, feature, corpus, index, and agent artifacts. Serve mode resolves only an approved compatible set. Rollback is an alias move to a known set, not an emergency rebuild.

---

## Agents, tools, and autonomy

Durable Functions owns anything that waits, compensates, mutates external state, or must replay. A Foundry agent is a bounded task: context selection inside policy, a typed proposal, a critique, or a tool-choice recommendation.

A supervisor is a finite graph router, not an unconstrained manager. Cycle detection hashes `(node, validated state, artifact set)`. Repetition terminates the run. One schema repair and one grounding repair are allowed. Budget exhaustion is `AGENT_BUDGET_EXHAUSTED`, never a partial success.

| Capability | Typed output | Maximum authority |
| --- | --- | --- |
| Intake normalizer | `NormalizedIntent` | Proposal only. Cannot merge identity |
| Longitudinal synthesizer | `LongitudinalSummary` | Read-only. No canonical mutation |
| Coordination planner | `CoordinationPlan` | Ranks admissible actions. Cannot execute |
| Evidence challenger | `DefectReport` | May block promotion. Cannot execute |
| Communication author | `OutboundDraft` | Draft only. Cannot send |
| Referral packet analyst | `ReferralPacketAssessment` | Cannot invent facts or close |
| Human-review clerk | `ReviewBrief` | Cannot approve |
| Policy gate | Non-model | Consent, identity, safety. Fail closed. Not overridable by a prompt |

The film adds one more capability, in shadow only: a **late-event reconciler**. It is bound to the released snapshot, classed with the evidence challenger, limited to read-only tools (`Timeline read`, `Evidence read`), and capped (tokens, steps, seconds, cost, one repair). Consent, identity, chart writes, and any open-web tool stay locked in the manifest. Shadow on save means it can challenge a stale outreach after a late event. It cannot send, close, or approve.

### Autonomy is calculated outside the model

The only results are:

| Class | Meaning on this platform |
| --- | --- |
| `AUTO_EXECUTE` | Only where scorecard, language, consent class, and override rate already allow it. A fresh discharge is not in this class. |
| `DRAFT_FOR_REVIEW` | The voice follow-up. The model may draft. A person approves an exact hash. Approval of this artifact does not authorize the next one. |
| `HUMAN_ONLY` | SMS, while channel consent is absent. The draft can exist. It cannot leave. |
| `PROHIBITED` | Closing without a receipt. Writing the clinical chart. Any open web tool. A prompt cannot promote a class. |

Live quality can reduce autonomy. Raising it requires reviewed promotion evidence. Calibration breach disables confidence-based automation. Raw model self-confidence is not a probability.

### Human interrupt

Review is a durable external event: review id, exact artifact hash, evidence manifest, options, reason code, reviewer role, expiry, and aggregate version. The callback revalidates consent, policy, state, and external availability. Approval of artifact N cannot authorize N+1.

In the film, the transition coordinator approves the voice draft with a structured reason and a note that the portal message is not a completed visit and SMS must not be sent. `DR-2041` is appended. History is not overwritten.

### Tools

Internal tools are versioned, MCP-compatible capabilities behind API Management. APIM checks managed identity, tenant and purpose claims, capability, schema, rate, payload class, and destination. There is no generic HTTP tool. Recipient identity comes from verified canonical state, never from generated text. Transitive tool authority does not cross an organizational boundary.

---

## Evidence, graph, and features

Search is an evidence-discovery projection. It is not authority. Raw EHR payloads are not embedded by default. Structured facts stay canonical. Indexed chunks keep source identity, subject, tenant, time, sensitivity, purpose, and deletion lineage.

Hybrid retrieval, in order:

1. Compile tenant, subject, purpose, time, and sensitivity filters **before** similarity.
2. Run BM25 and vector retrieval inside that set.
3. Fuse, rerank, and enforce source diversity and a contradiction quota.
4. Hydrate graph paths and structured facts from authoritative services.
5. Reject stale, superseded, unsupported, or inaccessible evidence.
6. Pack by authority and token budget. Emit a claim-to-source map.

GraphRAG projects patient, episode, interaction, appointment, referral, task, evidence, policy, provider, location, and decision. Queries use reviewed path templates with hop, row, and time budgets. Every edge hydrates to a source row. Similarity is never promoted to a completed visit. Graph centrality is not authority.

### Feature contract

A feature is a versioned contract, not a column name: entity keys, event time, availability time, source lineage, transform digest, freshness, null semantics, data class, permitted purposes, owner, version.

Online inference and offline training consume the same declared computation at different as-of times. A training row joins only values whose availability time is at or before the decision cut-off. Event time alone is not enough, because an older event may become known later. The compiler freezes the candidate universe, policy version, corpus cut-off, exposure probability, and label maturity.

Stale required features block autonomous use. Consent and safety are gates. They are not ranker features.

Ranking starts only after deterministic eligibility builds the candidate set. Unexposed actions are not treated as negatives. Rank, calibrated probability, and policy utility stay separate. The film shows that split on the voice action: a rank, an interval, and an explicit exclusion of consent from the model.

---

## Closed loop

There is no distributed transaction across the EHR, the communications provider, and platform state. Sagas persist intent, acknowledgement, and reconciliation. Delivery is at-least-once. Consumers commit inbox state with the aggregate mutation. If the EHR times out after a mutation, the workflow is marked `COMMIT_UNCERTAIN` and queried by idempotency key before any retry. The acceptance target is zero duplicate appointment or referral mutation.

An outcome is not a training label until the maturity window, deviations, and adjudication travel with it. Late corrections supersede. They do not rewrite the original decision. `latest` is forbidden in a decision record.

The handoff in the film binds the episode, the approved draft, the permitted channel (voice only), and the chain of custody. The call has not been placed. SMS is not in the package.

---

## Control plane, safety, and recovery

API Management is the only model egress. It checks workload identity and purpose, data-class eligibility, and rate, token, and cost quotas. It injects immutable trace and decision ids. Standard logs do not contain raw PHI prompts.

The router is not “pick a model”:

```text
candidate
  .where(capability)
  .where(schema-compatible)
  .where(data-class-approved)
  .where(region-allowed)
  .where(scorecard = APPROVED)
  .where(not expired)
  .order_by(risk-adjusted quality, deadline fit, marginal cost)
  .first_or_abstain()
```

No eligible route returns `NO_APPROVED_MODEL_ROUTE`. The workflow takes a deterministic template or a human path. It does not substitute an unevaluated model.

The context compiler emits a signed `ContextManifest`: tenant, subject, purpose, as-of, evidence with source, interval, authority, and hash, retrieval filters and ranks, omissions, redactions, token allocation, policy digest, manifest hash. System policy, structured facts, retrieved text, and user content stay in separate channels.

### Voice budget

Latency is recovered by speculative read-only work, streaming overlap, a compact sentinel, and deterministic acknowledgement. It is not recovered by sending first and validating later. Identity is never skipped. An unstable ASR partial may prefetch. It may not cause a side effect. Barge-in cancels synthesis with an epoch token so stale audio cannot play.

### Clinical and threat boundary

| Threat | Control |
| --- | --- |
| Prompt injection in a message, PDF, or retrieved chunk | Instruction and data stay separate. Evidence agents are read-only. Tool policy is independent. Outbound content is verified. No privilege expansion. |
| Cross-tenant disclosure | Tenant claim at identity, network, row-level security, search, cache, feature, and telemetry |
| Excessive agency | Allow-listed tools, expected version, idempotency, review |
| Evidence poisoning | Approved source, content hash, provenance, quarantine, corpus release |
| Denial of wallet | Step, token, retrieval, graph, tool, deadline, and money budgets |
| Supply chain | Pinned digest, signature, SBOM, scan, registry approval |

Typed denials an agent may not reinterpret include `IDENTITY_AMBIGUOUS`, `CONSENT_DENIED`, `EVIDENCE_INSUFFICIENT`, `CONTEXT_STALE`, `POLICY_DENIED`, `MODEL_ROUTE_UNAVAILABLE`, `HUMAN_REVIEW_REQUIRED`, `TOOL_COMMIT_UNKNOWN`, `EXTERNAL_STATE_CONFLICT`, `FEATURE_STALE`, and `TENANT_BOUNDARY_VIOLATION`.

### Degradation

Recovery is not “the endpoint returns 200”. It is workflow authority, decision lineage, external effects, and reconciliation back to a known consistent state. One active write epoch per tenant. If fencing is uncertain, the cell goes read-only.

| Dependency lost | Keep | Stop |
| --- | --- | --- |
| Foundry route | Deterministic workflow, templates, human queue | Free-form generation and agent promotion |
| Azure AI Search | Canonical fact lookup | RAG that required the missing evidence |
| EHR connector | Internal task and queued intent | Any assumption that the external write completed |
| Speech synthesis | Text or live transfer | Automated spoken response |
| Online feature store | Static eligibility and fresh last-known values | Ranking and autonomy that depend on stale features |

Hard controls fail closed. Identity, safety policy, kill switch, and audit intake replicate to the paired region and fail closed (`T0`).

### AI SLOs that change behavior

| Signal | Response |
| --- | --- |
| Decision trace incomplete | Block release |
| Grounded field support fails | Demote the capability or force review |
| Any hard-policy bypass | Fleet or intent kill switch |
| Retrieval sufficiency fails | Roll back corpus, index, or router |
| External effect not exactly once | Stop the tool and reconcile |
| Calibration fails | Disable confidence-based autonomy |
| Cost per verified workflow | Change route or context. Do not weaken safety |

Release vetoes, not exceptions: cross-tenant exposure, a bypassed forbidden action, an untraceable decision, missing rollback, evaluation leakage, a critical safety regression, unresolved uncertain commits, a non-replayable migration, or a tenant-derived artifact that cannot be deleted.

---

## Three calls that define the design

**Latency versus control.** Safety, consent, identity, and recipient checks stay on the critical path.

**Managed agents versus durable authority.** Foundry accelerates bounded reasoning. Workflow, business state, and external effects stay explicit. The extra contract surface is accepted so an agent loop cannot become the system of record.

**Personalization versus isolation.** Tenant style and policy are retrieval and configuration artifacts first. Shared training is opt-in and de-identified. Less pooled data is accepted so deletion and leakage boundaries can actually be enforced.

Every decision in the compendium states the authoritative state, the enforcement point, the telemetry, the kill switch, the rollback, the accountable human, the failure mode, and the condition that would reopen it. None of that may be inferred from model prose.

---

## Deliberately rejected

| Rejected | Why |
| --- | --- |
| One autonomous agent end to end | No replay, least privilege, termination, or external-effect semantics |
| Vector store as source of truth | Similarity has no transaction, temporal authority, or admissibility |
| Prompt-only safety or tenancy | Instructions are not authorization |
| One frontier model for every task | Cost, latency, and correlated failure |
| Active-active writes everywhere | Split-brain cost exceeds the need |
| Embed all EHR content | PHI, deletion burden, and irrelevant retrieval |
| Fine-tune before retrieval and evaluation are mature | Weights cannot repair a missing evidence contract or a missing label |
| Generic HTTP tool | Unbounded exfiltration and side effects |
| Post-filtering retrieval | Unauthorized content already entered memory, logs, and caches |
| Treating `latest` as a decision pin | A long-running episode must not change behavior mid-flight |

Policy-before-retrieval is not a preference. The ordering is not reopened. Only the implementation may change.

---

## Decision register

Thirty operating decisions. Each one has a failure mode and a reconsideration trigger in the architecture compendium. The short form:

| ADR | Decision |
| --- | --- |
| 001 | Durable workflow owns lifecycle. Agents are bounded tasks. |
| 002 | Capability-based AI gateway. Workflows do not bind to deployment IDs. |
| 003 | Minimum-necessary context is compiled and signed. |
| 004 | Policy precedes retrieval. Denied scope returns nothing, not a best effort. |
| 005 | Every tool is authorized deterministically. A model is not a policy decision point. |
| 006 | No generic HTTP tool. |
| 007 | Outbox, inbox, and uncertain-commit reconciliation. |
| 008 | One writer per aggregate. Stale mutation is `EXTERNAL_STATE_CONFLICT`. |
| 009 | Bitemporal facts. Corrections append. Decisions use an as-of cut-off. |
| 010 | Point-in-time feature and dataset compiler. Latest-value joins are leakage. |
| 011 | Search is a rebuildable projection. Never the source of truth. |
| 012 | Structured facts are not embedded by default. |
| 013 | Hybrid retrieval plus semantic reranking, with a contradiction budget. |
| 014 | GraphRAG uses reviewed path templates only. |
| 015 | Safety sentinel is independent of the authoring model. |
| 016 | Calibrated confidence controls autonomy. Logits are not probabilities. |
| 017 | Abstention is a successful terminal state. |
| 018 | Human approval binds an exact artifact hash. |
| 019 | Autonomy is retractable. Promotion stays deliberate. |
| 020 | Feature definitions are versioned contracts. Meaning is not mutated in place. |
| 021 | Ranking logs exposure. Unshown options are not negatives. |
| 022 | Labels mature. They never rewrite the decision. |
| 023 | Long workflows pin an artifact set. |
| 024 | Independent versions, with a compatibility matrix. |
| 025 | Shadow, then canary. Offline scorecards are not live behavior. |
| 026 | Observability is per decision, not per service uptime. |
| 027 | PHI stays out of standard telemetry. |
| 028 | Regional cells. One active write epoch. |
| 029 | Degradation is risk-tiered. Hard controls fail closed. |
| 030 | FinOps is per decision and per verified outcome, not per cloud invoice. |

---

## How an outcome is judged

No result number is claimed here. The measures that would justify a claim are tied to exposure, a mature outcome, and a guardrail: time to successful contact, time to scheduled follow-up, referral closure, completed tasks, no-show, staff handling time, override rate, opt-out, duplicate action, reconciliation debt, and cost per verified outcome.

Booking is not success when attendance, closure, or a completed follow-up was the point. A cheaper model route that increases review, error, or rework can cost more across the lifecycle. Routing optimizes quality-adjusted cost. Safety and access control are not cost knobs.

Where it is ethical and operationally real, incremental effect is estimated with stepped wedge, randomized timing, shadow ranking, or matched controls. Not with a demo anecdote.

---

## Acceptance

The platform is acceptable only when:

- every consequential action reconstructs from admissible evidence, exact artifacts, and workflow history
- every probabilistic component can fail without corrupting canonical state
- every uncertain external effect can reconcile
- tenant and patient boundaries live outside prompts
- operators can stop, degrade, recover, and roll back without trusting a model’s story about its own reasoning

A capability is not production-complete until its evidence path, authority boundary, failure semantics, observability, rollback, kill switch, deletion lineage, recovery behavior, and accountable owner are as concrete as its happy-path model call.

Production verification is a release input: replay parity, crash-point idempotency, concurrent approval, retrieval ACL and deletion, agent trajectory under tool denial and budget exhaustion, multilingual adversarial safety, cross-tenant probes, regional failover of pinned workflows, kill-switch drills, and a denial-of-wallet burst. Zero unexplained divergence. No duplicate consequential effect.

---

## Authority

Architecture owns cross-cutting contracts, quality attributes, isolation, lifecycle gates, resilience tiers, and the exception process. Product owns intent and experience. Clinical governance owns the clinical boundary. Security owns security policy. Data governance owns rights and retention. Service teams own implementation inside those guardrails. No owner can unilaterally weaken another owner’s hard control.

The architect does not approve clinical content, accept legal risk, or attest compliance. The role makes those authorities explicit in software, and impossible for an agent composition to bypass.

A veto cites the invariant, the evidence, the affected decisions, a safe alternative, and the exit criteria. It is an ADR or a risk item. It reopens when telemetry, threat evidence, regulation, or workload invalidates the assumption. Not when a demo looks simpler.

Delivery order is the control plane first: identity, network, and audit; canonical contracts and the event spine; durable workflow and reconciliation; retrieval and features; predictive models; bounded agents; autonomy; then the learning loop. A feature does not go concurrent until the control-plane dependency it needs is production-ready.

---

## Repository

| Path | What it is |
| --- | --- |
| `README.md` | This file |
| `docs/Meridian-Care-Coordination.mp4` | Narrated walkthrough, 4:22 |
| `docs/Longitudinal-Clinical-Intelligence-Principal-AI-Architecture.pdf` | Full architecture: problem, reference model, agent fabric, features, control plane, retrieval, speech, LLMOps, resilience, stack, thirty ADRs, verification matrix |

The interactive console, if you are running this repository, is a local decision-surface simulation of the transition slice above. It is useful for walking the gates, the evidence dossier, the path template, the agent contract, the human interrupt, and the append-only record. It is not the Azure cell, and it must not be loaded with real patient data.

---

## License and use

Architecture and walkthrough © Jyotirmoy Bardhan. All rights reserved.

Do not treat illustrative subjects, ranks, or release hashes as operational evidence. Do not connect this console to a clinical system of record.
