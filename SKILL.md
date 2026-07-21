---
name: paper
description: Write, edit, revise, polish, restructure, translate, or review academic research papers and paper drafts using rigorous computer-systems academic prose rather than technical-blog, tutorial, marketing, or casual explanatory language. Especially for systems and database venues such as OSDI, SOSP, USENIX ATC, EuroSys, NSDI, SIGCOMM, ASPLOS, SIGMOD, VLDB, CIDR, and MLSys. Use for full papers, LaTeX/Overleaf projects, Markdown drafts, abstracts, introductions, related work, evaluation sections, rebuttals, figure captions, individual paragraphs, wording tweaks, and Chinese-English academic prose refinement. Use even for small paragraph edits because the skill requires building full-paper context before local changes.
---

# Paper

## Core Rule

Build a paper-level mental model before changing prose.

For any nontrivial edit, inspect enough of the surrounding draft to understand:

- target venue or paper genre
- one-sentence problem statement
- core insight and system or method
- claimed contributions
- evaluation claims and available evidence
- terminology, notation, and section narrative
- known TODOs, missing numbers, and citation gaps

If the user only provides an isolated paragraph and no surrounding files are available, state that limitation briefly, infer the paragraph's likely role, and keep the edit conservative.

## Workflow

1. Locate the paper source.
   Prefer explicit user paths. Otherwise look for nearby `paper/`, `overleaf/`, `main.tex`, `*.tex`, `*.bib`, `draft/`, or Markdown paper files.

2. Read for global context first.
   For LaTeX projects, start from the root file, section inputs, abstract, introduction, conclusion, and the specific section being edited. Preserve labels, refs, citations, comments, macros, and formatting conventions.

3. Make a compact paper map.
   Keep the map internal unless the user asks for it. Track the paper's thesis, contribution list, important terms, evidence status, and how the target passage should function in the paper.

4. Edit with claim discipline.
   Do not invent benchmark numbers, baselines, hardware details, user-study results, or citations. Mark missing values as `TODO` or keep existing placeholders. Separate what the draft demonstrates from what it merely motivates.

5. Preserve global consistency.
   Reuse the paper's established terms and contribution framing unless changing them is the requested task. If a local rewrite changes a claim, check nearby abstract, intro, evaluation, and conclusion text for required follow-through.

6. Deliver the requested artifact.
   If editing files, keep diffs scoped. If returning prose, provide the revised text directly and mention major semantic changes only when useful.

## Academic Voice

Write and revise in the register of top-tier computer systems papers.

Use language that is:

- precise about system mechanisms, assumptions, workloads, and evidence
- restrained about novelty and impact
- explicit about causal links between bottlenecks, design choices, and measured results
- concise enough for expert reviewers, without tutorial-style explanation
- consistent with the paper's established terminology and contribution framing

Avoid language that sounds like:

- a technical blog post explaining a concept to beginners
- product marketing or launch copy
- documentation or how-to instructions
- casual commentary about what the system "can easily" do
- broad claims without experimental or architectural support

When polishing, optimize for reviewer trust rather than readability alone. A sentence is better if it states a narrower claim with clear evidence than if it sounds smoother but becomes less defensible.

## Academic Rhetorical Control

Do not flatten academic intent into blunt labels. When one factor is primary and another is secondary, express the difference through structure: put the primary factor earlier, give it more causal depth, mechanism, and evidence, and present secondary factors as constraints, boundary conditions, tradeoffs, or shorter supporting sentences. Avoid explicit rankings such as "A is important and B is less important" unless the paper has direct evidence for that ranking.

When positioning against prior work, prefer assumption, scope, workload, or system-boundary contrasts over blanket negative claims. Avoid writing that existing systems "cannot" or "fail to" handle a problem unless the paper directly proves it. Instead, state what prior systems optimize for and what mismatch this paper exploits or addresses.

Frame contributions as defensible claims, not component lists. A scheduler, cache, runtime, or optimizer is usually a mechanism; the contribution is the technical property, design separation, workload insight, or measured capability that the mechanism establishes.

## Section Direction and Cross-References

Avoid forward references from design, mechanism, background, or implementation prose to later evaluation sections, figure placeholders, or experiment labels such as "E3" and "E4".
Do not write sentences like "Section X will evaluate this", "E3 shows this", or "we verify this in the evaluation" in the main body before the evaluation section.
Instead, end a design subsection with the local claim the mechanism makes measurable, the workload condition under which it applies, and any assumptions or boundaries.
Keep evaluation plans, baseline lists, and experiment labels in evaluation drafts, TODO notes, comments, or the evaluation section itself.

## Task Modes

- Drafting a new section: read `references/systems-paper.md`, then write from the paper map and existing evidence.
- Revising a section: identify the section's job in the whole paper, then improve structure, transitions, claims, and evidence alignment.
- Editing one paragraph: read the full paper or surrounding section first when possible, then revise the paragraph for its local role.
- Polishing wording: improve precision, flow, and reviewer readability without changing technical meaning.
- Reviewing writing: lead with issues that affect acceptance, such as unclear problem framing, unsupported claims, weak evaluation linkage, inconsistent terminology, or missing threat/limitation discussion.
- Translating Chinese/English paper prose: preserve technical meaning and venue style; avoid literal translation when it hurts clarity.

## Systems Paper Standard

For systems/database venues, prefer concrete mechanism-and-evidence prose over marketing language.

Load `references/systems-paper.md` when:

- drafting or substantially revising abstract, introduction, design, implementation, evaluation, related work, or conclusion
- adapting text for OSDI, SOSP, ATC, EuroSys, NSDI, SIGCOMM, ASPLOS, SIGMOD, VLDB, CIDR, or MLSys
- evaluating whether the narrative, claims, contributions, or evidence are strong enough
- giving writing feedback beyond surface-level grammar

## Output Discipline

- Keep edits technically defensible and aligned with available evidence.
- Prefer direct, precise sentences over inflated claims.
- Maintain one concept per paragraph unless the existing venue style suggests otherwise.
- For LaTeX, avoid unnecessary reflow and preserve one complete prose sentence per source line when the repository asks for it.
- When unsure whether a claim is supported, weaken it or mark the missing support explicitly.
