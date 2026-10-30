# LCC ⇄ SUMO: debate log

How the merged mapping was produced, who conceded what, and every point the coordinator had to rule on. Written so the exercise can be described as a method, not just reported as a result.

## 1. Setup

| Item | Value |
|---|---|
| Date | 2026-10-30 |
| Model | Three instances of the same model (Claude Opus 5.5): two advocates and one coordinator. |
| LCC Advocate | Instructed to argue for the interests of the Library of Congress Classification: keep LCC's structure, scope notes and coverage from being flattened to fit SUMO. |
| SUMO Advocate | Instructed to argue for the interests of SUMO: keep its formal distinctions (Physical/Abstract, Object/Process) from being misapplied to fit a shelving scheme. |
| Shared task | Two-way mapping of LCC to the top levels of SUMO, normalized for maximum completeness, with holes identified. |
| Shared inputs | Latest SUMO from GitHub (commit `2b55bb5`, 2026-10-28; both advocates cloned independently and their `Merge.kif` files are byte-identical). Latest LCC Outline PDFs from loc.gov (fetched 2026-10-30; no edition statement on the PDFs). "Top levels" fixed as the `Merge.kif` subclass tree from `Entity` to depth 4: 179 classes. |
| Grounding rule | Both advocates were told to verify every SUMO name against the `.kif` text and never invent one, and to mark unverified LCC ranges. |
| Rounds | Round 1: each advocate drafts its own direction in parallel. Round 2: each critiques the other's draft (concede / contest / compromise on every advocacy point, row-level disputes, hole classification, proposed rules). Neither advocate saw the other's critique. Merge: the coordinator applies agreed points, rules on the rest, and re-verifies every SUMO name by script. |
| Human input during the run | The user relayed one argument from a separate Claude Code session: SUMO's "formal relation classes have no LCC home" may be a granularity mismatch (BC, QA and BD do study relations), not a missing shelf. It was passed to the LCC Advocate as part of its round-2 brief. |

## 2. Round 1

| | LCC Advocate | SUMO Advocate |
|---|---|---|
| Direction drafted | LCC → SUMO | SUMO → LCC |
| Units mapped | 246 (21 main classes + 225 subclasses), plus 263 K jurisdiction codes as one block | 179 classes (depth 0–4) |
| Relation counts | 1 exact, 123 broader, 121 partial, 0 narrower, 1 none | 61 exact, 6 broader, 14 narrower, 64 partial, 34 none |
| Holes claimed | 14 hole categories covering 70+ LCC units | 34 SUMO classes with no LCC home |
| Advocacy points | 10 | 10 |
| Run time | ~38 min (89 tool calls) | ~9 min (63 tool calls) |

## 3. Round 2: concessions

| | LCC Advocate on SUMO's 10 points | SUMO Advocate on LCC's 10 points |
|---|---|---|
| Conceded | 6 (A2, A3, A4, A5, A8, A9) | 8 (points 2, 3, 4, 5, 7, 8, 9, 10) |
| Compromised | 4 (A1, A6, A7, A10) | 2 (points 1 and 6) |
| Contested outright | 0 | 0 |
| Row-level disputes raised | 34 SUMO→LCC rows | 32 LCC→SUMO rows (two of them whole patterns) |

### Converged independently

Neither advocate saw the other's critique, yet both proposed:

1. **The same structure.** Drop "primary/secondary". Use two co-equal slots, Discipline and Subject, with the relation scored per slot, plus facet fields for place, language and period. The SUMO Advocate added that SUMO's own `refers` relation reads the row: `(refers Discipline Subject)`.
2. **The same mirror-image framing of holes.** SUMO has formal machinery no shelf is about (relation properties, arities); LCC has shelves defined by form, audience or notation that no ontology should model. Both called these no-fault and agreed to exclude them from coverage, reported separately.
3. **The same rule for bearers vs content.** `Text` is a subject only for form-defined units.
4. **Overlapping false-friend lists** (`Medicine`, `Painting`, `Law`, `Index`, `Music`, `Literature`), each then extended by the other side.
5. **The same Q/T finding.** SUMO's top levels cannot separate science (Q) from technology (T); the LCC Advocate found it is worse: MILO declares `(subclass Engineering Science)`.

## 4. Coordinator rulings

Points that were contested, split, or raised by one side after the other had finished. Each was checked against commit `2b55bb5`.

