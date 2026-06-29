# Know-Your-Rights — PLAN.md

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

Neutral, primary-source-cited **"know your rights"** explainers that help people who cannot
afford a lawyer understand their legal rights in everyday high-stakes situations — starting with
**tenant rights**, then **worker rights**, then **civil rights** — always as **information, not
legal advice**, always **jurisdiction-sourced**, and never shipped without **licensed-attorney
review**. The project produces an open content commons (CC-BY): a structured, machine-readable
dataset of "rights cards" plus a plain-language, accessible, offline-printable static site, built
on a publishing pipeline whose **review gates and neutrality policy are the product**, not a
disclaimer footer.

---

### What Know-Your-Rights is — and is not

**It is a primary-source-cited public legal-information commons, not a lawyer and not a chatbot.**
The access-to-justice gap is enormous: most people facing eviction, wage theft, or a police
encounter never speak to an attorney, and the authoritative information that *would* protect them
(statutes, regulations, case law, official agency guidance) exists but is fragmented, jargon-heavy,
and impossible to apply under pressure. This project closes the gap between *the law exists* and
*the person can understand and act on it in time* — **for the general case, in a named
jurisdiction**, never for the individual's specific matter.

- **It explains the law; it never advises a person.** A licensed attorney advising a specific
  client on a specific situation is the practice of law. This project produces **general legal
  information** about how the law works in a jurisdiction — categorically distinct from
  individualized advice — to stay on the correct side of the **unauthorized-practice-of-law (UPL)**
  line. Every surface says so, and routes the reader to counsel / legal aid for their actual case.
- **It is neutral and non-partisan by construction.** "Know your rights" topics (police stops,
  protest, immigration enforcement, housing) are politically charged. The project states **what the
  law is** in a jurisdiction — what it permits, requires, and prohibits — neutrally and completely;
  it never advocates a position, never tells a person to resist or evade the law, and never frames
  rights as the cause of one side.
- **The content is the artifact, and the review gates are the moat.** Anyone can ask an LLM "what
  are my tenant rights." What no blank-slate generation can match is content that is
  **jurisdiction-correct, primary-source-cited, attorney-reviewed, and provably current** — with a
  recorded provenance and staleness fail-safe so it cannot silently rot when the law changes.

> In one line: **the law already protects you; this project makes that protection legible, current,
> and free — without ever pretending to be your lawyer.**

---

## Executive summary

People facing eviction, wage theft, unsafe work, discrimination, or a law-enforcement encounter
routinely make irreversible decisions without knowing the rights the law already grants them.
Authoritative sources exist — statutes, regulations, court rules, agency guidance, and openly
licensed legal-aid materials — but they are scattered, written for lawyers, and unusable at the
moment of need. **Know-Your-Rights** turns that primary law into neutral, plain-language,
**jurisdiction-specific** explainers and concise, printable "rights cards," published as an open
commons (CC-BY) that legal-aid organizations, tenant unions, worker centers, and civil-liberties
groups can adopt, embed, translate, and hand to the people they serve.

The single most important design fact is the **"information, not legal advice" boundary**, enforced
as a tested subsystem rather than asserted as a disclaimer. Producing individualized legal advice
without a license is the unauthorized practice of law and can harm the very people the project means
to help; inaccurate or outdated rights information in a high-stakes moment (a detention, an eviction
hearing, a firing) can get someone jailed, evicted, or fired. So the project is engineered around
three hard gates: a **neutrality / non-advice / UPL editorial policy** (built first), a **mandatory
licensed-attorney review** for every jurisdiction-specific claim before it ships, and a **runtime
staleness fail-safe** that withholds or flags any claim whose backing source is past its
review window until it is re-verified and re-signed-off.

This is a **HIGH risk-tier** project (legal content, per `docs/good-deed-definition.md`). No
content stating a right or legal rule ships without (a) a primary-source citation to the law of a
**named jurisdiction**, (b) recorded sign-off by a **licensed attorney admitted in that
jurisdiction**, and (c) the persistent **"informational, not legal advice — consult a lawyer"**
framing. Errors are not merely embarrassing here; they are dangerous. The review apparatus is
treated as safety-critical.

**Honesty note: no partner organization or licensed-attorney reviewer is yet secured.** Every
delivery-dependent task is marked `TO BE SECURED` with `verifiedNeed: false`. The project is **not
"shipped" on merge**; it is shipped only when a real legal-aid / tenant / worker / civil-liberties
organization distributes the content to real beneficiaries, with attorney sign-off recorded and the
neutrality and currency controls independently verified.

