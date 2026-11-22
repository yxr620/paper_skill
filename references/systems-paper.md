# Systems Paper Writing Reference

Use this reference for computer systems, data management, and ML systems papers aimed at venues such as OSDI, SOSP, USENIX ATC, EuroSys, NSDI, SIGCOMM, ASPLOS, SIGMOD, VLDB, CIDR, and MLSys.

## Acceptance-Level Priorities

A strong systems paper makes these relationships obvious:

- important problem -> current gap -> key insight -> concrete system design -> implementation reality -> evidence -> implication
- each contribution -> a section that explains it -> an evaluation result or qualitative justification that supports it
- each performance claim -> workload, metric, baseline, hardware/software setup, and experimental condition

Treat prose quality as a function of reviewer decision-making. The draft should help a skeptical expert answer:

- Why is this problem worth a top-tier paper?
- What is hard or surprising here?
- What is the core idea that changes the design space?
- What exactly was built or analyzed?
- Which claims are proven by which experiments?
- What are the limits, assumptions, and deployment constraints?

## Paper Map Template

Before major edits, form this compact map:

```text
Problem:
Gap in prior systems:
Key insight:
System / method:
Main contributions:
For each contribution: supporting evidence and conditions of validity:
Primary workloads and metrics:
Baselines:
Strongest evidence:
Known limitations:
Terms that must stay consistent:
Claims needing TODO/citation/evidence:
```

Do not include this map in the final answer unless the user asks for planning or diagnosis.

## Claim Discipline

Use precise claim levels:

- Observed: supported by code, experiments, logs, tables, figures, or draft text.
- Inferred: plausible from architecture or context, but not directly proven.
- External: depends on published work or external facts and needs citation.
- Missing: should be `TODO`, not invented.

Avoid unsupported words such as "optimal", "guarantees", "always", "negligible", "state-of-the-art", "significant", "novel", or "first" unless the draft supplies enough evidence.

Prefer measurable statements:

- Weak: "The system is much faster."
- Better: "The design reduces decode-stage overhead by TODO under the workload in Section X."

## Evidence and Claim Presentation

Apply these checks within the requested editing scope:

- **Evidence:** For central results, connect the comparison, conditions, metric, and magnitude to the claim they support. In result prose and captions, preserve aggregate definitions, uncertainty, and material exceptions; do not substitute a best case for a typical result or an inferred explanation for a demonstrated cause.
- **Novelty and confidence:** Locate novelty in a changed assumption, mechanism, or demonstrated capability. State measured outcomes directly; keep qualifications that express real uncertainty. Review hedges individually rather than deleting them globally or making every claim more cautious.
- **Scope:** Explain the common conditions that connect evaluated settings when the evidence supports that connection. Separate demonstrated coverage, reasoned extrapolation, and untested cases; neither generalize from a benchmark without support nor describe all findings as merely preliminary.
- **Revision control:** Resolve gaps in argument and evidence before polishing wording, then check factual and cross-section consistency. Identify missing research as such. When using AI feedback, require a passage and a checkable reason for each proposed change; a score increase alone is not a reason to keep rewriting. Stop when the scoped writing issues are resolved, and revisit only for concrete remaining problems.

Example with placeholders, to use only when supported by the draft:

> Under [condition], X reduces [metric] by [aggregate and value] relative to Y at the same [resource budget]. This supports [bounded claim]; [material exception] limits its applicability.

