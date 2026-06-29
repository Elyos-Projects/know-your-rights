# Know-Your-Rights — Competitive & Improvement Analysis

> Analyst review of `PLAN.md` (v0.1.0 Draft) + `TASKS.md` for the Elyos good-deed project
> **know-your-rights**: neutral, primary-source-cited, jurisdiction-specific "know your rights"
> explainers (tenant → worker → civil rights), published as an open CC-BY commons + machine-readable
> dataset. HIGH risk-tier (legal content). Web-researched and cited throughout.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually strong for a HIGH-risk legal-content project. It already internalizes the
hardest lessons that have sunk or sanctioned others in this space. Reviewed against the dimensions
that matter most:

**Legal-information-not-advice boundary + UPL risk — strong, and correctly the #1 design fact.**
The plan treats the "information vs. advice" line as a *tested, fail-closed subsystem* (the
non-advice/UPL content-lint built first, M0 `know-your-rights-policy-001` + `lint-004`), not a
disclaimer footer. This is exactly right. The UPL line is not theoretical: Upsolve — a well-funded
nonprofit trying to let trained volunteers give *basic* debt-defense advice — won at the district
court (May 2022) but **lost at the Second Circuit in September 2025**, which held New York's UPL
rules *can* be enforced against even free, nonprofit, non-lawyer advice; the case is now headed for a
cert petition ([Pro Bono Institute](https://www.probonoinst.org/2025/10/07/setback-for-justice-advocates-in-upsolve-litigation/),
[Cato](https://www.cato.org/blog/upsolve-wins-right-give-basic-legal-advice)). The lesson for this
project: staying on the **general-information** side of the line is not optional caution, it is
existential, and the plan's bright-line refusal of "what should *I* do in *my* situation," case
intake, triage, document-drafting, and outcome prediction is the correct posture. *One gap:* the
plan asserts general legal information is "categorically distinct" from advice and therefore safe,
but UPL is defined **state-by-state** and some states sweep more broadly. Recommendation: the M0
policy should include a **per-jurisdiction UPL scan** (does the pilot state's UPL statute/bar
guidance reach generalized published information? — almost always no, but it must be confirmed by the
admitted attorney, not assumed), and the policy spec should cite the specific safe-harbor theory it
relies on (publishing/First-Amendment protection for general legal information, distinct from the
*conduct* of advising a specific person that tripped Upsolve).

**Jurisdiction-specificity + currency — strong; this is the genuine moat.** Mandatory jurisdiction
label + `scope-level` on every claim, lint failing on unscoped "this is the law" claims, and the
**runtime staleness fail-safe** (`lastVerified`/`validUntil` → auto-flag/withhold → re-verify +
attorney re-sign-off) directly target the two most common failure modes of existing free resources:
jurisdiction-blindness and silent staleness. This is well-judged — law changes fast in exactly the
launch domain (e.g., the UK's Renters' Rights Act banned Section 21 "no-fault" evictions from
1 May 2026, a generation-defining change [Citizens Advice](https://www.citizensadvice.org.uk/about-us/media-centre/press-releases/citizens-advice-responds-to-the-renters-rights-bill-becoming-law/);
US states constantly revise rent caps, eviction timelines, and minimum wage). *Gap:* the staleness
model is **time-triggered** (`validUntil`), but the most dangerous staleness is **event-triggered**
(a statute amended or a controlling case decided *before* the review window lapses). The plan
mentions "material legal changes trigger re-verification" in Sustainability but does not wire an
**event-driven trip** into the fail-safe. Recommendation: add a lightweight legislative/docket-watch
signal (even a manual maintainer checklist tied to the jurisdiction's legislature session + the
relevant agency) so a known change forces re-review immediately, not at `validUntil`.

**Accuracy + legal-expert/legal-aid review gate — strong; the hard, honest dependency.** The
mandatory **attorney-admitted-in-the-jurisdiction** sign-off, version-scoped, with recusal/COI,
name-use limits, and an attorney **veto** a maintainer cannot override, is the correct safety-
critical design and is the single biggest moat versus blank-slate LLM output. The plan is also
admirably honest that **no attorney and no partner is yet secured** (`TO BE SECURED`,
`verifiedNeed: false`) with a dated acquisition plan and a build-vs-mothball/pivot rule. *Risk to
flag:* this is the project's critical-path bottleneck and single point of failure. A volunteer
attorney's time is the scarcest input, and the plan loads *every* rights-stating claim onto them.
Recommendations: (a) make the **law-school clinic** path primary rather than one option among many —
clinics supply both a credentialed supervising attorney *and* student labor *and* a distribution
channel in one relationship (Stanford's Legal Design Lab model: it "assembled a national network of
housing law experts" to present eviction rules in plain language
[Stanford Legal Design Lab](https://law.stanford.edu/legal-design-lab/)); (b) design the content unit
so attorney review is **cheap and batchable** (review a jurisdiction's *source set* once, then
review *deltas*), or the gate will throttle the whole project.

**Sourcing to primary law — strong, with a real licensing trap correctly flagged.** The plan
leans on the edict-of-government doctrine (*Georgia v. Public.Resource.Org*, 2020) and the
cite-don't-copy rule, and correctly warns that **state annotations and compiled codes may carry
copyright** and **legal-aid materials are copyrighted unless openly licensed**. This is accurate and
is a trap that catches naive scrapers. *Gap:* the plan should name its clean primary-source pipes
explicitly as a selection criterion — Public.Resource.Org, the Caselaw Access Project /
CourtListener, and Cornell's Legal Information Institute are reliable PD/edict sources; the pilot
jurisdiction should be chosen partly for **machine-readable, openly-reusable statutes** (some states
lock their official code behind a vendor like LexisNexis/Westlaw with asserted copyright on the
compilation).

**Plain-language without losing accuracy — addressed, but under-tested.** Reading-level ceilings
(explainers ≤ grade 8, cards ≤ grade 6) are enforced in CI, which is good and rare. *Gap:* a Flesch-
Kincaid score does **not** measure whether the simplification *changed the law's meaning* —
plain-language rewriting is precisely where legal nuance gets dropped (a "may" becomes a "will," an
exception disappears). Recommendation: the attorney sign-off checklist must explicitly include a
**"does the plain-language version still state the law correctly, including caveats/exceptions?"**
item, and the eval (eval-008/015) should score *fidelity-after-simplification*, not just readability
and citation presence.

**No partisanship — strong, operationalized.** Neutrality lint + red-team (≥ 8 cases per charged
topic, per-version changelog) + independent editorial audit + deferral of charged "street rights"
domains to M6 is far beyond a "be non-partisan" sentence. Correctly identifies the realistic
adversary as **well-intentioned scope creep** (authors trying to be *more* helpful by advising or
taking a side), which is exactly how neutral resources drift.

**Accessibility / multilingual — strong on a11y, correctly conservative on i18n.** WCAG 2.2 AA +
offline printable wallet card + no-JS rendering directly serves low-connectivity, low-literacy
beneficiaries. Treating each translation as **HIGH-tier requiring combined legal + linguistic
review** (no machine-translated legal claims) is the right call — DOJ/ATJ research stresses that
language access *is* access to justice and that plain language makes accurate translation feasible
([DOJ ATJ 2023](https://www.justice.gov/atj/executive-summary-legal-aid-interagency-roundtable-2023-report)).
*Gap:* i18n is scaffolding-only at launch, but LEP populations are a core beneficiary group; the
plan should at least **commit a target language + partner-driven trigger** so multilingual isn't
indefinitely deferred.

**Harm from wrong legal info — correctly treated as safety-critical.** The plan repeatedly frames
errors as dangerous (a detention, an eviction hearing, a firing), not embarrassing. This is the
right register and is reinforced by the AI-hallucination evidence below.

**Minor completeness gaps:** (1) **No explicit professional-liability / "no attorney-client
relationship" + indemnity posture** beyond the banner — for a HIGH-risk legal publisher this should
be a named control (terms of use, reviewer-credit limits already exist, but the *entity's* liability
stance is unstated). (2) The **eval relies on an LLM judge** scoring legal accuracy — but LLMs are
themselves unreliable on law (see §5); the plan should weight the **attorney spot-check** as the
ground truth and treat the LLM judge as a pre-filter only. (3) **Partner-acquisition is the highest
delivery risk** and depends entirely on cold outreach; consider whether contributing into an
*existing* commons (LawHelp/LSC network, a clinic's public materials) should be the **primary** plan
A rather than the mothball/pivot plan B.

---

## 2. Competitive landscape

The "know your rights" / free legal-information space is crowded but **fragmented, jurisdiction-
patchy, and almost entirely non-machine-readable and non-openly-licensed** — which is precisely the
seam this project targets.

**ACLU "Know Your Rights"** — [aclu.org/know-your-rights](https://www.aclu.org/know-your-rights),
plus ~50 state affiliates (e.g., [ACLU-WA](https://www.aclu-wa.org/know-your-rights/),
[ACLU-DC](https://www.acludc.org/know-your-rights/police-immigration-or-fbi-stops/)).
*Strengths:* the most recognized brand in the category; excellent plain-language, wallet-card, and
downloadable lock-screen formats; multilingual; covers exactly the charged domains (police stops,
ICE/immigration, protest) this project defers. *Weaknesses:* explicitly **advocacy-organization**
content (the AC**LU**), so not neutral-by-construction and politically coded; **constitutional/
federal-rights-focused**, light on jurisdiction-specific statutory rights (tenant/worker); **not a
structured, openly-licensed dataset** others can embed/translate at scale; currency varies by
affiliate. The ACLU owns "street rights" mindshare — this project is wise to start on tenant/worker
where the ACLU is weak.

**LawHelp.org / Legal Services Corporation (LSC)** —
[lawhelp.org](https://www.lawhelp.org/), backed by [LSC](https://www.lsc.gov/).
*Strengths:* the canonical access-to-justice network; state-by-state referrals, court forms, self-
help tools from **actual legal-aid providers**; deep trust and reach; LSC funds the field. This is
the single most important **potential partner**, not just a competitor — contributing reviewed
content into this network is a credible plan-A distribution path. *Weaknesses:* content is a
**directory/aggregator of heterogeneous provider materials**, not a uniform, primary-source-cited,
machine-readable commons; quality, plain-language level, and currency vary widely by state provider;
not a reusable structured dataset; UX is dated.

**Citizens Advice (UK)** — [citizensadvice.org.uk](https://www.citizensadvice.org.uk/).
*Strengths:* the gold standard for plain-language, jurisdiction-specific rights guidance (housing,
employment, consumer, debt); statutory consumer advocate for energy/post; 19,000+ trained volunteers
across 1,900+ outlets; consistently current (e.g., immediate Renters' Rights Act guidance).
*Weaknesses:* **UK-only** (England & Wales law); **all-rights-reserved**, not an open commons or
dataset; gives **individualized advice** (a different, advice-side model that works because UK has no
US-style UPL bar). A proof that the *plain-language-by-jurisdiction* model works at scale; not a US
competitor and not openly reusable.

**Nolo** — [nolo.com](https://www.nolo.com/), legal self-help publisher since 1971.
*Strengths:* enormous, well-respected plain-English legal encyclopedia and DIY books across hundreds
of topics; trusted for education and empowerment ([Venture Smarter](https://venturesmarter.com/nolo-vs-legalzoom/)).
*Weaknesses:* **commercial / all-rights-reserved** (now part of Internet Brands/MH Sub I); sells
forms and lawyer-directory leads; **not openly licensed**, not a dataset, not citation-to-primary-
law transparent; breadth-over-depth and not always jurisdiction-pinned.

**Rocket Lawyer / LegalZoom** — [rocketlawyer.com](https://www.rocketlawyer.com/),
[legalzoom.com](https://www.legalzoom.com/).
*Strengths:* polished UX, document automation, on-demand attorney access (subscription vs. per-doc)
([ZenBusiness comparison](https://www.zenbusiness.com/rocket-lawyer-vs-legalzoom/)).
*Weaknesses:* **for-profit, transactional** (LLC formation, wills, contracts), aimed at small
business/consumers who can pay — *the opposite beneficiary* of this project; document-/intake-
oriented (the UPL-adjacent model this project explicitly refuses); not free, not open, not a rights
commons.

**Upsolve** — [upsolve.org](https://upsolve.org/).
*Strengths:* nonprofit, free, genuinely serves low-income beneficiaries (23,000+ families,
$1.1B debt erased); excellent plain-language "Learn" articles; foundation- and LSC-funded.
*Weaknesses:* **narrow** (Chapter 7 bankruptcy + debt); and most importantly, the **cautionary UPL
tale** — its attempt to give basic non-lawyer advice was blocked by the Second Circuit in 2025
([ABA Journal](https://www.abajournal.com/news/article/nonprofit-sues-over-unauthorized-practice-rules-that-prevent-free-nonlawyer-advice-in-debt-cases),
[Pro Bono Institute](https://www.probonoinst.org/2025/10/07/setback-for-justice-advocates-in-upsolve-litigation/)).
Validates this project's information-only line.

**Law-school clinics / Stanford Legal Design Lab** —
[law.stanford.edu/legal-design-lab](https://law.stanford.edu/legal-design-lab/).
*Strengths:* the methodological state-of-the-art for **plain-language, user-tested legal
information**; builds plain-language court forms and rights sites with courts/legal-aid; assembled a
national housing-law expert network for eviction-rights explainers; now building AI "co-pilots" for
legal-aid staff (Gates-funded). *Weaknesses:* **research/project-based**, not a single durable,
openly-licensed, machine-readable national commons; outputs are scattered across projects/courts.
The **best potential collaborator and reviewer-pool source** (a clinic = supervising attorney +
students + distribution).

**iCivics / Justia / Cornell LII / Oyez** — [icivics.org](https://ed.icivics.org/who-we-are),
[justia.com](https://www.justia.com/), [law.cornell.edu](https://www.law.cornell.edu/).
*Strengths:* iCivics is the premier **non-partisan civic-education** nonprofit (9M+ students, founded
by Justice O'Connor) — a model for neutral, free, at-scale civic content; Justia/LII/Oyez provide
free primary law and case access. *Weaknesses:* iCivics is **civics education, not applied rights**;
Justia/LII are **raw primary law**, not plain-language applied "what are my rights" guidance — they
are *upstream sources* for this project, not competitors.

**Net competitive read:** No existing player is simultaneously **(a) free, (b) neutral-by-
construction, (c) primary-source-cited, (d) jurisdiction-pinned, (e) attorney-reviewed with a
currency fail-safe, (f) openly licensed (CC-BY), and (g) machine-readable.** Each competitor holds
2–4 of these; none holds all. That intersection is the open seam.

---

## 3. Gaps we can fill

1. **An openly-licensed, machine-readable rights *dataset*** — every competitor publishes HTML for
   humans; none ships a CC-BY structured corpus partners can embed, translate, and republish. This
   is the project's first-class deliverable and is genuinely missing from the market.
2. **Neutral-by-construction rights content** — ACLU content is advocacy-coded; Citizens Advice is
   advice; this project's enforced non-partisan posture fills the "I don't trust either side" gap and
   makes the content adoptable by courts, bar programs, and across the political spectrum.
3. **Provable currency** — no free resource exposes per-claim `lastVerified`/`validUntil` with a
   runtime fail-safe; "is this still the law?" is the unanswered question on every existing site.
4. **Citation-to-primary-law transparency** — Nolo/Rocket Lawyer/most legal-aid pages assert the law
   without per-claim primary-source citations a reader (or partner attorney) can verify.
5. **Jurisdiction-pinned statutory rights in the tenant/worker lane** — ACLU is federal/
   constitutional; LawHelp is patchy by state; a uniform, deeply-sourced single-jurisdiction tenant
   pack done *excellently* beats fifty done shallowly.
6. **Offline, low-literacy, multilingual-ready artifacts** — printable ≤grade-6 wallet cards with
   a structured source that makes per-language legal+linguistic review tractable.
7. **A reusable publishing/review *engine*** — the lint + schema + staleness + attorney-gate pipeline
   is itself a gap: legal-aid orgs lack a turnkey way to publish trustworthy rights content.

---

## 4. Differentiators to win

1. **The review apparatus *is* the product** — attorney-gated, citation-enforced, fail-closed,
   currency-tripped. Anyone can prompt an LLM for "tenant rights"; nobody else ships
   *jurisdiction-correct, primary-source-cited, attorney-signed-off, provably-current* content. This
   is the moat, and it is the exact opposite of the documented AI-hallucination failure mode (§5).
2. **Open CC-BY commons + machine-readable dataset** — reach multiplies through partners (legal-aid
   networks, tenant unions, clinics), not just one website; embeddable and translatable.
3. **Neutral-by-construction** — adoptable where advocacy-branded content can't go (courts, bars,
   across the aisle), and trustworthy to readers who distrust advocacy orgs.
4. **Zero-PII, no-intake by design** — eliminates a whole privacy/security risk class *and* keeps
   the project firmly on the safe side of the UPL line that sank Upsolve's advice program.
5. **Depth-first wedge (one tenant jurisdiction, excellently)** — credibility through correctness in
   a low-physical-danger, high-need domain before touching charged "street rights."
6. **Currency fail-safe as a brand promise** — "we tell you when we're not sure it's current" is a
   trust differentiator no competitor offers.

---

## 5. Claude API leverage

**Where Claude is genuinely valuable (donated-lane drafting/lint aid behind the neutral LLM
client — Claude never "decides the law"):**

- **Retrieval-grounded plain-language drafting from supplied primary sources.** Given the vetted
  statute/reg/case text, Claude drafts the ≤grade-8 explainer / ≤grade-6 card — fast, consistent
  tone, good at simplification. Always grounded in provided sources, never blank-slate.
- **Jurisdiction-tagging and scope-level classification** — propose `jurisdiction` + general-vs-
  specific labels and surface unscoped claims for the lint to catch.
- **Translation drafting** for the i18n lane (draft only — every legal claim still gets combined
  legal + linguistic human review; no machine-translated law ships).
- **Reading-level rewriting** to hit the grade ceilings while flagging where simplification risks
  changing meaning (pair with the attorney "fidelity" check).
- **Powering the non-advice / neutrality lint and the eval judge** as a pre-filter — classify
  individualized-advice phrasings, loaded/partisan framing, and missing-citation/missing-jurisdiction
  nodes; draft red-team cases for charged topics.
- **Source-triage assistant** — summarize/flag candidate sources and their reuse terms for the
  human + attorney to verify (never the final reuse decision).

**Where Claude must NOT decide (hard guardrails — these are load-bearing):**

- **No legal advice, ever** — Claude must not answer "what should *I* do," predict outcomes, or
  apply law to a reader's specific facts. The UPL line is enforced in the lint, not left to the model.
- **Legal-expert / legal-aid review is blocking** — no Claude-drafted rights claim ships without
  attorney-admitted-in-jurisdiction sign-off. Claude drafts; the attorney decides.
- **Jurisdiction + currency are human-verified** — Claude may *propose* tags and flag staleness, but
  a human/attorney sets `lastVerified`/`validUntil` and confirms the jurisdiction.
- **Every claim sourced to primary law; no fabricated law or citations.** This is the central
  evidence-grounded risk: studies find general-purpose LLMs **hallucinate on 58–82% of legal
  queries**, and even purpose-built legal-research tools hallucinate in **>1 in 6** queries
  ([Stanford HAI](https://hai.stanford.edu/news/ai-trial-legal-models-hallucinate-1-out-6-or-more-benchmarking-queries));
  real attorneys have been **sanctioned, fined, and disqualified** for AI-fabricated citations
  ([Thomson Reuters](https://www.thomsonreuters.com/en-us/posts/technology/genai-hallucinations/),
  [Sterne Kessler 2025 review](https://www.sternekessler.com/news-insights/insights/ai-ip-year-in-reviewai-hallucinations-in-court-filings-and-orders-a-2025-review-of-sanctions-across-the-courts-and-rule-proposals/)).
  The **no-source-no-claim** rule + citation-coverage test + attorney sign-off are the precise
  antidote, and they are the project's entire reason to exist over a chatbot.
- **UPL-aware framing is non-negotiable** — Claude must keep content general and route to real help,
  never substitute an opinion.
- **The LLM eval judge is not ground truth** — given the above, attorney spot-check is authoritative;
  the Claude judge is a pre-filter only.

---

## 6. Ten concrete optimizations

1. **Add a per-jurisdiction UPL scan** to the M0 policy: have the admitted attorney confirm the
   pilot state's UPL statute/bar guidance does not reach generalized published information, and cite
   the specific publishing/First-Amendment safe-harbor theory the project relies on (learn from
   Upsolve's *conduct*-vs-*publishing* distinction).
2. **Make the staleness fail-safe event-driven, not just time-driven** — add a manual
   legislative-session + agency-guidance watch checklist per jurisdiction so a known statutory change
   trips re-review immediately, before `validUntil`.
3. **Pick the pilot jurisdiction partly for openly-reusable, machine-readable primary law** — confirm
   the official code/statutes are PD/edict-reusable (Public.Resource.Org, LII, CAP/CourtListener),
   not vendor-locked with asserted compilation copyright.
4. **Add a "simplification fidelity" gate** — readability score plus an explicit attorney checklist
   item ("does the plain-language version preserve the law's meaning, exceptions, and qualifiers?"),
   and score fidelity-after-simplification in the eval, not just citation presence.
5. **Lead with the law-school clinic relationship** — one clinic supplies supervising attorney +
   student reviewers + a distribution channel; design content so attorney review is **batchable**
   (review the source set once, then review deltas) to relieve the reviewer bottleneck.
6. **Make "contribute into an existing commons" (LawHelp/LSC, a clinic) the primary distribution
   plan**, not only the mothball/pivot fallback — it de-risks the M5 partner gate, the highest
   delivery risk.
7. **Publish a public eval/accuracy scorecard** that explicitly contrasts cited+reviewed content with
   raw-LLM legal answers, citing the hallucination evidence — turn the project's core differentiator
   into a trust artifact partners can point to.
8. **Add an explicit liability / "no attorney-client relationship" posture** (terms of use +
   entity stance), not just the reader-facing banner — appropriate for a HIGH-risk legal publisher.
9. **Commit a target i18n language + partner-driven trigger** so multilingual (a core LEP-beneficiary
   need) isn't indefinitely "scaffolding," given language access *is* access to justice
   ([DOJ ATJ](https://www.justice.gov/atj/executive-summary-legal-aid-interagency-roundtable-2023-report)).
10. **Ship the dataset with a stable citation/version API + `lastVerified` stamp baked into every
    record** so downstream embeds/forks carry currency metadata and a stale republished fork is
    detectable (reinforce with the CC-BY-SA consideration already raised).

---

## 7. Parallel & perpendicular spin-offs

- **Reusable legal-information engine (the strongest spin-off).** The schema + non-advice/neutrality
  lint + citation-coverage + staleness fail-safe + attorney-gate pipeline is a generic, agent-neutral
  **"trustworthy public legal/civic content" engine**. Extract it as a shared package so any
  jurisdiction or domain (or sibling project) can publish citation-grounded, currency-checked,
  reviewer-gated content. This is the most valuable perpendicular asset.
- **`benefits-navigator` (parallel).** Same engineering shape — plain-language, jurisdiction-pinned,
  primary-source-cited, currency-sensitive eligibility/benefits information — and the same UPL-
  adjacent "information not advice" boundary. Could share the engine, schema, and staleness machinery
  wholesale.
- **`public-official-guide` (sibling, already referenced as house-style upstream).** Same HIGH-tier
  legal/civic neutrality + sourcing apparatus; cross-pollinate the editorial/non-advice policy and
  review workflow.
- **`civics-exam-prep` (perpendicular).** Neutral, sourced civic content for naturalization/civics —
  iCivics-adjacent, lower legal risk, reuses the neutrality lint and accessibility/multilingual
  stack; a good lower-stakes proving ground for the engine.
- **`vital-info-translations` (parallel).** The per-language legal+linguistic review workflow and the
  "no machine-translated legal claims" guardrail generalize directly to translating other vital
  public-interest information.
- **Partnerships with legal-aid orgs / clinics (the distribution flywheel).** LawHelp/LSC network,
  ACLU affiliates (for the deferred street-rights domains, where they're strong), law-school housing/
  employment clinics, tenant unions, worker centers, and bar pro-bono programs — each is both a
  reviewer source and a distribution channel. Stanford Legal Design Lab is the natural methodology
  collaborator.
- **An MCP server (perpendicular tooling).** Expose the CC-BY rights dataset as a **read-only,
  citation-returning MCP server** so other agents/tools can retrieve *grounded, jurisdiction-tagged,
  attorney-reviewed, currency-stamped* rights claims with primary-source citations — turning the
  commons into infrastructure that *reduces* legal hallucination across the ecosystem (every answer
  comes back with a verifiable citation and a `lastVerified` stamp). High-leverage and directly
  aligned with the project's anti-hallucination thesis.

---

## 8. Open questions

1. **Plan-A distribution:** should contributing into an existing commons (LawHelp/LSC, a clinic's
   public materials) be the *primary* delivery path rather than a standalone site + later partner?
2. **Reviewer-bottleneck economics:** can a single volunteer attorney realistically gate *every*
   rights claim, or does the project need a clinic (attorney + students) or a funded review lane
   (hard-capped) from the start?
3. **UPL safe-harbor specifics:** what is the exact legal theory and per-jurisdiction confirmation
   that generalized published rights information is outside the pilot state's UPL reach?
4. **Pilot jurisdiction selection** still open (the M0 decision) — weight machine-readable/openly-
   reusable primary law and clinic availability heavily.
5. **CC-BY vs CC-BY-SA** — share-alike better deters stale closed forks but reduces reach; governance
   call (already flagged).
6. **i18n timing** — which language first and what triggers it, given LEP beneficiaries are core?
7. **Eval ground-truth** — how heavily to discount the LLM judge given documented legal-LLM
   unreliability; what attorney spot-check sampling rate is sufficient?
8. **Liability/insurance posture** for a HIGH-risk legal publisher — terms of use, disclaimers, and
   whether any E&O-style coverage is warranted before scaling beyond one jurisdiction.

---

### Key sources (web-researched)

- LSC Justice Gap 2022 — 92% of low-income Americans' civil legal problems get no/inadequate help:
  [justicegap.lsc.gov](https://justicegap.lsc.gov/resource/2022-justice-gap-report/)
- Upsolve UPL litigation (2nd Cir. 2025 setback): [Pro Bono Institute](https://www.probonoinst.org/2025/10/07/setback-for-justice-advocates-in-upsolve-litigation/),
  [ABA Journal](https://www.abajournal.com/news/article/nonprofit-sues-over-unauthorized-practice-rules-that-prevent-free-nonlawyer-advice-in-debt-cases),
  [Cato](https://www.cato.org/blog/upsolve-wins-right-give-basic-legal-advice)
- Legal-LLM hallucination (58–82% general / >1-in-6 legal tools; real sanctions):
  [Stanford HAI](https://hai.stanford.edu/news/ai-trial-legal-models-hallucinate-1-out-6-or-more-benchmarking-queries),
  [Thomson Reuters](https://www.thomsonreuters.com/en-us/posts/technology/genai-hallucinations/),
  [Sterne Kessler](https://www.sternekessler.com/news-insights/insights/ai-ip-year-in-reviewai-hallucinations-in-court-filings-and-orders-a-2025-review-of-sanctions-across-the-courts-and-rule-proposals/)
- ACLU KYR: [aclu.org/know-your-rights](https://www.aclu.org/know-your-rights) ·
  LawHelp/LSC: [lawhelp.org](https://www.lawhelp.org/), [lsc.gov](https://www.lsc.gov/) ·
  Citizens Advice: [citizensadvice.org.uk](https://www.citizensadvice.org.uk/) ·
  Nolo: [nolo.com](https://www.nolo.com/) ·
  Rocket Lawyer/LegalZoom: [zenbusiness comparison](https://www.zenbusiness.com/rocket-lawyer-vs-legalzoom/) ·
  Stanford Legal Design Lab: [law.stanford.edu/legal-design-lab](https://law.stanford.edu/legal-design-lab/) ·
  iCivics: [icivics.org](https://ed.icivics.org/who-we-are)
- DOJ Office for Access to Justice, language access: [justice.gov/atj 2023](https://www.justice.gov/atj/executive-summary-legal-aid-interagency-roundtable-2023-report)