**Partner-acquisition plan (dated) and build-vs-mothball decision rule.** Outreach is time-boxed
against the build, not left open-ended: by **2026-08-31** the pilot jurisdiction + first rights
domain (proposal: **tenant rights, one US jurisdiction**) is selected against the criteria in *Open
questions*, and ≥ 3 candidate partners (legal-aid society, tenant union, law-school housing clinic,
or bar pro-bono program) are in active conversation; by **2026-10-31** a licensed-attorney reviewer
admitted in the pilot jurisdiction is secured (the M2 gate); by **2026-12-31** a distribution
partner / steward is secured (the M5 gate). **Decision rule:** if no licensed attorney is secured
by the M2 entry date, M2 content work does **not** start and the project holds at M1 (pipeline +
sourced corpus). If no distribution partner is secured by **2027-03-31** (≈ M4 completion), the
project does **not** publish blindly to no one: it either (a) **pivots** the last-mile beneficiary
(e.g., contribute the attorney-reviewed content into an existing established commons such as a legal-
aid network or a law-school clinic's public materials) or (b) **mothballs** — archived,
maintenance-only, no further HIGH-tier content — recorded in governance. The reviewed
single-jurisdiction content remains valuable as a reference artifact either way.

---

## Problem & beneficiaries

**Who is helped (directly):** people who must make consequential legal decisions without access to a
lawyer — disproportionately low-income, immigrant, disabled, and limited-English-proficiency
people. Concretely, in the launch domains:

- **Tenants** facing eviction, illegal rent increases, withheld deposits, retaliation, uninhabitable
  conditions, or housing discrimination.
- **Workers** facing wage theft, unpaid overtime, misclassification, unsafe conditions, denied
  breaks, or retaliation for complaints.
- **People exercising civil rights** — interactions with law enforcement, the right to record,
  protest rights, and (later, behind a hardened review apparatus) immigration-enforcement
  encounters.

**Who is helped (ultimately):** the broader public and the **access-to-justice ecosystem** —
legal-aid organizations, tenant unions, worker centers, public defenders, and clinics whose
capacity is multiplied when accurate, current, citable rights information is free and reusable.

**The need.** The civil access-to-justice gap is well documented: a large majority of low-income
people's civil legal problems receive no or inadequate legal help, and most tenants in eviction
proceedings are unrepresented. The law that protects them already exists; what is missing is a
**trustworthy, current, plain-language, jurisdiction-correct** bridge to it — one that does not
masquerade as advice. Generic web search and blank-slate LLM answers are dangerous here precisely
because they are confident, jurisdiction-blind, uncited, and frequently stale.

**Verified need / partner:** **TO BE SECURED.** No specific legal-aid organization, tenant union,
worker center, civil-liberties group, or law-school clinic has yet agreed to adopt, co-develop, or
distribute the content, and **no licensed-attorney reviewer is secured.** Target partner profiles
to pursue: a Legal Services Corporation–funded legal-aid program or local legal-aid society; a
tenant union or tenants'-rights coalition; a worker center or workers'-rights project; an ACLU
state affiliate or other civil-liberties organization; a law-school **housing / employment / civil-
rights clinic** (a natural source of both a credentialed reviewer and a distribution channel); or a
state/local bar **pro bono** program. Until one is secured, the project builds the agent-neutral
pipeline, the neutrality/non-advice policy, the sourced corpus, and **one illustrative
jurisdiction + domain** content set for review, and marks all distribution/adoption work `TO BE
SECURED`. Outreach is **dated, not open-ended** (see the partner-acquisition plan above), governed
by a **build-vs-mothball/pivot decision rule** if the dates slip — the content is contributed to an
existing commons or mothballed rather than published to no real beneficiary.

---

## Goals and non-goals

**Goals**

- Publish neutral, plain-language, **primary-source-cited, jurisdiction-specific** rights explainers
  and concise printable "rights cards," starting with one domain in one jurisdiction done
  *excellently* rather than fifty done shallowly.
- Ship a **neutrality / non-advice / UPL editorial policy** that *provably* keeps content general
  (not individualized advice), non-partisan, and within the bounds of public legal information —
  verified by an automated content-lint suite and an independent editorial reviewer.
- Make **licensed-attorney review** a hard, recorded gate: no jurisdiction-specific legal claim
  ships without sign-off by an attorney admitted in that jurisdiction.
- Guarantee **currency**: every claim is backed by a dated, provenance-tracked source and a runtime
  staleness fail-safe so stale law is flagged or withheld, never silently served as current.
- Produce an **accessible, offline-usable** artifact (WCAG 2.2 AA, plain-language, printable
  wallet-card format) because beneficiaries often act with no connectivity and limited literacy.
- Build a **machine-readable open dataset** (CC-BY) of structured rights cards so partners can
  reuse, embed, and translate the content.
- Prove via an eval that **cited + jurisdiction-scoped + reviewed** content beats blank-slate LLM
  output on accuracy, citation, jurisdiction-fitness, and neutrality.

**Non-goals**

- **Not legal advice** and not a substitute for a lawyer, legal aid, the court clerk, or an agency.
  It never answers "what should *I* do in *my* situation."
- **Not a lawyer-matching, case-intake, triage, or document-filing service**, and not an automated
  "legal assistant" that interacts with a user's specific facts.
- **Not partisan or advocacy content.** It states the law neutrally; it does not campaign for or
  against any policy, party, or cause, and it never tells a person to resist, evade, or break the
  law.
- **Not a 50-state / multi-jurisdiction database at launch.** Depth and verified accuracy for one
  jurisdiction + one domain first; breadth later, and never breadth without per-jurisdiction
  attorney review.
- **Not real-time or emergency-response infrastructure.** It is reference content, framed as such;
  it never claims to be reliable in a live emergency and always routes to counsel/hotlines.
- **Not a collector of user data.** It is published content, not an app with accounts; it does not
  ask users about their personal legal situation or store any reader PII (see *Security & privacy*).

These refusals are the identity of the project as much as the content is. A "know your rights"
resource that drifted into individualized advice, partisanship, or stale confidence would harm the
people it claims to serve.

---

## Success metrics (outcomes)

Outcome-centric and beneficiary-first. Traffic/pageviews are explicitly **not** success.

| Metric | Baseline | Target (pilot) | How measured |
|---|---|---|---|
| Jurisdiction-specific legal claims with a primary-source citation | none | **100%** of shipped claims carry a citation to primary law of the named jurisdiction | Citation-coverage test in CI + reviewer checklist |
| Attorney sign-off before content ships | none | **100%** of HIGH-tier (rights-stating) content has recorded sign-off by an attorney admitted in the jurisdiction | Governance / reviewers ledger |
| Non-advice / UPL lint pass rate | none | **100%** of content passes the automated non-advice + jurisdiction-label + "not legal advice" lint; 0 individualized-advice phrasings shipped | Content-lint suite in CI |
| Neutrality red-team pass rate | none | reported as **passed/total at version N** with a per-version changelog; **≥ 8 cases per charged-topic category**; 100% neutral/non-advocacy | Automated neutrality eval + independent editorial audit |
| Stale-content containment | none | **0** claims served past their `validUntil` without an auto-flag/withhold and re-sign-off | Staleness test against `lastVerified`/`validUntil` + runtime audit |
| Reading level of explainers | none | core explainers at **≤ grade 8** (rights cards ≤ grade 6); measured + enforced | Automated readability check in CI |
| Accessibility | none | core surfaces meet **WCAG 2.2 AA**; printable card is legible offline | axe/Lighthouse + manual audit |
| Cited+reviewed vs. blank-slate quality delta (eval) | none | cited+jurisdiction-scoped+reviewed clearly beats blank-slate on accuracy, citation, jurisdiction-fit, neutrality | LLM-judge eval harness + attorney spot-check |
| Reader PII collected/stored | n/a | **zero** — no accounts, no case intake, no tracking of personal legal facts | Privacy review; site has no PII surface |
| Partner adoption to real beneficiaries (the deed) | 0 | ≥ 1 partner org **distributes** the content to its served population; ≥ 1 documented instance of a beneficiary using it to assert a right | Partner-attested log (with consent, no PII) |

The **defining success outcome** (Definition of Shipped): a real access-to-justice organization
distributes the attorney-reviewed content to the people it serves, and there is at least one
documented instance of a beneficiary using it to understand or assert a right — with neutrality and
currency controls independently verified and all legal content attorney-signed-off.

---

## Scope

**In scope**

- Neutrality / non-advice / UPL **editorial policy** and its automated content-lint enforcement.
- A **content schema** (structured "rights card" / explainer format) with mandatory fields:
  jurisdiction, topic/scenario, the plain-language right, the primary-source citation(s), "what you
  can do / who to contact," explicit "this is not legal advice," reading level, `lastVerified`,
  `validUntil`, reviewer + sign-off record, license, and provenance.
- A **source corpus** for the pilot jurisdiction + domain: primary law (statutes, regulations, court
  rules, controlling case law), official government/agency guidance, and **openly licensed**
  legal-aid materials, each with verified reuse terms and recorded provenance.
- A **publishing pipeline**: schema validation, citation-coverage, non-advice/neutrality lint,
  readability check, link-checking, and staleness checks in CI; a static-site generator; and a
  machine-readable dataset export.
- A **multi-gate review workflow**: editorial (plain language, neutrality, non-advice) → **legal
  (licensed attorney for the jurisdiction)** → accessibility → maintainer merge.
- The pilot domain's explainer set + concise printable rights card, attorney-reviewed.
- Accessibility (WCAG 2.2 AA), plain-language/reading-level enforcement, and a printable/offline
  card format. i18n **scaffolding** (translations are a future, per-language-reviewed deliverable).
- An eval harness proving cited+reviewed beats blank-slate.

**Out of scope (explicitly will NOT do)**

- **Individualized legal advice**, case-specific recommendations, outcome predictions, or any
  feature that takes a user's personal facts and tells them what to do — this is the bright UPL line.
- **Document drafting / filing for a user's matter** (e.g., generating *their* eviction answer),
  lawyer-matching, case intake, or triage.
- **Partisan, advocacy, or "resist/evade" content** — telling people to break, resist, or evade the
  law; campaigning for/against any policy, party, official, or cause; framing rights as one
  political side's issue.
- **Help committing an offense or harming others** (e.g., how to obstruct a lawful investigation,
  how to retaliate, how to commit fraud) — refused and flagged.
- **Multi-jurisdiction claims without per-jurisdiction sourcing + attorney sign-off**, or any "this
  is the law" statement that is not tied to a **named jurisdiction**.
- **Collecting reader PII** or any personal legal situation; building user profiles; tracking.
- **The most physically dangerous / charged domains at launch** (live police-encounter tactics,
  immigration-enforcement encounters, protest tactics) — these are sequenced **after** the review
  apparatus is proven on tenant/worker content, because an error there can get someone hurt or
  detained (see *Roadmap*).

When a request falls in the refused set, the project (and any agent producing its content) refuses
that part, explains why in plain terms, and where possible points to the lawful, appropriate
resource (legal aid, the relevant agency, an attorney). **Routing to real help — not a bare refusal
and not a substitute opinion — is the project's ethical posture.**

---

## Solution approach & architecture

This is a **content + data + lightweight tooling** project, not a multi-tenant application. The
"product" is an open, reviewed, current corpus plus the pipeline and review gates that keep it
trustworthy. There are **no user accounts and no reader data**, which removes an entire class of
privacy/security risk by construction.

**Stack.** TypeScript, ESM, pnpm workspaces (per Elyos conventions). Content authored as **MDX/
Markdown with typed front-matter**, plus a normalized **machine-readable dataset** (JSON/YAML)
validated against a JSON Schema with **Ajv** (mirroring `packages/schema`). Static site via a
content-focused generator (**Astro** or **Eleventy** — open question) for fast, accessible, offline-
friendly, no-JS-required pages and a print stylesheet for the wallet card. Anthropic **Claude** is
used *only as a donated-lane drafting/translation/lint aid behind a thin provider-neutral LLM
client* — the human runs their own agent (donated lane; the CLI never runs headless), Claude never
"decides" what the law is, and no generated claim ships without a citation and attorney sign-off.
Code/tooling license **MIT**; content/dataset **CC-BY-4.0** (attribution to primary sources and
reviewers preserved; CC-BY-SA vs CC-BY is an open question).

**Components**

1. **Editorial policy + content-lint layer (`lib/editorial`) — built first.** The safety-critical
   subsystem. Not a style guide PDF; an enforced policy with automated checks:
   - *Non-advice / UPL lint*: flags individualized-advice phrasings ("you should," "in your case,"
     second-person imperative legal directives), missing **jurisdiction labels**, and missing the
     **"informational, not legal advice"** banner. Fail-closed: content that cannot be confidently
     classified as general information is **held for human review**, not published.
   - *Neutrality lint*: flags advocacy/partisan framing, "resist/evade" directives, and loaded
     language on charged topics; pairs with the neutrality red-team eval (see below).
   - *Citation-coverage check*: every claim node must carry ≥ 1 `Source`; a claim without a source
     fails the build ("no source, no claim").
   - *Readability check*: enforces the reading-level ceiling per content type.

2. **Content schema + dataset (`packages/kyr-schema`, `content/`).** A JSON Schema for the rights
   card / explainer with required fields (jurisdiction, scope-level [general vs jurisdiction-
   specific], topic, plain-language right, citations[], "what you can do / who to contact",
   not-legal-advice banner, readingLevel, `lastVerified`, `validUntil`, reviewer sign-off record,
   license, provenance). Content is authored once and rendered to both the site and the dataset, so
   the human-facing page and the machine-readable record never drift.

3. **Source / provenance store (`content/sources/`).** Each legal claim is backed by a `Source`
   record: citation (statute/reg/case/court-rule/agency guidance), jurisdiction, retrieval date,
   stable URL, **reuse/legal-status note** (edict-of-government primary law vs. copyrighted
   annotation vs. openly licensed legal-aid material), and `lastVerified`/`validUntil`. A claim may
   not render without an attached, in-window source.

4. **Staleness fail-safe (`lib/staleness`).** Law changes constantly (rent caps, eviction rules,
   minimum wage, agency guidance). Each `Source` carries `lastVerified` + `validUntil` derived from
   a per-source-type **review interval** (e.g., statutes annually; agency guidance and fast-moving
   tenant rules on a shorter cadence). At **render/build time** a claim whose source is past
   `validUntil` is **auto-flagged** ("this may be out of date — verify before relying") or, for the
   highest-stakes surfaces, **withheld**, and the source enters the re-verification queue. It cannot
   return to normal service until re-verified **and re-signed-off by an attorney**, which writes a
   fresh `lastVerified`/`validUntil`. Stale law is a visible, gated event, never a silent error.

5. **Review workflow (`docs/review/`, CODEOWNERS, PR gates).** A PR template + checklist enforce the
   gate order: **editorial** (plain language, neutrality, non-advice) → **legal (licensed attorney
   admitted in the jurisdiction)** → **accessibility** → **maintainer merge**. Sign-off is
   **version-scoped** (attaches to a specific content version + citation set; later edits require
   re-sign-off). Reviewers are recorded in a reviewers ledger with credentials and consent.

6. **Publishing surface (`apps/site`).** A static, accessible (WCAG 2.2 AA), no-JS-required site
   with: persistent "informational, not legal advice" framing; an explicit **jurisdiction selector
   / label** on every page (so a reader never mistakes one jurisdiction's law for another's); a
   **printable, offline wallet-card** stylesheet; "last verified" + "get real help" (legal aid /
   hotline) blocks on every page; and the dataset export for partners.

7. **Eval harness (`scripts/eval-grounded.ts`).** Runs content generation/answering cited+
   jurisdiction-scoped vs. blank-slate on fixture scenarios; an LLM judge (plus attorney spot-check)
   scores accuracy, citation/groundedness, jurisdiction-fitness, neutrality, and non-advice
   compliance. The headline metric is the delta: if cited+reviewed does not clearly beat
   blank-slate, the thesis fails.

**Key decisions (locked)**

- **Wedge = tenant rights, one jurisdiction.** Highest access-to-justice need, clearest statutory
  basis, lowest physical-danger profile, and the most accessible partner/reviewer pool (housing
  legal aid + housing clinics) — the right place to prove the review apparatus before touching
  physically dangerous domains.
- **Editorial / non-advice / UPL policy is the first build item and a release gate**, tested in CI —
  not a disclaimer.
- **No user accounts, no reader PII, ever** — the artifact is published content, eliminating a whole
  risk class.
- **Depth before breadth**: one jurisdiction + domain fully reviewed before any second.
- **Agent-neutral core**: any Anthropic/Claude specifics sit behind the LLM client; the corpus and
  pipeline carry no vendor logic.

---

## Data, licensing & compliance

**THIS SECTION IS CRITICAL — conservative by default.**

**Source material.** Primary law and official guidance: statutes and constitutions, regulations and
administrative codes, court rules, controlling case law, and official agency/government guidance for
the named jurisdiction; plus **openly licensed** legal-aid / nonprofit materials where they exist.
Many U.S. statutes, regulations, and judicial opinions are **government edicts not subject to
copyright** (the edict-of-government doctrine; *Georgia v. Public.Resource.Org*, U.S. 2020), and
court opinions are generally public domain. **But this varies by source and jurisdiction:** some
states assert copyright in **annotations and compiled codes**, some official guidance carries terms,
and **legal-aid materials are usually copyrighted unless explicitly openly licensed.** Therefore:

- **Every source's reuse terms are verified and recorded before its content ships.** We **cite and
  link** primary law and **paraphrase in our own plain language**; we do **not** copy proprietary
  annotations or compiled-code text, and we reuse third-party legal-aid material **only** when it
  carries an open license (PD / CC-BY / CC0 / CC-BY-SA) compatible with redistribution.
- Provenance is stored per source: source name, jurisdiction, citation, retrieval date, stable URL,
  and a **license / legal-status note** (edict-of-government PD vs. copyrighted annotation vs. open
  license vs. all-rights-reserved-cite-only).

**Provenance model.** Each rights claim is backed by a `Source` record (citation + provenance +
verified legal status + `lastVerified`/`validUntil`). The renderer may not surface a claim without
an attached, in-window source; a citation-coverage test enforces this.

**Staleness is fail-safe, not best-effort** (see *Solution approach* §4). A claim past its
`validUntil` is auto-flagged or withheld and cannot return to normal service until re-verified and
**re-signed-off by an attorney**.

**Output licensing.** Tooling/code: **MIT**. Content + dataset: **CC-BY-4.0** (attribution to
primary sources preserved; whether to use **CC-BY-SA** to keep derivatives open is an open question
for governance). Where reused upstream material is **CC-BY-SA**, derivative content inherits
share-alike for that material.

**Privacy / PII stance (strong, by construction).** The artifact is **published content with no
user accounts and no case intake**, so it **collects no reader PII**, asks no one about their
personal legal situation, and stores no personal legal facts. Any examples/scenarios in content are
**fictional or fully de-identified**. The only personal data the project handles is **reviewer**
identity (attorney name, bar admission, jurisdiction) — stored with consent in the reviewers ledger,
used only for the sign-off record and (with consent) public credit. The site avoids third-party
trackers; any analytics, if used at all, are privacy-preserving and aggregate-only (open question:
prefer none). **No secrets, tokens, or PII in logs, receipts, or committed files** (Elyos rule).

**Attribution.** Content cites primary law and attributes any openly licensed upstream material per
its license. Attorney reviewers are credited (with consent), scoped to the versions they approved
(no implied endorsement of unreviewed content — see *Governance*).

---

## Quality, review & risk gates

**Risk tier: HIGH** (legal content; `docs/good-deed-definition.md` requires credentialed expert
sign-off before merge). Pipeline/tooling/site-infra tasks are low–medium; **anything that states a
right, a legal rule, or a jurisdiction-specific obligation is HIGH** and gated on attorney sign-off.

**Required reviews before a deed is "done":**

- **Editorial review** — plain language, reading level, **neutrality**, and **non-advice/UPL**
  compliance (independent of the drafter).
- **Licensed-attorney sign-off** — by an attorney **admitted in the jurisdiction** the content
  describes — recorded before *any* rights-stating / jurisdiction-specific content ships. **No
  attorney, no ship.**
- **Accessibility review** — WCAG 2.2 AA on the rendered surface; the printable card is legible
  offline.
- **Maintainer review** — engineering quality, agent-neutral core, schema validity, citation
  coverage, staleness wiring, CI green, no secrets.

**Every content surface carries the persistent banner: "This is general legal information, not legal
advice. Laws change and vary by location. For your situation, talk to a lawyer or your local legal
aid."** and a routing block to real help.

**Definition of Shipped (project):** a real access-to-justice organization distributes the
attorney-reviewed content to the people it serves, with ≥ 1 documented beneficiary use; all
rights-stating content is **attorney-signed-off and primary-source-cited to the named
jurisdiction**; neutrality + non-advice controls pass and are independently audited; the staleness
fail-safe is in force; and the artifact is accessible and plain-language. Merge ≠ shipped.

---

## Roadmap & milestones

Phased: policy + pipeline first; sourced corpus + review workflow next; content only behind the
attorney gate; distribution last and gated on a secured partner. **Tenant rights, one jurisdiction**
is the wedge; physically dangerous/charged domains are deferred until the apparatus is proven.

- **M0 — Editorial policy, content schema & pipeline (cold-start).**
  *Goal:* the neutrality/non-advice/UPL policy and an agent-neutral content pipeline exist before any
  rights content.
  *Exit:* editorial policy spec + content-lint suite (non-advice, neutrality, citation-coverage,
  readability) merged and **passing in CI**; content JSON Schema + dataset/site build green;
  "informational, not legal advice" + jurisdiction-label framing wired into the template; the
  multi-gate review workflow (CODEOWNERS + PR checklist) defined. **Pilot jurisdiction + domain
  selected** (tenant rights, one jurisdiction) so M1+ builds against a real corpus and reviewer
  profile.

- **M1 — Source corpus, provenance & staleness foundation.**
  *Goal:* a vetted, provenance-tracked source corpus for the pilot domain + the currency machinery.
  *Exit:* sources for the pilot domain vetted with **recorded reuse terms** (edict-of-government PD
  vs. copyrighted annotation vs. open license) and provenance; `Source` model with
  `lastVerified`/`validUntil`; citation-coverage + **staleness fail-safe** implemented and tested.
  **Kill-gate:** a **minimal cited-vs-blank-slate eval** on a handful of fixtures runs here as an
  early **go/no-go** — if cited+jurisdiction-scoped does not at least trend ahead, HIGH-tier content
  investment (M2) pauses for review rather than waiting for the full M4 eval.

- **M2 — Pilot content set (one domain, one jurisdiction), attorney-reviewed.**
  *Goal:* the tenant-rights explainer set + printable card for the pilot jurisdiction, cited and
  signed off.
  *Exit:* core tenant explainers (e.g., the eviction process & notice rules, repairs/habitability,
  security deposits, illegal lockouts/utility shutoffs, retaliation, housing discrimination) drafted
  in plain language, **primary-source-cited to the jurisdiction**, neutrality/non-advice lint clean,
  and **attorney-signed-off**; the concise printable rights card produced and signed off.
  **Kill-gate confirmed:** the minimal cited-vs-blank-slate eval, now on real reviewed content, still
  shows cited+reviewed ahead — otherwise stop and reassess before M3.

- **M3 — Publishing surface, accessibility & i18n scaffolding.**
  *Goal:* the public artifact, accessible and offline-usable.
  *Exit:* static site + dataset export live; WCAG 2.2 AA on core surfaces; reading-level ceilings
  enforced; **jurisdiction label/selector** on every page; printable/offline wallet card; "last
  verified" + "get real help" blocks; i18n scaffolding ready (translations deferred, per-language
  review required).

