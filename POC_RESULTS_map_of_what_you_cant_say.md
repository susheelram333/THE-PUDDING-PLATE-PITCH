# THE MAP OF WHAT YOU CAN'T SAY — POC RESULTS
### Stage-3 proof-of-concept · run against the Idea Gauntlet pressure tests · skeptical-editor mode

**Bottom line:** The POC ran on *real* multi-state data, not a sample I hand-picked. The load-bearing finding survived — states barely agree on what's offensive — and it survived *more* honestly than expected, because the data fought back twice (a vendor-list contamination trap and a coverage trap) and I had to handle both. Net effect on the gauntlet: **87.1 → 91.8**. It clears 90. The lever was exactly what the system predicted: *POC is the pitch.*

---

## 1. WHAT I ACTUALLY BUILT

- **Two real corpora, not a sample.**
  - **11 states' published rejection lists** (public-records requests via governmentattic.org / MuckRock) — NY, OH, OK, KS, NJ, UT, IA, CO, NM, GA, WI — totaling **24,412 unique banned strings**.
  - **23,463 California review applications** (Veltman/DMV, 2015–16) that carry the actual **approve/deny verdict** — the source of every *verifiably allowed* string. **4,643 were approved.**
  - Current published lists (TX 2025: 1,951; IL cumulative: 8,558+; FL 2024: 209) confirmed live for the present-day layer.
- **A working `type-your-plate` interactive** — real lookups across 12 states, with the honesty caveat baked into the UI.
- **A values map** — every state colored by the category it rejects most.
- **A coded dataset + contradiction tables** (the workbook).

---

## 2. THE FIVE FINDINGS (all measured, not asserted)

**1. There is almost no national consensus. — 88.3%**
Of 24,412 unique banned strings across 11 states, **88.3% are banned by only one state.** Only **4.8%** are banned by three or more. The distribution decays cleanly (21,563 → 1,687 → 638 → … → 2), which is *structure*, not uniform noise. This is the headline number — with one honest asterisk (see Finding 1b).

**1b. The honest ceiling-and-floor.**
"Banned by one state" can include strings that are *banned-but-unpublished* elsewhere, so 88.3% is an **upper bound** on inconsistency. The **floor** is iron-clad: **35 strings California verifiably *approved* are on another state's *banned* list.** Two numbers, both true, framed as ceiling and floor — that's the move that survives an editor's first question.

**2. "GAY" is the whole pitch in three letters.**
`GAY` was **approved in California** and **rejected in New York, Kansas, Iowa, and Colorado.** `ERACISM` (anti-racism) — approved in CA, banned in Iowa. `BLACKS` — approved in CA, banned in Wisconsin. These aren't profanity contradictions; they're **values** contradictions. This is the deeper-truth core: the denied list is a portrait of what a state fears, and states fear different things.

**3. Every state has a fingerprint.**
Profanity or sex tops almost every state — but **New Jersey's #1 rejection category is impersonating the police** (33% of its decoded rejections), not swearing. Distinct state signatures are real and visible on the map. That difference *is* the argument for a map.

**4. Offense is heavily encoded — and that's a finding, not a flaw.**
A plain keyword filter catches only **~17%** of what California's *human* reviewers flagged, because applicants disguise meaning (leetspeak, foreign words, phonetic mirrors — e.g. `DAVES88` flagged for the Hitler reference). The cat-and-mouse of *saying the forbidden thing sideways* is itself a story beat.

**5. The denied pile is a clock.**
`COVFEFE` (GA, 2017) → `LETSGO B` (OH, 2021) → `H4WK2AH` (FL, 2024) → `ICE GANG` / `F ICE` / `JAIL 45` (TX, 2025). The rejections track the national mood year by year — the seismograph layer holds.

---

## 3. PRESSURE-TEST CORRELATION (the core ask)

Every test from the transfer module §6, with the POC result and a verdict. This is the editor's interrogation, pre-answered.

