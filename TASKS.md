# Know-Your-Rights — TASKS.md

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

Backlog for **Know-Your-Rights** (slug: `know-your-rights`), a neutral, primary-source-cited public
**legal-information** commons (tenant → worker → civil rights) published as open content (CC-BY) plus
a machine-readable dataset — always **information, not legal advice**, **jurisdiction-sourced**, and
**licensed-attorney reviewed**. See `PLAN.md` for full context.

The **neutrality / non-advice / UPL editorial policy is the first build item** and a hard product
requirement. This is a **HIGH risk-tier** project on its legal-content surface: any task that states
a right, a legal rule, or a jurisdiction-specific obligation requires **sign-off by a licensed
attorney admitted in the jurisdiction** before it ships. No partner, distribution channel, or
attorney reviewer is yet secured, so delivery-dependent tasks carry `requestor: TO BE SECURED` and
`verifiedNeed: false`.

## How these tasks map to Elyos

Each task below becomes an Elyos **Task JSON** validated against `packages/schema/src/schemas.ts`.
Field mapping:

- **id** — stable slug `know-your-rights-<area>-NNN` (e.g. `know-your-rights-policy-001`).
- **title** — the task title in the milestone table.
- **project** — `know-your-rights`.
- **type** — one of `code | research | writing | data | design-spec | maintenance`.
- **lane** — `donated` (default; no funded tasks planned. Any `funded` task must add
  `fundedBudgetUsd` with a hard cap).
- **priority** — `high | medium | low`.
- **domain** — array, e.g. `["legal","civic","tenant-rights","access-to-justice","content"]`.
- **riskTier** — `low | medium | high`. Anything stating a right / legal rule / jurisdiction-specific
  obligation is `high`; source-vetting and currency tasks are `medium`+; pure pipeline/site/infra is
  `low`.
- **urgent** — boolean (no urgent tasks at cold-start).
- **deliverable** — `pr | dataset | document | translation`.
- **tokenEstimate** — `small | medium | large` (maps to the Size column).
- **status** — `open | in-progress | review | delivered | done` (all start `open`).
- **context / objective / acceptanceCriteria[] / resources[] / output** — per task.
- **requestor** — partner/steward/attorney; `TO BE SECURED` where unknown.
- **verifiedNeed** — `true` only once a specific partner/need is confirmed; otherwise `false`
  (currently `false` everywhere — no partner secured).
- **outputLicense** — tooling/code: `MIT`; content/dataset/docs: `CC-BY-4.0` (CC-BY-SA is an open
  governance question — see PLAN).

Size legend: small ≈ tokenEstimate `small`, med ≈ `medium`, large ≈ `large`.
Reviewer "Attorney (jurisdiction)" = licensed attorney **admitted in the pilot jurisdiction** for the
relevant domain (HIGH-tier sign-off, **TO BE SECURED**). "Editorial" = independent
plain-language/neutrality/non-advice reviewer.

---

## Milestone M0 — Editorial policy, content schema & pipeline (cold-start)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| know-your-rights-jurisdiction-000 | Pilot jurisdiction + domain selection (scored vs. criteria) — gates M2–M6 | research | small | medium | document | — | Maintainer + Attorney (jurisdiction) |
| know-your-rights-policy-001 | Editorial / non-advice / UPL + neutrality policy specification | design-spec | medium | high | document | — | Editorial + Attorney (jurisdiction) |
| know-your-rights-repo-002 | Monorepo + pnpm + TS/ESM + static-site + CI (build/test/lint) skeleton | code | small | low | pr | — | Maintainer |
| know-your-rights-schema-003 | Rights-card / explainer content JSON Schema + single-source render to site + dataset | code | medium | medium | pr | 002 | Maintainer |
| know-your-rights-lint-004 | Content-lint suite: non-advice + neutrality + jurisdiction-label + citation-coverage + readability (CI gate) | code | medium | high | pr | 001, 003 | Editorial + Maintainer |
| know-your-rights-workflow-005 | Multi-gate review workflow: CODEOWNERS + PR checklist (editorial→legal→a11y→merge) + reviewers ledger | design-spec | small | medium | document | 001 | Maintainer + Editorial |