- **M4 — Eval, hardening & distribution readiness.**
  *Goal:* prove the thesis and prepare for a real partner.
  *Exit:* full eval shows cited+reviewed clearly beats blank-slate; expanded neutrality + non-advice
  red-team green; link-checking + staleness CI green; a **distribution/partner runbook** (how a
  legal-aid org embeds, links, prints, or republishes the content; attribution + "not advice"
  preserved) ready.

- **M5 — Partner adoption & handoff (the deed).**
  *Goal:* a real organization distributes the content to real beneficiaries.
  *Exit (Definition of Shipped):* a secured partner distributes the attorney-reviewed content to its
  served population; ≥ 1 documented beneficiary use of a right; neutrality + currency controls
  independently verified; content attorney-signed-off; outcome recorded (no PII). *(Gated on a
  secured partner — TO BE SECURED.)*

- **M6 — Sustain & scale (post-delivery).**
  *Goal:* durable maintenance + careful expansion to a second domain (worker rights) or jurisdiction.
  *Exit:* maintenance rotation + review cadence (law-change → re-verify → **re-sign-off**) + outcome
  tracking; documented, attorney-gated process to add the next domain/jurisdiction; the most
  dangerous/charged "street rights" domains addressed **only** here, behind the hardened apparatus
  and extra safety review.