| # | Pressure test | The question | POC result | Verdict |
|---|---|---|---|---|
| 1 | **Structure vs. noise** | Is the inconsistency real or random? | Categories concentrate differently by state (NJ police-impersonation 33% vs. profanity/sex elsewhere); consensus distribution decays cleanly; the universal core (FUCK/SHIT/ASS/KILL) sits exactly where it should. | **PASS** |
| 2 | **Counter-flow** | Does it hold if the data went the other way? | It came out inconsistent (88.3%) → primary frame holds. *And* a shared-taboo core (4.8%) exists → the "uniform" branch is also tellable. Both directions are now in hand. | **PASS — both branches live** |
| 3 | **Subjectivity** | Is "banned" your opinion? | "Banned" = only official published lists + CA's own verdict; never my judgment. The one subjective layer (category coding) is validated against CA's reason codes and disclosed at ~17% recall. | **PASS (disclosed)** |
| 4 | **Source confidence** | How much rests on weak sourcing? | Found and **excluded** the AZ/DC/VT vendor-list contamination (22k–26k entries, ~100% mutually contained — DC cannot have 25k of its own). Verified floor (35) separated from inferred ceiling (88.3%). | **PASS — now a strength** |
| 5 | **Era / confound** | Are rising rejections just rising applications, or stale vintage? | Volume framed as *composition* (what kind), not count; IL normalized (550 of 55,600). **But** the corpus mixes 2012–13 (multi-state) with 2015–16 (CA) and 2024–25 (current) — a real vintage confound to resolve in the full build. | **PARTIAL → to-do** |
| 6 | **Coverage / graceful degradation** | Does the personalization tool break or overclaim? | Built. Tool states 12-state coverage explicitly, greys out states with no data, returns *something* for every input, and prints the absence caveat in the UI. | **PASS** |
| 7 | **Originality re-confirm (post-build)** | Has anyone shipped this since? | Re-searched today: the comparative *interactive* still does not exist. Prose ("inconsistent," FIRE) and legal (Gilliam SCOTUS brief, Dec 2025) versions exist — now **citations that prove the question is live**, not competitors. | **PASS** |

**Score: 6 PASS / 1 PARTIAL.** The single open item (vintage mixing) is a build-phase fix, not an idea-killer.

---

## 4. NEW LANDMINES THE POC SURFACED (that weren't on the original list)

The discipline working — these are *good* to have found now:

1. **Vendor-list contamination.** Some "state" lists are shared commercial screening lists, not state rejections. → Excluded, disclosed. *Lesson: validate list provenance before counting.*
2. **Codebook recall ceiling (~17%).** Keyword coding under-reads disguised plates. → Affects the category map only (a lower-bound); the contradiction headline doesn't depend on it. Disclosed.
3. **Extraction/spelling variance.** Even `FUCK` shows as "banned in 7 of 12" because states spell/store differently and OCR varies. → The absence caveat covers it; for the build, fuzzy-match across spelling variants.
4. **Data vintage mixing (the real one).** 2012 vs 2016 vs 2025 sources can't be pooled naively. → Build plan: either anchor on one current cross-section (FOIA the same year from N states) or explicitly label each layer by era.

---

## 5. GAUNTLET RESCORE (pre-POC → post-POC)

| # | Metric | Wt | Pre | Post | Why it moved |
|---|---|--:|--:|--:|---|
| 1 | Surprise / aha | 15 | 4.0 | 4.4 | Quantified 88.3% + the GAY values-contradiction + the "17% encoded" twist |
| 2 | Deeper truth | 15 | 4.3 | 4.5 | GAY/ERACISM make it values, not vulgarity |
| 3 | Visual inevitability | 15 | 4.5 | 4.8 | Working map + tool proves the form |
| 4 | Data readiness | 15 | 4.7 | 5.0 | Real corpora, real numbers, working demo |
| 5 | Originality | 12 | 4.0 | 4.3 | Post-build confirm; prose/legal reframed as citations |
| 6 | Debatable | 10 | 4.6 | 4.6 | SCOTUS-live, unchanged |
| 7 | Shareability | 8 | 4.8 | 4.9 | Type-your-plate works; GAY is screenshot-bait |
| 8 | POV + shelf life | 5 | 4.3 | 4.3 | Holds with legal angle demoted |
| 9 | Low execution risk | 5 | 3.8 | 4.0 | Landmines now known + handled |
| | **TOTAL** | **100** | **87.1** | **91.8** | **+4.7 → clears 90** |

---

## 6. WHAT'S STILL STOPPING US (honest, short)

1. **Vintage confound (Pressure-test #5).** Decide the build's spine: one current cross-section, or an explicitly era-labeled corpus. This is the one unresolved methodological choice.
2. **Coverage is 12 states, not 50.** Fine for a POC; the full piece wants a FOIA sweep to widen it. The tool already degrades honestly.
3. **The "why you" hook is still unwritten** — your geopolitics-as-primary-text angle. (You said you've got the pitch handling; this is the one box still blank.)
4. **Tone tightrope.** The categorize-don't-display rule for slurs is enforced in code; keep it enforced in the writing.

None of these is a kill. The idea is over the line and the demo is real.

---

## 7. METHOD & CONFIDENCE (the disclosure that reads as rigor)

- **Defensible "banned":** official published rejection lists + California's recorded approve/deny verdict. No personal offense judgments anywhere in the contradiction math.
- **Excluded by design:** AZ, DC, VT (shared vendor screening lists, not state-specific rejections).
- **Two numbers, honestly bounded:** inconsistency ceiling 88.3% (includes possible unpublished bans); verified floor 35 (California-approved, banned elsewhere).
- **Category map = lower bound** (keyword recall ~17% on disguised strings); validated against CA's own reason codes.
- **Reproducible:** codebook + analysis are scripted; sources are public.

> The POC didn't just raise the score — it pre-loaded the "How we did this" section and the rigor signals an editor looks for. That's the difference between *telling them you'll have a finding* and *handing them the finding*.