These editorial priorities are informed by [Li et al., arXiv:2608.08975, §§4–5](https://arxiv.org/html/2608.08975v1#S4). The study found greater AI-review sensitivity to evidence and novelty framing than to linguistic complexity. Its full-manuscript interventions on ICLR submissions do not establish sentence-level effects or gains in human review or actual acceptance. The checks above are a writing workflow, not a validated score-optimization recipe.

## Section Roles

### Abstract

Write in one tight arc:

1. problem and why it matters
2. missing capability or bottleneck in existing systems
3. paper's core idea
4. system or method name and what it does
5. evidence summary with concrete metrics when available, otherwise `TODO`
6. implication

Do not overload the abstract with all mechanisms. Include only the mechanism needed to understand the result.

### Introduction

Build reviewer commitment:

- Start from a concrete, current systems pressure.
- Explain why straightforward extensions of prior systems fail.
- Introduce the key insight before listing components.
- State contributions as claims the paper later proves.
- End with an evaluation preview that names workloads, baselines, and the strongest results when available.

Avoid a list of features before the reader understands the bottleneck.

### Background and Motivation

Use this section to teach only what the argument needs.

- Define workload properties, system constraints, or model behavior that drive design choices.
- Use measurements or examples to motivate bottlenecks when available.
- Separate established background from this paper's design choices.

### Design

For each design component, make the chain explicit:

```text
challenge -> design decision -> mechanism -> tradeoff -> why it works for this workload
```

Good design prose names boundaries: what runs online vs. offline, CPU vs. GPU, frontend vs. runtime, control plane vs. data plane, scheduler vs. executor, logical plan vs. physical execution.

### Implementation

Implementation sections should establish credibility, not dump code structure.

- Name the implementation substrate, language, runtime, kernels, storage layer, optimizer, or execution engine.
- Explain engineering details only when they affect correctness, performance, deployability, or reproducibility.
- Include version, hardware, deployment, and integration details when they matter to claims.

### Evaluation

Every evaluation subsection should answer one question.

Common questions:

- Does the full system improve the main metric over relevant baselines?
- Which component explains the improvement?
- How does performance scale with batch size, sequence length, data size, model size, concurrency, shards, nodes, or skew?
- What is the overhead of the new mechanism?
- Where does the approach break down?

Evaluation prose should tie figures back to claims:

```text
Figure X shows ... This supports Claim Y because ... The remaining gap comes from ...
```

Never invent missing numbers. Use `TODO` or describe the intended analysis.

### Related Work

Organize by technical relationship, not by paper list.

- Same problem, different assumptions
- Same mechanism, different target
- Same workload, different system layer
- Complementary techniques

Clearly state why prior systems do not make this paper unnecessary.

### Limitations

Limitations increase credibility when written concretely.

- State assumptions and unsupported cases.
- Explain whether limitations are fundamental, engineering debt, or evaluation scope.
- Avoid apologetic phrasing.

## Paragraph Revision

Before rewriting a paragraph, identify its job:

- motivate a problem
- state a claim
- explain a mechanism
- connect sections
- interpret a result
- compare against prior work
- describe a limitation

Then revise so the first sentence sets the job, the middle gives mechanism or evidence, and the final sentence advances the paper's argument. Keep terminology consistent with the paper map.

## Emphasis and Hedging

Reviewers read relative emphasis as a claim. Calibrate it to the evidence the draft actually has.

The common case: two factors, A and B, both affect outcome C, and the draft believes A matters more.

Without ablation or decomposition evidence, do not rank explicitly. Carry the difference through structure and verb strength instead.

```text
Too blunt: A is the important factor for C, and B matters less.
Paper-like: C is driven primarily by A, which <mechanism>. B also contributes, but its effect is confined to <condition>.
```

Give A a full mechanism sentence and, when available, a measurement. Give B a single clause that names its scope, boundary, or the regime where it becomes visible. Order carries as much weight as wording: whatever comes first and receives causal explanation is read as primary.

With ablation evidence, hedging becomes a weakness. State the split directly.

```text
Paper-like with evidence: Removing A costs TODO% of the improvement and removing B costs TODO%, so A accounts for most of the gain under <workload>.
```

Match the verb to the evidence level:

- `dominates`, `accounts for most of` — requires ablation or decomposition
- `is driven primarily by`, `is largely attributable to` — requires a clear measured gap
- `contributes`, `improves`, `reduces` — requires a directional measurement
- `also plays a role`, `is a secondary factor` — acceptable when the direction is observed but the magnitude is not
- `may`, `is intended to` — no measurement yet; pair with `TODO`

The same calibration applies to negative claims. "B is ineffective" requires evidence that B was measured and did not help. "B yields a smaller benefit under <workload>" usually does not, and is the safer sentence when only one workload was run.

## Style

Prefer:

- concrete nouns over vague abstractions
- active voice for design choices
- short technical sentences when introducing mechanisms
- explicit subjects for comparisons
- "because", "therefore", and "however" when logic matters
- formal systems-paper phrasing that names mechanisms, constraints, and evidence
- measured claims such as "reduces", "bounds", "amortizes", "exposes", "decouples", "profiles", "schedules", or "materializes" only when technically accurate

Avoid:

- sales language
- exaggerated novelty
- long strings of adjectives
- unsupported causal explanations
- paragraphs that mix motivation, design, and evaluation without transitions
- blog-style transitions such as "let's look at", "the key idea is simple", "it is easy to see", "in this post", or "we can just"
- tutorial language that teaches basic concepts not needed by an expert reviewer
- vague system praise such as "powerful", "seamless", "lightweight", "robust", "efficient", or "flexible" unless the sentence states the measured basis

## Blog-to-Paper Rewrite Pattern

Convert blog-like prose into claims that a systems reviewer can evaluate.

```text
Blog-like: The system smartly batches requests so the GPU is used much better.
Paper-like: The scheduler groups requests with compatible decode states, amortizing kernel launch overhead and increasing GPU occupancy under mixed-length workloads.
```

```text
Blog-like: This makes the design easy to deploy in real systems.
Paper-like: The design preserves the serving interface and confines online changes to the batching layer, so it can be integrated without modifying model definitions or client request formats.
```

If the evidence is missing, keep the claim narrow:

```text
Paper-like with missing evidence: The scheduler is intended to reduce decode-stage idle time under TODO workloads.
```

## LaTeX Editing

When editing LaTeX:

- Preserve `\label`, `\ref`, `\cite`, `\autoref`, macros, comments, and custom commands.
- Avoid changing bibliography keys unless explicitly asked.
- Do not rewrap entire files for cosmetic reasons.
- Respect local source style, including one sentence per source line when present.
- Check that introduced text does not require missing packages or new macros.