Dependencies flow M0 → M1 → M2 → M3 → M4 → M5. The **pilot jurisdiction+domain decision (made in
M0)** gates M2–M6 (it fixes the source corpus, source-reuse legality, and the reviewer's required
bar admission); M2 content blocks on M0 policy, the chosen jurisdiction, a vetted corpus (M1), and a
**secured licensed-attorney reviewer**; M5 blocks on a secured distribution partner.

---

## Work breakdown

The itemized, schema-mapped backlog lives in **`TASKS.md`**: ~18 tasks across milestones M0–M6 plus
a future backlog, each mapped to the Elyos Task JSON schema, with per-task acceptance criteria for
the most important items, milestone Definitions of Done, and a complete example Task JSON for the
first M0 task (the editorial / non-advice / UPL policy spec). The first build item is that policy
spec, reflecting its status as a hard product requirement; an early **pilot-jurisdiction+domain
selection** and a **minimal cited-vs-blank-slate kill-gate eval** at M1 are sequenced so HIGH-tier
content investment is gated on both a chosen corpus and an early thesis check.

---

## Governance, roles & stakeholders

- **Maintainer (Owner): TBD.** Owns the pipeline, content schema, agent-neutral core, CI, and merge
  quality.
- **Editorial reviewer (rotation):** owns plain-language, reading-level, **neutrality**, and
  **non-advice/UPL** review, independently of the drafter.