| # | Issue | Positions | Ruling | Basis |
|---|---|---|---|---|
| 1 | History of a place (D, E, F; 22 units) | LCC draft: `FieldOfStudy` + `GeopoliticalArea`. SUMO critique: History is about events, so Subject = `Process` / `PoliticalProcess`, place as a facet via `eventLocated`. LCC side has not answered. | **SUMO critique adopted.** | Consistent with the LCC Advocate's own concession A5 (place reading in D–F); `eventLocated` exists in Merge (domains `Process`, `Object`). Keeps D distinguishable from G. |
| 2 | Religions BL–BR | LCC draft put `Group` primary, while its own point 4 says religions are not just groups. | **Doctrine first:** Subject = `Proposition` + `ReligiousProcess`; `BeliefGroup` instance as a group facet; gap G1. | The draft contradicted itself; the fix follows the LCC Advocate's stated position. |
| 3 | TX Home economics | LCC (round 1 and 2): cooking under `Maintaining`. SUMO critique: `Cooking` ⊂ `Making`. | **SUMO critique adopted.** | `(subclass Cooking Making)` is in Merge.kif. |
| 4 | `Quantity`, `FiniteQuantity` → QA | SUMO: `partial`. LCC: `narrower`. | **`partial`.** | QA covers geometry, logic and computing (not quantities), and physical quantities sit in QC. Overlap, not containment. |
| 5 | `Artifact` → T | SUMO: `partial`. LCC: `broader`. | **`partial`.** | T includes processes; `Artifact` includes art and clothing. |
| 6 | `ContentBearingPhysical` → P99 | SUMO: `broader`. LCC: `partial`. | **`partial`.** | Semiotics also studies abstract sign relations. |
| 7 | Real LCC gaps | SUMO conceded small LCC gaps (action theory; holes). LCC rebutted: BF608-635 and BF309-499 shelve action theory; GB561-649 shelves caves. | **0 LCC gaps.** | Evidence-based rebuttal; ranges from the outline. Single motor actions (poking) go to the granularity bin. |
| 8 | Four SUMO classes as "misfits" | LCC critique: `InheritableRelation`, `RelationExtendedToQuantities`, `CollectionOfProcesses`, `SingleAgentProcess` (weak) are ontology-engineering devices. SUMO side has not answered. | **Accepted** as SUMO defects D4–D6, excluded from coverage. | Documentation and usage checked in the repo. Open for the SUMO Advocate to contest. |
| 9 | BS The Bible | Both drafts: `Text` → `ChristianBible`. | **Both wrong.** Subject = `Proposition` + `ContentBearingObject` → `ChristianBible`. | In this commit `ChristianBible` ⊂ `Book` ⊂ `Document` ⊂ `ContentBearingObject`; `Book` is **not** under `Text`. Caught only by the coordinator's script check. |
| 10 | ML Literature on music | SUMO critique: Discipline = `Music` [MILO]. | **Discipline generic**, new gap G8 (no musicology class). | `Music` is a `Proposition`, not a FieldOfStudy; using it would break rule R1. |
| 11 | PS American literature | LCC: nationality of author is inexpressible in SUMO. SUMO: `authors` + `citizen` express it. | **SUMO correct.** A class is missing, not the ability to state the criterion. | Both relations are in Merge with suitable domains. |
| 12 | MILO `Painting` | Both round-1 drafts: "house-painting, not art". LCC critique corrected itself and the other side. | **Correction accepted:** too broad (covers `ArtPainting` and painting a kitchen), still the wrong ND target. | Documentation text in `Mid-level-ontology.kif` l.4841–4845. |
| 13 | `Sensing`, `Creation` | SUMO draft: `Sensing` → BF (exact); `Creation` → creation doctrine. LCC: false friends. | **LCC critique adopted.** | `Sensing` documentation scopes it to non-biological sensors; `Creation` ⊂ `InternalChange` with child `Making`. |
| 14 | Re-scoring the "vacuous broader" rows | SUMO critique: 58 LCC rows are `broader` only because `FieldOfStudy` is broader than anything. | **Re-scored on the Subject slot by rule** (87 rows): one subject class → `broader`; two or more, or originally `partial` → `partial`; general units → `generic`. | Mechanical and disclosed (provenance `RS`). Not a row-by-row judgement; a candidate for round 3. |
| 15 | Empty Subject slots | CC, GE, RJ had no subject after FieldOfStudy was moved out. | **Gap-filled** (provenance `F`): CC → `Artifact`; GE → `NaturalProcess` + `PhysicalSystem`; RJ → `Human`. | Coordinator judgement; the SUMO draft itself lists CC under `Artifact`. |

## 5. Result

| | LCC → SUMO | SUMO → LCC |
|---|---|---|
| Units | 246 | 179 |
| No-fault, excluded | 9 (8 form/audience classes + JX obsolete) | 31 (27 granularity + 4 SUMO misfits) |
| Mapped (exact/broader/narrower/generic) | 120 of 237 (51%) | 75 of 148 (51%) |
| Mapped or partial | 234 of 237 (99%) | 148 of 148 (100%) |
| Gaps on the other side | 3 units with no SUMO Subject at all (RV, RX, RZ), plus 9 SUMO gap families touching 39 units | 0 LCC gaps |
| Discipline named in SUMO (MILO FieldOfStudy subclass exists) | 131 of 238 (55%) | — |
| SUMO names failing script verification | 0 | 0 |

## 6. Open items (candidates for a round 3)

1. The LCC Advocate has not answered the SUMO critique's 32 row disputes; most are adopted here (provenance `S` / `S+R`). The largest is ruling 1 (D–F pattern).
2. The SUMO Advocate has not answered the LCC critique's 34 row disputes, the four misfit classes (ruling 8), or the "0 LCC gaps" rebuttal (ruling 7).
3. The 87 rule-scored rows (ruling 14) deserve a row-by-row pass; the SUMO Advocate estimated 15–25 should be `narrower`, and only one (NX) currently is.
4. The K jurisdiction appendix is mapped as one pattern; instance coverage of the 263 jurisdictions was not counted.

## 7. Notes for publication

- **Shared blind spots are real.** Two errors appeared in *both* advocates' drafts: the BS bearer chain (`Book` assumed to be a `Text`) and the "non-art" reading of `Painting`. The first was caught only by an external script check; the second by one advocate rereading the source text. Two instances of the same model do not supply independent error-checking on matters where they share priors; grounding in the source files did.
- **The debate stayed concrete.** Both advocates argued over named classes, verified ranges and documentation strings. The one move toward abstraction came from the coordinator, who resolved the first dispute by adding a meta-category ("no fault: granularity mismatch"); both advocates then accepted it with conditions (a mandatory LCC pointer; exclusion from numerator and denominator).
- **Asymmetry of assignments.** The LCC Advocate's task (outline PDFs, 225+ subclasses) took about four times as long as the SUMO Advocate's (one .kif file, 179 classes). Its draft is correspondingly larger and absorbed more of the critique.
- **Threats to validity.** One model family on all three seats. LCC at outline level only (Classification Web not reachable). LCC edition inferred, not stated. Ruling 14 is a heuristic.