**Acceptance criteria — key tasks**

- **know-your-rights-jurisdiction-000** (pilot jurisdiction + domain selection)
  - Scores candidate jurisdiction+domain pairs against explicit criteria: (1) primary law reusable
    under the edict-of-government doctrine (no copyrighted compiled-code/annotation lock-in); (2) high
    access-to-justice need / density of unrepresented people in the domain; (3) an available licensed
    attorney admitted there (ideally a law-school clinic); (4) manageable legal complexity / stable
    regime; (5) a plausible distribution partner.
  - Records the decision (or shortlist + the fixed decision deadline of 2026-08-31) with rationale;
    proposal is **tenant rights, one jurisdiction**. The chosen pair becomes a dependency for M2.
  - The *specific* jurisdiction stays `TO BE SECURED` until confirmed, but the decision rule +
    deadline are fixed; this task gates M2–M6 sequencing.

- **know-your-rights-policy-001** (editorial / non-advice / UPL + neutrality policy)
  - Defines the bright-line distinction between **general legal information** (in scope) and
    **individualized legal advice** (out of scope / UPL), with concrete examples of each.
  - Enumerates the refused set in testable terms: individualized advice / case-specific
    recommendations / outcome predictions; partisan or advocacy framing; "resist/evade the law"
    directives; help committing offenses or harming others; unscoped ("no jurisdiction") legal claims.
  - Mandates the persistent **"general legal information, not legal advice — laws change and vary;
    consult a lawyer / legal aid"** banner + route-to-help block on every surface.
  - Mandates a **jurisdiction label + `scope-level` (general vs jurisdiction-specific)** on every
    claim, and the **no-source-no-claim** rule.
  - Specifies the neutrality standard for charged topics and the **red-team taxonomy** the neutrality
    eval must cover (≥ 8 cases per charged-topic category, multiple phrasings).
  - Mandates the **licensed-attorney sign-off gate** (admitted in the jurisdiction) and the
    fail-closed default (content that can't be confidently classified as general info is held).
  - Reviewed and signed off by an independent editorial reviewer + a licensed attorney (recorded).

- **know-your-rights-lint-004** (content-lint suite)
  - **Non-advice lint** flags individualized-advice phrasings (second-person legal imperatives, "in
    your case," "you should [legal action]") and routes them to human review; fail-closed.
  - **Jurisdiction-label check** fails the build on any rights-stating claim lacking a named
    jurisdiction + `scope-level`.
  - **Citation-coverage check** fails the build on any claim node without an attached `Source`
    ("no source, no claim").
  - **Neutrality lint** flags advocacy/partisan/loaded framing and "resist/evade" directives.
  - **Readability check** enforces ≤ grade 8 for explainers and ≤ grade 6 for cards.
  - Runs in CI; a regression that lets advice/partisan/unsourced/unscoped content through **fails the
    build**; results reported as passed/total at version N with a per-version changelog.

- **know-your-rights-schema-003** (content schema + single-source render)
  - JSON Schema (Ajv) with required fields: jurisdiction, scope-level, topic/scenario,
    plain-language right, citations[], "what you can do / who to contact", not-legal-advice banner,
    readingLevel, `lastVerified`, `validUntil`, reviewer sign-off record, license, provenance.
  - Content authored once renders to **both** the static site and the machine-readable dataset (no
    drift); schema validation runs in CI.

**M0 Definition of Done:** editorial/non-advice/UPL + neutrality policy spec (editorial- and
attorney-reviewed) merged; content-lint suite passing in CI (non-advice, neutrality,
jurisdiction-label, citation-coverage, readability) with a regression failing the build; content
JSON Schema + single-source site/dataset build green; "not legal advice" + jurisdiction-label framing
wired into the template; the multi-gate review workflow (CODEOWNERS + PR checklist + reviewers
ledger) defined; **pilot jurisdiction + domain selected (or shortlisted with a fixed decision)**.

---

## Milestone M1 — Source corpus, provenance & staleness foundation

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| know-your-rights-sources-006 | Pilot-domain source vetting: verify reuse terms + record provenance | data | medium | high | dataset | 000, 005 | Attorney (jurisdiction) + Maintainer |
| know-your-rights-provenance-007 | Source/provenance model + citation-coverage enforcement + runtime staleness fail-safe | code | medium | medium | pr | 003, 006 | Maintainer |
| know-your-rights-eval-008 | Minimal cited-vs-blank-slate eval as an early go/no-go kill-gate (handful of fixtures) | code | small | medium | pr | 007 | Maintainer + Editorial |

**Acceptance criteria — key tasks**

- **know-your-rights-sources-006** (source vetting)
  - Reuse terms verified and recorded per source (edict-of-government PD primary law vs. copyrighted
    annotation/compiled code vs. openly licensed legal-aid material vs. cite-only); only reusable
    sources enabled, and proprietary annotations are **never copied** (paraphrase + cite only).
  - Provenance recorded per source: name, jurisdiction, citation, retrieval date, stable URL,
    license/legal-status note.
  - Attorney sign-off recorded before sources are enabled for content.

- **know-your-rights-provenance-007** (provenance + citation coverage + staleness)
  - No claim renders without an attached `Source` (citation-coverage test).
  - Each `Source` carries `lastVerified` + `validUntil` (per-source-type review interval); at
    render/build time a claim past `validUntil` is **auto-flagged or withheld** until re-verified and
    **re-signed-off by an attorney**. A staleness test asserts no claim serves as current past its
    window.

- **know-your-rights-eval-008** (minimal cited-vs-blank-slate kill-gate)
  - Runs content answering cited+jurisdiction-scoped vs. blank-slate on a small fixture set; reports
    the delta as an early **go/no-go**: if cited+scoped does not at least trend ahead on accuracy +
    citation + jurisdiction-fit, HIGH-tier content work (M2) **pauses** for review rather than waiting
    for the full M4 eval (eval-015).

**M1 Definition of Done:** pilot-domain sources vetted with recorded reuse terms + provenance;
`Source` model with `lastVerified`/`validUntil`; citation-coverage + runtime staleness fail-safe
implemented and tested; the **minimal cited-vs-blank-slate kill-gate** passes (cited+scoped trends
ahead) before M2 content investment.

---

## Milestone M2 — Pilot content set (one domain, one jurisdiction), attorney-reviewed

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| know-your-rights-content-009 | Tenant-rights explainer set for pilot jurisdiction (eviction, repairs, deposits, lockouts, retaliation, discrimination) — cited, attorney-reviewed | writing | large | high | document | 004, 006, 007 | Attorney (jurisdiction) + Editorial |
| know-your-rights-card-010 | Concise printable/offline "tenant rights" wallet card (≤ grade 6) — cited, attorney-reviewed | writing | small | high | document | 009 | Attorney (jurisdiction) + Editorial |
| know-your-rights-dataset-011 | Structured rights-card dataset records for the pilot content (schema-valid, CC-BY) | data | medium | high | dataset | 003, 009 | Maintainer + Attorney (jurisdiction) |

**Acceptance criteria — key tasks**

- **know-your-rights-content-009** (tenant-rights explainer set)
  - Covers the core tenant scenarios for the jurisdiction (eviction process & notice rules,
    repairs/habitability, security deposits, illegal lockouts/utility shutoffs, retaliation, housing
    discrimination), each as a **general** explainer (not individualized advice).
  - Every legal claim is **primary-source-cited to the named jurisdiction**; passes the non-advice +
    neutrality + jurisdiction-label + citation-coverage + readability lint (≤ grade 8).
  - Carries the "not legal advice" banner + route-to-help (legal aid / housing court self-help /
    relevant agency) on every page.
  - **Attorney-signed-off** (admitted in the jurisdiction), sign-off recorded and version-scoped.

- **know-your-rights-card-010** (printable wallet card)
  - One-page, printable, legible **offline**; ≤ grade 6 reading level; covers the highest-value
    tenant rights + "what to do / who to call."
  - Cited (claims trace to the explainer's sources); attorney-signed-off; carries "not legal advice"
    + "verify currency" + `lastVerified` stamp.

- **know-your-rights-dataset-011** (structured dataset)
  - Each rights card is a schema-valid record (all required fields, valid jurisdiction + scope-level
    + citations + sign-off record + license).
  - Exported under CC-BY-4.0; single-sourced with the site (no drift); validation passes in CI.

**M2 Definition of Done:** the pilot jurisdiction's tenant-rights explainer set + printable card
drafted in plain language, **primary-source-cited to the jurisdiction**, lint-clean, and
**attorney-signed-off**; the structured CC-BY dataset records produced and schema-valid; the minimal
cited-vs-blank-slate kill-gate (eval-008), now on real reviewed content, still shows cited+reviewed
ahead — otherwise stop and reassess before M3.

---

## Milestone M3 — Publishing surface, accessibility & i18n scaffolding

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| know-your-rights-site-012 | Static site: jurisdiction selector/label, "not legal advice" + route-to-help blocks, print stylesheet | code | medium | medium | pr | 003, 009 | Maintainer + Editorial |
| know-your-rights-a11y-013 | Accessibility pass (WCAG 2.2 AA) + offline card legibility + reading-level CI enforcement | code | small | medium | pr | 012 | Accessibility + Maintainer |
| know-your-rights-i18n-014 | i18n scaffolding (per-language-review-gated; no machine-translated legal claims shipped) | code | small | low | pr | 012 | Maintainer |

**Acceptance criteria — key tasks**

- **know-your-rights-site-012** (publishing surface)
  - Every page shows a **jurisdiction label/selector** and the persistent "not legal advice" +
    route-to-help blocks; no-JS-required rendering; print stylesheet produces the offline card.
  - Pages stamp `lastVerified`; stale (`validUntil`-passed) claims render flagged/withheld per the
    fail-safe.

- **know-your-rights-a11y-013** (accessibility + reading level)
  - Core surfaces meet WCAG 2.2 AA (axe/Lighthouse + manual audit); the printable card is legible
    offline; reading-level ceilings enforced in CI (explainers ≤ grade 8, cards ≤ grade 6).

**M3 Definition of Done:** static site + dataset export live; WCAG 2.2 AA on core surfaces;
jurisdiction label on every page; printable/offline card; reading-level + "last verified" +
route-to-help enforced; i18n scaffolding ready with translations gated on per-language legal +
linguistic review.

---

## Milestone M4 — Eval, hardening & distribution readiness

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| know-your-rights-eval-015 | Full eval: cited+jurisdiction-scoped+reviewed vs. blank-slate (accuracy/citation/jurisdiction-fit/neutrality) | code | medium | medium | pr | 008, 009 | Maintainer + Attorney (jurisdiction) |
| know-your-rights-hardening-016 | Hardening: expanded neutrality + non-advice red-team, link-check + staleness CI, distribution/partner runbook | code | medium | high | pr | 004, 012, 013 | Editorial + Maintainer |

**Acceptance criteria — key tasks**

- **know-your-rights-eval-015** (full eval)
  - Runs content answering cited+scoped+reviewed vs. blank-slate on fixture scenarios; LLM judge +
    attorney spot-check score accuracy, citation/groundedness, jurisdiction-fitness, neutrality, and
    non-advice compliance.
  - Reports the delta; cited+reviewed must clearly beat blank-slate or the thesis is flagged failing.

- **know-your-rights-hardening-016** (hardening + distribution readiness)
  - Expanded neutrality + non-advice red-team (≥ 8 cases per charged category) still 100%
    neutral/non-advice; link-checking + staleness checks green in CI.
  - **Distribution/partner runbook**: how a legal-aid org embeds, links, prints, or republishes the
    content while preserving attribution + "not legal advice" + currency stamps.

**M4 Definition of Done:** full eval proves cited+reviewed beats blank-slate; expanded red-team +
link-check + staleness CI green; the distribution/partner runbook is ready — the artifact is
partner-ready.

---

## Milestone M5 — Partner adoption & handoff (the deed)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| know-your-rights-partner-017 | Secure distribution partner/steward + independent neutrality+currency audit + attorney sign-off of shipped content | research | medium | high | document | 015, 016 | Steward + Attorney (jurisdiction) + Editorial |
| know-your-rights-handoff-018 | Partner distributes content to beneficiaries; ≥ 1 documented beneficiary use recorded (no PII) | maintenance | medium | high | document | 017 | Steward + Editorial |

**Acceptance criteria — key tasks**

- **know-your-rights-partner-017** (secure partner + audits)
  - A real legal-aid / tenant / worker / civil-liberties org or law-school clinic is secured as the
    distribution partner; steward assigned; `verifiedNeed` flips to `true`.
  - Independent editorial reviewer audits neutrality + non-advice + currency; all shipped
    rights-stating content has recorded attorney sign-off; zero-PII posture confirmed.
  - Driven by the **dated partner-acquisition plan** (jurisdiction by 2026-08-31, attorney by
    2026-10-31, partner by 2026-12-31). If no partner is secured by **~2027-03-31**, apply the
    **build-vs-mothball/pivot decision rule** (PLAN exec summary): contribute the attorney-reviewed
    content into an existing established commons (legal-aid network / law-school clinic public
    materials), or mothball to maintenance-only — recorded in governance — rather than publish to no
    real beneficiary.

- **know-your-rights-handoff-018** (closed loop — the deed)
  - The partner distributes the content to the people it serves; ≥ 1 documented instance of a
    beneficiary using it to understand or assert a right (partner-attested, **no PII**).
  - Neutrality + "not legal advice" + currency upheld throughout; outcome recorded.

**M5 Definition of Done:** project-level **Definition of Shipped** met — a real org distributes the
attorney-reviewed content to real beneficiaries with ≥ 1 documented use; neutrality + currency
independently verified; shipped content attorney-signed-off; zero reader PII; outcome recorded.
*(Gated on a secured partner — TO BE SECURED.)*

---

## Milestone M6 — Sustain & scale (post-delivery)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| know-your-rights-ops-019 | Ops runbook + review cadence (law-change → re-verify → re-sign-off) + outcome tracking + maintenance rotation | maintenance | medium | medium | document | 018 | Maintainer + Steward |

**Acceptance criteria — know-your-rights-ops-019**
- Runbook covers publish/deploy, link/staleness monitoring, source re-verification, and partner
  support.
- Review cadence enforced via the `lastVerified`/`validUntil` fail-safe (law-change re-verification +
  attorney re-sign-off before content returns to normal service).
- Outcome tracking records content distributed, documented beneficiary uses, and neutrality/currency
  audit status (no PII, no engagement vanity metrics); named maintenance rotation; documented,
  attorney-gated process for adding the next domain/jurisdiction.

**M6 Definition of Done:** project sustainably maintained with outcomes tracked, a rotation owning
it, a runtime-enforced review cadence for legal content, and a gated expansion process.

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
|---|---|---|---|---|---|---|
| know-your-rights-worker-020 | Worker-rights domain pack (wage theft, overtime, misclassification, safety, retaliation) | writing | large | high | document | After M6; full source-vetting + attorney sign-off |
| know-your-rights-jurisdiction-021 | Second jurisdiction tenant-rights pack | data | large | high | dataset | After M6; per-jurisdiction sourcing + attorney admitted there |
| know-your-rights-streetrights-022 | "Street rights" domain (police encounters / recording / protest) — deferred, extra safety review | writing | large | high | document | Highest physical-danger profile; attorney + practitioner safety review; never advise escalation |
| know-your-rights-immigration-023 | Immigration-enforcement-encounter rights — deferred, specialist review | writing | large | high | document | Specialist immigration attorney + safety review; never advise unlawful conduct |
| know-your-rights-i18n-024 | Per-language translations of reviewed content | translation | medium | high | translation | Each language = combined legal + linguistic review; no machine-translated legal claims |
| know-your-rights-funded-025 | (Optional) Funded lane for attorney review hours | maintenance | small | high | document | Hard `fundedBudgetUsd` cap; must not compromise reviewer independence |

---

## Example task JSON

Complete, schema-valid Task JSON for the first M0 task (`know-your-rights-policy-001`):

```json
{
  "id": "know-your-rights-policy-001",
  "title": "Editorial / non-advice / UPL + neutrality policy specification",
  "project": "know-your-rights",
  "type": "design-spec",
  "lane": "donated",
  "priority": "high",
  "domain": ["legal", "civic", "access-to-justice", "tenant-rights", "content"],
  "riskTier": "high",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "medium",
  "status": "open",
  "context": "Know-Your-Rights publishes neutral, primary-source-cited, jurisdiction-specific 'know your rights' explainers (starting with tenant rights) as open content for people who cannot afford a lawyer. The defining risk is that legal content can drift into individualized legal advice (the unauthorized practice of law), into partisanship on charged topics, or into dangerous staleness - any of which harms the people it means to help. So the neutrality / non-advice / UPL editorial policy is a hard product requirement built FIRST and enforced as a tested CI gate, not a disclaimer footer. This cold-start task specifies that policy before any rights content is written. No partner, distribution channel, or licensed-attorney reviewer is yet secured.",
  "objective": "Write the authoritative editorial policy that all later content and tooling must implement and be tested against: the bright-line distinction between general legal information (in scope) and individualized legal advice (out of scope / UPL); the refused set (advice, partisan/advocacy framing, resist/evade directives, help with offenses/harm, unscoped legal claims); the mandatory 'not legal advice' + route-to-help framing; the mandatory jurisdiction label + scope-level and no-source-no-claim rules; the neutrality standard and red-team taxonomy for charged topics; and the licensed-attorney sign-off gate (attorney admitted in the jurisdiction) with a fail-closed default.",
  "acceptanceCriteria": [
    "Defines the bright-line distinction between general legal information (in scope) and individualized legal advice (out of scope / unauthorized practice of law), with concrete in/out examples",
    "Enumerates the refused set in concrete, testable terms: individualized advice / case-specific recommendations / outcome predictions; partisan or advocacy framing; resist-or-evade-the-law directives; help committing offenses or harming others; and unscoped 'no jurisdiction' legal claims",
    "Mandates the persistent 'general legal information, not legal advice - laws change and vary by location; consult a lawyer or legal aid' banner plus a route-to-help block on every content surface",
    "Mandates a jurisdiction label and a scope-level field (general vs jurisdiction-specific) on every claim, and the no-source-no-claim citation rule",
    "Specifies the neutrality standard for charged topics and the red-team taxonomy the neutrality eval must cover (>= 8 cases per charged-topic category, multiple phrasings), with a fail-closed default (content not confidently classifiable as general info is held for human review)",
    "Mandates the licensed-attorney sign-off gate - an attorney admitted in the jurisdiction the content describes - recorded before any rights-stating content ships, with version-scoped sign-off and name-use limits",
    "Reviewed and signed off by an independent editorial reviewer and a licensed attorney (recorded in the reviewers ledger)"
  ],
  "resources": [
    "planning/projects/know-your-rights/PLAN.md",
    "CLAUDE.md",
    "docs/good-deed-definition.md",
    "packages/schema/src/schemas.ts",
    "planning/projects/public-official-guide/PLAN.md",
    "planning/ROADMAP.md"
  ],
  "output": "A reviewed policy-specification document (the editorial / non-advice / UPL + neutrality charter) defining the information-vs-advice line, the refused set, the mandatory framing and jurisdiction/citation rules, the neutrality standard and red-team taxonomy, and the attorney-review gate - the contract that know-your-rights-lint-004 (content-lint suite) and all content tasks implement and are verified against.",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "CC-BY-4.0"
}
```