- **Licensed-attorney reviewers (HIGH tier): TO BE SECURED** — an attorney **admitted in the pilot
  jurisdiction** for the relevant domain (housing/tenant law for the wedge). Signs off all
  rights-stating / jurisdiction-specific content before it ships; recorded in the reviewers ledger
  with bar admission and consent.
  **Independence / COI mechanism:** a reviewer **recuses** from content touching a matter or party
  they currently represent. Sign-off is **version-scoped** — it attaches to a specific content
  version + citation set and does **not** carry forward to later edits (dovetails with the
  `lastVerified`/`validUntil` staleness model). **Name-use limits:** a reviewer's name and
  credentials may be published only for the versions they approved, with consent, and may not imply
  endorsement of the product as a whole or of content they did not review. **Disagreement fallback
  (attorney vs. maintainer):** the attorney holds a **veto on whether legal content is accurate and
  safe to ship** — a maintainer cannot override a "do not ship" on substance; the content does not
  ship, the disagreement is logged and escalated to Elyos governance / a second attorney for a
  tie-break. Where a single reviewer is a single point of failure, the project prefers securing a
  **second attorney** before relying on contested content. **Bar-rule note:** the project confirms
  with reviewing attorneys that general-information review (vs. client advice) is compatible with
  their professional-responsibility obligations, and that crediting them does not create an
  attorney–reader relationship.
- **Accessibility reviewer:** verifies WCAG 2.2 AA + offline legibility.
- **Steward (last-mile owner): TO BE SECURED** — owns the partner relationship and the
  distribution/adoption that constitutes shipping.
- **Partner / requestor: TO BE SECURED** — the legal-aid org, tenant union, worker center,
  civil-liberties group, or law-school clinic that distributes the content to beneficiaries.
- **Community / board:** the CC-BY vs CC-BY-SA license choice, the Astro-vs-Eleventy decision, and
  domain-expansion (especially to "street rights") go through Elyos governance.

---

## Dependencies & integrations

- **External services:** Anthropic Claude API (drafting/translation/lint aid behind the neutral LLM
  client; donated lane — the human runs their agent, the CLI never runs headless); static-site
  hosting/CDN.
- **Datasets / sources:** the pilot jurisdiction's primary law and official guidance (statutes,
  regulations, court rules, case law, agency guidance) and any **openly licensed** legal-aid
  material — each with verified reuse terms and recorded provenance. Public-domain legal corpora
  (e.g., Public.Resource.Org, CourtListener/Caselaw Access Project, official state legislature
  sites) for sourcing.
- **Upstream/reference for house style:** `planning/projects/public-official-guide/{PLAN,TASKS}.md`
  (sibling HIGH-tier legal/civic project).
- **Elyos pieces:** `packages/schema` (Task JSON), `CLAUDE.md` (work rules + refusal guardrails),
  `docs/good-deed-definition.md` (risk tiers), Elyos governance for license/edge-case decisions, the
  Elyos CLI (donated-lane task workspaces).
- **Human/decision dependencies (critical path):** the **pilot jurisdiction+domain decision (M0,
  gates M2–M6)**; a **secured licensed-attorney reviewer admitted in the jurisdiction** (blocks M2);
  and a **secured distribution partner/steward** (blocks M5).

---

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| Content drifts into individualized legal advice (UPL) | High | Critical | Non-advice/UPL lint built first + fail-closed; "general information, not advice" framing on every surface; editorial gate; **no case-intake / personal-facts feature exists**; attorney confirms general-info posture | Editorial reviewer / Attorney |
| Inaccurate or outdated rights claim relied on in a high-stakes moment | High | Critical | Primary-source citation required (coverage test); **attorney sign-off before ship**; **runtime staleness fail-safe** (`lastVerified`/`validUntil` auto-flags/withholds past-window claims until re-signed-off); "verify before relying" + route-to-help on every page | Attorney / Maintainer |
| Jurisdiction confusion (reader applies State A's law in State B) | High | High | Mandatory **jurisdiction label/selector on every page**; scope-level field (general vs jurisdiction-specific); lint fails on missing jurisdiction; no unscoped "this is the law" claims | Maintainer / Editorial |
| Content becomes partisan / advocacy / "resist-evade" | Medium | Critical | Neutrality policy + lint + red-team (≥ 8 cases per charged topic); independent editorial audit; refuse "resist/evade" framing; charged domains deferred to M6 behind hardened review | Editorial reviewer |
| Physically dangerous error in police/immigration/protest content | Medium | Critical | **Defer** these domains to M6; when built, extra safety review + attorney + (where relevant) practitioner review; never advise actions that escalate danger; factual rights only | Maintainer / Attorney |
| No attorney reviewer secured → M2 content blocked | Medium | High | Recruit via law-school clinics, bar pro-bono programs, legal-aid networks; **hard gate** (no attorney, no ship); dated plan (attorney by 2026-10-31) | Maintainer |
| No distribution partner secured → cannot reach Definition of Shipped | High | High | Honest `TO BE SECURED`/`verifiedNeed:false`; **dated partner-acquisition plan** + **build-vs-mothball/pivot rule** at ~2027-03-31 (contribute reviewed content to an existing commons, or mothball — not publish to no one) | Steward / Maintainer |
| Source license/copyright on annotations or compiled codes | Medium | Medium | Verify + record reuse terms per source; prefer edict-of-government primary law; **paraphrase**, never copy proprietary annotations; reuse third-party material only under an open license | Attorney / Maintainer |
| Over-reliance: reader treats content as their lawyer | High | High | Persistent "not legal advice" + route-to-help; general (not individualized) content only; no case-specific features | Maintainer / Attorney |
| Bad-faith reuse: someone publishes a stale/edited fork as "current" | Medium | Medium | CC-BY attribution + dated `lastVerified` stamped into content; clear versioning; "verify currency at source" note; consider CC-BY-SA | Maintainer |
| LLM hallucination of a right or citation | Medium | High | Retrieval-grounded drafting only; **no-source-no-claim**; citation-coverage test; attorney sign-off; eval harness | Maintainer |

---

## Security & privacy

**Threat surface.** Because there are **no user accounts and no reader data**, the classic
app-security surface (cross-tenant leakage, PII exfiltration, account takeover) is largely
**eliminated by construction**. The remaining surface is: (1) **content integrity** — a wrong,
stale, or tampered legal claim being served as current; (2) **supply-chain / build integrity** of
the static site and dataset; (3) **misuse of the pipeline** to generate refused content
(advice/partisan/harmful); and (4) **secrets handling** for any API keys used during drafting.

**Controls.**
- **Content integrity is the top control:** no-source-no-claim, citation coverage, attorney
  sign-off, and the **runtime staleness fail-safe** — a stale claim is flagged/withheld, never
  silently served. Content is versioned; the rendered page stamps `lastVerified`.
- **Editorial/non-advice/neutrality lint + red-team** run in CI as a release gate; a regression that
  lets advice/partisan/harmful framing through **fails the build**.
- **No reader PII**: no accounts, no case intake, no personal legal facts collected or stored; no
  third-party trackers (analytics, if any, aggregate-only — preferably none). Examples are fictional
  or de-identified.
- **Reviewer data** (attorney name/bar/jurisdiction) stored with consent, minimal, used only for
  sign-off + (consented) credit.
- **Build/supply-chain:** pinned dependencies, dependency + secret scanning in CI, reproducible
  static build, integrity-checked publish.
- **Secrets:** any drafting API key lives in the runner's environment only; **no secrets, tokens, or
  PII in logs, receipts, or committed files** (Elyos rule).
- **Abuse/misuse prevention:** the refused-content set (individualized advice; partisan/advocacy;
  resist/evade; help committing offenses or harming others) is enforced by the editorial layer and
  the agent's refusal guardrails, tested, and logged (reasons only, not sensitive content).

**Abuse note specific to this domain:** the most likely "misuse" is well-intentioned scope creep
(an author or contributor trying to be *more helpful* by giving advice or taking a side). The lint +
review gates are designed to catch helpful-but-wrong drift, not just malicious input.

---

## Sustainability & maintenance

Law changes; static legal content is a liability if it is not maintained. After delivery, a named
**maintenance rotation** owns the pipeline and the site; the **steward** owns the partner
relationship and outcome tracking. The **review cadence is enforced at runtime, not just on a
calendar**: each source's `lastVerified`/`validUntil` drives the fail-safe staleness behavior, so a
source past its review interval is **auto-flagged or withheld** until a reviewer re-verifies it and
an **attorney re-signs-off**. Material legal changes (new statute, amended rule, controlling
decision) trigger re-verification + re-sign-off before the affected content returns to normal
service. Outcomes are tracked with the partner (content distributed, documented beneficiary uses,
neutrality/currency audit status — **no PII, no engagement vanity metrics**). Expansion to a second
domain (worker rights) or jurisdiction — and especially to the deferred "street rights" domains —
follows a documented, attorney-gated process and only after the first is stable. The neutrality +
non-advice lint and the eval are maintained as living tests and expanded as new failure modes are
found.

---

## Open questions

- **Pilot jurisdiction + domain — decided in M0, not deferred** (it gates M2–M6: corpus, source-reuse
  legality, reviewer bar admission). **Selection criteria**, scored before M1 content work:
  (1) primary law reusable under the **edict-of-government** doctrine (no copyrighted compiled-code/
  annotation lock-in); (2) **high access-to-justice need + density of unrepresented people** in the
  domain; (3) an **available licensed-attorney reviewer** admitted there (and ideally a law-school
  clinic); (4) **manageable legal complexity** and a reasonably stable statutory regime; (5) a
  plausible **distribution partner** in that jurisdiction. Proposal: **tenant rights** (wedge). The
  specific jurisdiction is **TO BE SECURED**, but the decision rule + deadline (2026-08-31) are fixed.
- **Content license: CC-BY-4.0 vs CC-BY-SA-4.0?** CC-BY maximizes reuse; CC-BY-SA keeps derivatives
  open (prevents a closed, stale fork). Governance decision. (Tooling: MIT.)
- **Static generator: Astro vs Eleventy?** Both give fast, accessible, low/no-JS output; decision on
  maintainer familiarity + print/offline ergonomics.
- **Analytics: none vs. privacy-preserving aggregate?** Default lean: **none**, to keep the
  zero-PII posture absolute; revisit only if a partner needs reach metrics (aggregate-only).
- **Attorney compensation/crediting** — volunteer (clinic/pro-bono) vs. a future funded lane for
  review hours (hard budget cap) without compromising independence; and confirming professional-
  responsibility compatibility of general-info review.
- **How far to go on i18n at launch** — scaffolding now; which languages first is partner-driven and
  each needs combined legal + linguistic review (HIGH tier per language).
- **Sequencing of "street rights" (police/immigration/protest)** — deferred to M6; what extra safety
  + practitioner review is required before any of it ships, given the physical-danger profile.

---

## References

- Proposal: `governance/proposals/know-your-rights.md` *(TO BE WRITTEN — no proposal file exists yet)*
- Elyos work rules & refusal guardrails: `CLAUDE.md`
- Good-deed definition & risk tiers: `docs/good-deed-definition.md`
- Task JSON schema: `packages/schema/src/schemas.ts`
- Portfolio entry: `planning/ROADMAP.md` (Track 9 — Truth, governance & rights)
- Sibling HIGH-tier legal/civic plan for house style: `planning/projects/public-official-guide/{PLAN,TASKS}.md`
- Edict-of-government doctrine (source reuse): *Georgia v. Public.Resource.Org* (U.S. 2020)
- Public-domain legal corpora for sourcing: Public.Resource.Org; CourtListener / Caselaw Access
  Project; official state legislature / agency sites

---

## Appendix A — Improvements applied

Twenty-five specific improvements identified against the first draft and **applied** to the plan
above (and mirrored in `TASKS.md`). Each is a concrete change, not a vague intention.

1. **Reframed UPL from a disclaimer to a tested subsystem.** Made the non-advice / unauthorized-
   practice-of-law boundary the *first build item* with an automated, fail-closed content-lint gate
   in CI — paralleling how the sibling project treats guardrails as safety-critical.
2. **Made "information, not legal advice" a structural property, not a footer.** It is wired into the
   content template, asserted by lint, and present on every rendered surface with a route-to-help
   block.
3. **Added a mandatory jurisdiction label/selector on every page** and a `scope-level` field
   (general vs jurisdiction-specific), with lint failing on any unscoped "this is the law" claim — to
   kill the jurisdiction-confusion failure mode.
4. **Specified a runtime staleness fail-safe** (`lastVerified`/`validUntil`, auto-flag/withhold,
   re-verify + attorney re-sign-off) rather than a calendar "review someday" promise — because stale
   legal content is dangerous, not just untidy.
5. **Eliminated the entire reader-PII risk class by design**: no accounts, no case intake, no
   personal legal facts collected or stored. Stated explicitly in Scope, Architecture, Security, and
   a zero-PII success metric.
6. **Chose an explicit wedge — tenant rights, one jurisdiction** — with a written rationale
   (highest need, clearest statutes, lowest physical danger, best reviewer/partner pool), instead of
   an undifferentiated "tenant/worker/civil" scope.
7. **Deferred the physically dangerous domains** (police-encounter tactics, immigration enforcement,
   protest tactics) to M6 behind the hardened apparatus, with extra safety + practitioner review —
   so a launch-time error can't get someone hurt or detained.
8. **Added a dated partner-acquisition plan + build-vs-mothball/pivot decision rule** (jurisdiction
   by 2026-08-31, attorney by 2026-10-31, partner by 2026-12-31; pivot/mothball at ~2027-03-31)
   instead of an open-ended "find a partner."
9. **Defined a multi-gate review workflow with explicit order** (editorial → legal → accessibility →
   maintainer) and encoded it in CODEOWNERS + a PR checklist task.
10. **Made attorney sign-off version-scoped** with name-use limits and a recusal/COI rule, plus a
    disagreement fallback giving the attorney a substantive veto — so credibility can't be
    laundered across unreviewed edits.
11. **Required the reviewing attorney to be admitted in the jurisdiction** the content describes
    (not just "a lawyer"), and added a professional-responsibility/bar-rule compatibility check.
12. **Separated "cite" from "copy"** in the licensing section: paraphrase primary law in our own
    plain words, never copy proprietary annotations/compiled codes, reuse third-party material only
    under an open license — with a per-source reuse-terms record.
13. **Added an early minimal cited-vs-blank-slate kill-gate at M1** so HIGH-tier content investment
    is gated on an early thesis check, not discovered at M4.
14. **Added concrete, beneficiary-centric success metrics** (citation coverage, attorney-sign-off
    rate, non-advice lint pass, neutrality red-team pass, stale-content containment, reading level,
    WCAG, zero reader PII, partner adoption) with baselines/targets — not pageviews.
15. **Enforced reading-level ceilings** (explainers ≤ grade 8, cards ≤ grade 6) as an automated CI
    check, since the beneficiaries include low-literacy and limited-English readers.
16. **Specified an offline, printable wallet-card format** because people often need their rights at
    a moment with no connectivity.
17. **Operationalized neutrality** with a neutrality lint + red-team (≥ 8 cases per charged-topic
    category, per-version changelog), not just a "be non-partisan" sentence.
18. **Named the realistic adversary** — well-intentioned scope creep (authors trying to be *more*
    helpful by advising or taking a side) — and aimed the lint/review gates at helpful-but-wrong
    drift, not only malicious input.
19. **Single-sourced content** to both the site and the machine-readable dataset so the human page
    and the partner-reusable record can never drift apart.
20. **Made the dataset a first-class deliverable** (CC-BY) so partners can embed/translate/republish,
    multiplying reach beyond one website.
21. **Added a stale-fork mitigation**: stamp `lastVerified` + version into distributed content and
    consider CC-BY-SA, so a republished stale copy is detectable and currency is checkable at source.
22. **Scoped i18n correctly**: scaffolding now, but each translation treated as HIGH-tier requiring
    combined legal + linguistic review — avoiding the trap of machine-translating legal claims.
23. **Tightened refusal routing**: every refusal points to real, appropriate help (legal aid,
    relevant agency, attorney), making "route to help" the ethical posture rather than a bare "no."
24. **Aligned with Elyos lane rules**: Claude is a donated-lane drafting/lint aid behind a neutral
    LLM client; the CLI never runs headless and never "decides the law"; agent-neutral core preserved.
25. **Added a content-integrity + supply-chain security model** appropriate to a static publishing
    project (versioning, pinned deps, secret scanning, integrity-checked publish) instead of copying
    an app-style multi-tenant threat model that doesn't apply.

---

## Review sign-off

**Reviewer:** senior staff engineer + TPM (self-review pass for completeness and correctness against
`PLAN_SPEC.md`, `CLAUDE.md`, `docs/good-deed-definition.md`, and the Task JSON schema).

**Completeness:** all 17 required H2 sections present and in order; Appendix A (25 applied
improvements) and this sign-off added. `TASKS.md` provides milestone tables (M0–M6), per-task
acceptance criteria, milestone Definitions of Done, a backlog, and a schema-valid example Task JSON.

**Correctness checks performed and resolved:**
- **Risk tier consistency** — HIGH tier is stated in the executive summary, quality-gates section,
  roadmap gating, and every rights-stating task in `TASKS.md`; pipeline/site/infra tasks correctly
  carry low/medium. ✔
- **Guardrail coverage** — license/provenance (open/PD/CC only; cite-don't-copy), privacy/PII (zero
  reader PII by construction), strict non-partisanship (neutrality lint + red-team), and the
  mandatory licensed-attorney gate with "informational, not legal advice" framing are each present in
  Scope, Data/licensing, Quality gates, Risks, and Security. ✔
- **Partner honesty** — no partner or attorney reviewer exists; all delivery-dependent items are
  `TO BE SECURED` with `verifiedNeed: false`, and a dated acquisition plan + mothball/pivot rule are
  specified. ✔
- **Schema validity** — the example Task JSON in `TASKS.md` was checked field-by-field against
  `packages/schema/src/schemas.ts` (all required fields present; enum values valid; `verifiedNeed:
  false`; donated lane needs no `fundedBudgetUsd`). ✔
- **Elyos rules** — agent-neutral core, CLI-never-headless donated lane, no secrets in logs, and the
  refusal guardrails are reflected. ✔

**Known gaps / human decisions required (carried to *Open questions*):** the specific pilot
jurisdiction, the CC-BY vs CC-BY-SA content license, the static-generator choice, the analytics
posture, attorney compensation/independence model, i18n language order, and the extra safety review
required before any deferred "street rights" content. None block M0–M1; the attorney gate blocks M2
and the partner gate blocks M5, as designed.

**Verdict:** Approved as a v0.1.0 Draft. Build may begin at M0; HIGH-tier content (M2) must not
start until a licensed-attorney reviewer admitted in the chosen jurisdiction is secured.
