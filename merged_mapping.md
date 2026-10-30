# LCC ⇄ SUMO: merged two-way mapping (normalized)

**Built from:** the LCC Advocate and SUMO Advocate drafts (round 1) and their cross-critiques (round 2). Every row records where its value came from.

| Item | Value |
|---|---|
| SUMO | `ontologyportal/sumo` commit `2b55bb59896b455cd4c3dc6c2d19e6cb3e924579` (2026-10-28). "Top levels" = `Merge.kif` subclass tree from `Entity` to depth 4: **179 classes** (1 / 2 / 10 / 41 / 125 by depth). |
| LCC | LC Classification Outline PDFs, all 21 classes, fetched 2026-10-30. No edition statement on the PDFs; schedule data at least as recent as September 2025. **246 units** (21 main classes + 225 subclasses) plus 263 K jurisdiction codes treated as one pattern. |
| Verification | Every SUMO name in this file is checked against the repo by `work/merge.py` (existence, depth, and that each refinement sits under its stated anchor). Problems found: **0**. |
| Companion files | `hole_register.md` (holes, gaps, SUMO defects, false friends) · `debate_log.md` (who conceded what, and coordinator rulings) · `lcc_sumo.sqlite` + CSVs (same data, queryable) |

## 1. Normalization rules (signed by both advocates)

Both critiques proposed six rules independently. They match closely; the merged versions are below. "Signed" means both critiques state the rule; differences in detail are noted.

| # | Rule | Source |
|---|---|---|
| R1 | **Two co-equal slots, no primary/secondary.** *Discipline* = a FieldOfStudy subclass (MILO/domain flagged), or *generic* when none exists, or *n/a* for form classes. *Subject* = Merge class(es) at d≤4 with an optional deeper refinement. The relation (SUMO relative to LCC) is scored **on the Subject slot**. A row reads as `(refers Discipline Subject)`. | Both (SUMO R1, LCC R1) |
| R2 | **Facets are fields, not targets**, each tied to a SUMO relation: place → `eventLocated` (D–F, place reading); polity → `GeopoliticalArea` agent reading (J, K, HC, HJ); language → `expressedInLanguage`; period → `holdsDuring`; nationality → `authors` + `citizen`. A facet whose instance exists is not a hole; a missing instance is an instance-level gap. | Both (SUMO R4, LCC R1) |
| R3 | **Bearer vs content.** `Text` / `ContentBearingObject` is the Subject only for form-defined units (A–AY, CD, CN, J, LH, LT, PZ, Z, ZA as `SymbolicString`). Units that shelve the works themselves (PN–PT, M, BS, CT) carry a `shelves-works` form flag; their content side is a SUMO gap where no content class exists. | Both (SUMO R2, LCC R6) |
| R4 | **Practices take a Process subject; roles never replace people; aspect is preserved.** Two LCC units with the same Subject must differ in Discipline (HE vs TF). | Both (SUMO R3, LCC R4) |
| R5 | **Honest coverage.** A fixed status vocabulary; no-fault rows (SUMO formal machinery; LCC form, audience and notational units) are excluded from numerator *and* denominator and reported separately; coverage is also reported by pattern. Granularity rows must carry an LCC pointer. | Both (SUMO R5, LCC R2) |
| R6 | **No mapping by name; no LCC nesting as `subclass`.** A false-friend list is mandatory; Discipline containment may use MILO `subField` only. Ranges are cited as printed. | Both (SUMO R6, LCC R3+R5) |

**Relation convention:** always SUMO relative to LCC. `broader` = the SUMO class is broader than the LCC unit; `narrower` = narrower; `partial` = overlap; `none` = no SUMO representation; `generic` = a general or second-order unit whose subject is the field itself.

## 2. Coverage

### LCC → SUMO (246 units)

| Measure | Count | Share |
|---|---|---|
| No-fault (form/audience classes A, AC, AI, AY, J, LH, LT, PZ; JX obsolete) | 9 | excluded |
| **Subject mapped** (exact / broader / narrower / generic), excluding no-fault | 120 of 237 | **51%** |
| Subject mapped or partial, excluding no-fault | 234 of 237 | 99% |
| Subject mapped, including no-fault rows in the denominator | 120 of 246 | 49% |
| SUMO gap (no Subject representation) | 3 | |
| **Discipline named** in SUMO (a FieldOfStudy subclass exists), of units where a discipline applies | 131 of 238 | **55%** |

| Subject relation | Count |
|---|---|
| exact | 1 |
| broader | 112 |
| narrower | 1 |
| partial | 119 |
| generic | 9 |
| none | 4 |

**By pattern** (rule R5; the 263 K jurisdiction codes count once, inside the polity pattern):

| Pattern | Units | Mapped | Partial | Gap / no-fault |
|---|---|---|---|---|
| subject/practice only | 100 | 60 | 36 | 4 |
| discipline × subject | 55 | 23 | 32 | 0 |
| discipline × polity (law/politics) | 36 | 2 | 34 | 0 |
| discipline × place (history) | 22 | 22 | 0 | 0 |
| discipline × language | 16 | 4 | 12 | 0 |
| discipline only (general/second-order) | 9 | 9 | 0 | 0 |
| form class | 8 | 0 | 0 | 8 |

### SUMO → LCC (179 classes)

| Measure | Count | Share |
|---|---|---|
| Too abstract to shelve (granularity, no fault, pointer given) | 27 | excluded |
| SUMO misfit (ontology-engineering classes, no fault on LCC) | 4 | excluded |
| **Mapped** (exact / broader / narrower), excluding no-fault | 75 of 148 | **51%** |
| Mapped or partial, excluding no-fault | 148 of 148 | 100% |
| Mapped or partial, including no-fault rows | 148 of 179 | 83% |
| Real LCC gaps | 0 | see `hole_register.md` §2 |

| Relation | Count |
|---|---|
| exact | 44 |
| broader | 13 |
| narrower | 18 |
| partial | 73 |
| none | 31 |

**Reading the numbers.** The two directions are not symmetric and should not be. Every non-trivial SUMO top-level class has *some* LCC shelf at coarse granularity, so SUMO → LCC is nearly complete. LCC → SUMO is limited at depth 4 because the top of SUMO cannot tell disciplines apart; the Discipline slot (MILO) and the facets carry that information, and its real holes are content-side (religion, literary works) and instance-side (historical regions, peoples).

## 3. LCC → SUMO table

Prov. codes: L LCC draft · A agreed by both · LS LCC self-correction · S SUMO critique proposal · R coordinator ruling · RS re-scored on Subject by rule R1 · F coordinator gap-fill. Gap IDs refer to `hole_register.md`.

| LCC | Caption | Discipline | Subject (d≤4 → refinement) | Facets | Other SUMO terms | Form | Rel | Status | Gaps | Prov | Note |
|---|---|---|---|---|---|---|---|---|---|---|---|
| A | General Works (main class) | *n/a (form)* | `Text` (d4); `ContentBearingObject` (d4) | — | — | polygraphic | partial | form (no-fault) | — | L | — |
| AC | Collections. Series. Collected works | *n/a (form)* | `Text` (d4) → `Series` [MILO]; `ContentBearingObject` (d4) → `Series` [MILO] | — | — | polygraphic | partial | form (no-fault) | — | A+Lc | Bibliographic-form class (collected works, series); not a physical `Collection`. LCC critique A7; SUMO had sent AC near `Set`. |
| AE | Encyclopedias | *generic* | `Text` (d4) → `ReferenceBook` [MILO] | — | `FactualText` (Merge d5) | reference | broader | mapped | G9 | L | — |
| AG | Dictionaries and other general reference works | *generic* | `Text` (d4) → `ReferenceBook` [MILO] | — | `Dictionary` [MILO] | reference | broader | mapped | — | L | — |
| AI | Indexes | *n/a (form)* | `Text` (d4) | — | — | polygraphic | broader | form (no-fault) | G9 | L | — |
| AM | Museums. Collectors and collecting | *generic* | `CollectionOfObjects` (d3) → `Museum` [MILO]; `Keeping` (d4) | — | — | — | partial | partial | — | A | Collecting is `Keeping` applied to a `CollectionOfObjects`; never `Set`. |
| AN | Newspapers | *generic* | `Text` (d4) → `Newspaper` [MILO] | — | `Periodical` [MILO] | serial | broader | mapped | — | L | — |
| AP | Periodicals | *generic* | `Text` (d4) → `Periodical` [MILO] | — | `Magazine` [MILO] | serial | broader | mapped | — | L | — |
| AS | Academies and learned societies | *generic* | `Organization` (d4) → `EducationalOrganization` (Merge d5) | — | — | — | broader | mapped | — | L | — |
| AY | Yearbooks. Almanacs. Directories | *n/a (form)* | `Text` (d4) → `FactualText` (Merge d5) | — | `ReferenceBook` [MILO] | polygraphic | broader | form (no-fault) | G9 | L | — |
| AZ | History of scholarship and learning. The humanities | `History` [MILO] | `Proposition` (d2) | — | — | — | partial | partial | — | RS | — |
| B | Philosophy (General) | `Philosophy` [MILO] | *(the field itself)* | — | — | — | generic | mapped | — | RS | General/second-order unit: Subject is the field itself (H11 pattern). |
| BC | Logic | `Philosophy` [MILO] | `Argument` (d3) → `DeductiveArgument` (d4); `LogicalOperator` (d4) | — | — | — | partial | partial | — | RS | — |
| BD | Speculative philosophy | `Philosophy` [MILO] | `Entity` (d0) | — | — | — | broader | mapped | — | RS | — |
| BF | Psychology | `Psychology` [MILO] | `BiologicalProcess` (d4) → `PsychologicalProcess` (Merge d5); `IntentionalPsychologicalProcess` (d4) | — | — | — | partial | partial | G5 | S | `PsychologicalProcess` ⊂ `BiologicalProcess` covers perception and emotion; BF1001-1999 (occult) is a G5 gap. Consistent with LCC critique (`Perception` → BF). |
| BH | Aesthetics | `Philosophy` [MILO] | `NormativeAttribute` (d4) → `SubjectiveAssessmentAttribute` (Merge d5) | — | — | — | broader | mapped | — | RS | — |
| BJ | Ethics | `Philosophy` [MILO] | `NormativeAttribute` (d4) → `ObjectiveNorm` (Merge d5) | — | `SubjectiveAssessmentAttribute` (Merge d5) | — | broader | mapped | — | RS | — |
| BL | Religions. Mythology. Rationalism | `Theology` [MILO] | `Proposition` (d2); `OrganizationalProcess` (d4) → `ReligiousProcess` (Merge d5) | group: `BeliefGroup` instances | `Deity` [People], `Atheism` [People] | — | partial | partial | G1 | S+R | Doctrine on the Abstract side; `BeliefGroup` instance kept as a group facet. Matches the LCC advocate's own point 4 / H8. |
| BM | Judaism | `Theology` [MILO] | `Proposition` (d2); `OrganizationalProcess` (d4) → `ReligiousProcess` (Merge d5) | group: `Judaism` (`BeliefGroup` instance) | `Judaism` [People], `JewishHoliday` [Media] | — | partial | partial | G1 | S+R | Doctrine on the Abstract side; `BeliefGroup` instance kept as a group facet. Matches the LCC advocate's own point 4 / H8. |
| BP | Islam. Bahaism. Theosophy, etc. | `Theology` [MILO] | `Proposition` (d2); `OrganizationalProcess` (d4) → `ReligiousProcess` (Merge d5) | group: `Islam` (`BeliefGroup`), `Bahai` (`ReligiousAttribute`, see D2) | `Islam` [People], `Bahai` [People] | — | partial | partial | G1 | S+R | Doctrine on the Abstract side; `BeliefGroup` instance kept as a group facet. Matches the LCC advocate's own point 4 / H8. |
| BQ | Buddhism | `Theology` [MILO] | `Proposition` (d2); `OrganizationalProcess` (d4) → `ReligiousProcess` (Merge d5) | group: `Buddhism` (`BeliefGroup` instance) | `Buddhism` [People] | — | partial | partial | G1 | S+R | Doctrine on the Abstract side; `BeliefGroup` instance kept as a group facet. Matches the LCC advocate's own point 4 / H8. |
| BR | Christianity | `Theology` [MILO] | `Proposition` (d2); `OrganizationalProcess` (d4) → `ReligiousProcess` (Merge d5) | group: `Christianity` (`BeliefGroup` instance) | `Christianity` [People], `Church` [People] | — | partial | partial | G1 | S+R | Doctrine on the Abstract side; `BeliefGroup` instance kept as a group facet. Matches the LCC advocate's own point 4 / H8. |
| BS | The Bible | `Theology` [MILO] | `Proposition` (d2); `ContentBearingObject` (d4) → `ChristianBible` [MILO] | — | `OldTestament` [MILO], `NewTestament` [MILO] | shelves-works | partial | partial | G1 | S+A+R | `ChristianBible` ⊂ `Book` ⊂ `Document` ⊂ `ContentBearingObject` (physical copies; **not** under `Text`, contrary to both drafts); BS covers versions and exegesis (content). |
| BT | Doctrinal Theology | `Theology` [MILO] | `Proposition` (d2) | — | — | — | broader | mapped | — | RS | — |
| BV | Practical Theology | *generic* | `OrganizationalProcess` (d4) → `ReligiousProcess` (Merge d5) | — | `Praying` [MILO], `ReligiousService` [MILO], `MissionOrganization` [MILO] | — | broader | mapped | — | L | — |
| BX | Christian Denominations | *generic* | `Organization` (d4) → `ReligiousOrganization` (Merge d5); `Group` (d4) → `ReligiousOrganization` (Merge d5) | — | `Church` [People], `RomanCatholicChurch` [People] | — | broader | mapped | — | L | — |
| C | Auxiliary Sciences of History (General) | `History` [MILO] | *(the field itself)* | — | — | — | generic | mapped | G3 | RS | General/second-order unit: Subject is the field itself (H11 pattern). |
| CB | History of Civilization | `History` [MILO] | *(the field itself)* | — | — | — | generic | mapped | G3 | RS | General/second-order unit: Subject is the field itself (H11 pattern). |
| CC | Archaeology | `Archeology` [Geography] | `Artifact` (d3) | — | — | — | broader | mapped | — | F | Archaeology studies material culture; SUMO side lists CC under `Artifact`. |
| CD | Diplomatics. Archives. Seals | *generic* | `CollectionOfObjects` (d3); `ContentBearingObject` (d4) → `Document` [MILO] | — | — | — | partial | partial | G3 | S | An archive is a physical collection of documents; `Seal`, `Archive` absent (G3). |
| CE | Technical Chronology. Calendar | *generic* | `PhysicalQuantity` (d4) → `TimeMeasure` (Merge d6); `TemporalRelation` (d3) | — | `TimeInterval` (Merge d8), `Year` (Merge d9), `Holiday` [MILO], `CalendarText` [ComputingBrands] | — | broader | mapped | G3 | L | — |
| CJ | Numismatics | *generic* | `Artifact` (d3) → `CurrencyCoin` [MILO] | — | `Currency` (Merge d7) | — | partial | partial | G3 | S | False friend: `CurrencyCoin` ⊂ `Text` in SUMO. No `Numismatics` discipline (G3). |
| CN | Inscriptions. Epigraphy | *generic* | `Text` (d4); `Artifact` (d3) | — | — | — | partial | partial | G3 | L | — |
| CR | Heraldry | *generic* | `Icon` (d4) → `Flag` [MILO]; `SocialRole` (d4) | — | — | — | partial | partial | G3 | L | — |
| CS | Genealogy | *generic* | `Group` (d4) → `FamilyGroup` (Merge d6) | — | `parent` (Merge d?), `ancestor` (Merge d?), `familyRelation` (Merge d?) | — | partial | partial | G3 | RS | — |
| CT | Biography | `History` [MILO] | `SentientAgent` (d4) → `Human` (Merge d6) | — | `HistoricalAccount` [MILO] | shelves-works | broader | mapped | — | S | CT is about persons; `Biography` [MILO] is the genre (form), not the subject. |
| D | History (General) | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `HistoricalAccount` [MILO], `War` (Merge d7) | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DA | Great Britain | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `UnitedKingdom` [CountriesAndRegions] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DAW | Central Europe | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `CentralEurope` [Geography] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DB | Austria - Liechtenstein - Hungary - Czechoslovakia | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Austria` [CountriesAndRegions], `Liechtenstein` [CountriesAndRegions], `Hungary` [CountriesAndRegions], `Czechoslovakia` [CountriesAndRegions] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DC | France - Andorra - Monaco | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `France` [CountriesAndRegions], `Andorra` [CountriesAndRegions], `Monaco` [CountriesAndRegions] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DD | Germany | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Germany` [CountriesAndRegions] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DE | Greco-Roman World | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | — | — | broader | mapped | G6 | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DF | Greece | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Greece` [CountriesAndRegions] | — | broader | mapped | G6 | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DG | Italy - Malta | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Italy` [CountriesAndRegions], `Malta` [CountriesAndRegions] | — | broader | mapped | G6 | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DH | Low Countries - Benelux Countries | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Belgium` [CountriesAndRegions], `Luxembourg` [CountriesAndRegions] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DJ | Netherlands (Holland) | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Netherlands` [CountriesAndRegions] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DJK | Eastern Europe (General) | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `EasternEurope` [Geography] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DK | Russia. Soviet Union. Former Soviet Republics - Poland | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Russia` [CountriesAndRegions], `SovietUnion` [CountriesAndRegions], `Poland` [CountriesAndRegions] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DL | Northern Europe. Scandinavia | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Sweden` [CountriesAndRegions], `Norway` [CountriesAndRegions], `Denmark` [CountriesAndRegions], `Iceland` [CountriesAndRegions], `Finland` [CountriesAndRegions] | — | broader | mapped | G6 | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DP | Spain - Portugal | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Spain` [CountriesAndRegions], `Portugal` [CountriesAndRegions] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DQ | Switzerland | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Switzerland` [CountriesAndRegions] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DR | Balkan Peninsula | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Turkey` [CountriesAndRegions], `Albania` [CountriesAndRegions] | — | broader | mapped | G6 | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DS | Asia | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Asia` [Geography] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DT | Africa | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Africa` [Geography] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DU | Oceania (South Seas) | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `Oceania` [Geography] | — | broader | mapped | — | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| DX | Romanies | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | people: `EthnicGroup` instance (Romanies) | `EthnicGroups_Gypsy` [mondial], `RomaniGroupLanguage` [Languages] | — | broader | mapped | G7 | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| E | History of the Americas: America (E11-143); United States (E151-889) | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `UnitedStates` [CountriesAndRegions], `NorthAmerica` [Geography], `EthnicGroups_NativeAmerican` [mondial] | — | broader | mapped | G7 | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| F | History of the Americas: US local history (F1-975); British America/Canada; Latin America (F1201-3799) | `History` [MILO] | `Process` (d2); `OrganizationalProcess` (d4) → `PoliticalProcess` (Merge d5) | place: `GeopoliticalArea` instance via `eventLocated` | `UnitedStates` [CountriesAndRegions], `Canada` [CountriesAndRegions], `Mexico` [CountriesAndRegions], `SouthAmerica` [Geography] | — | broader | mapped | G6 | S+R | History is about events located in a place, not the place as an object; place moved to a facet (SUMO critique row 8; LCC concession A5). |
| G | Geography (General). Atlases. Maps | `Geography` [MILO] | `GeographicArea` (d4); `Icon` (d4) → `Map` [MILO] | — | — | — | partial | partial | — | RS | — |
| GA | Mathematical geography. Cartography | `Cartography` [MILO] | `Icon` (d4) → `Map` [MILO] | — | — | — | broader | mapped | — | RS | — |
| GB | Physical geography | `Geography` [MILO] | `GeographicArea` (d4) → `LandForm` (Merge d5); `GeologicalProcess` (d4) | — | `WaterArea` (Merge d5) | — | partial | partial | — | RS | — |
| GC | Oceanography | *generic* | `GeographicArea` (d4) → `Ocean` [Geography]; `LiquidMotion` (d4) | — | `WaterArea` (Merge d5) | — | partial | partial | — | S | Currents, tides and waves as well as ocean regions. |
| GE | Environmental Sciences | *generic* | `NaturalProcess` (d3); `PhysicalSystem` (d2) | — | `Pollution` [Geography] | — | partial | partial | — | F | — |
| GF | Human ecology. Anthropogeography | *generic* | `GeographicArea` (d4); `Group` (d4) | — | — | — | partial | partial | — | RS | — |
| GN | Anthropology | `Anthropology` [MILO] | `Organism` (d4) → `Human` (Merge d6) | — | `EthnicGroup` (Merge d6) | — | broader | mapped | — | RS | — |
| GR | Folklore | *generic* | `Proposition` (d2) | — | `NarrativeText` (Merge d5), `FolkMusic` [Music] | — | partial | partial | — | RS | — |
| GT | Manners and customs (General) | *generic* | `SocialInteraction` (d4) → `Ceremony` [MILO]; `NormativeAttribute` (d4); `WearableItem` (d4) → `Clothing` (Merge d5) | — | `Wedding` [MILO], `Holiday` [MILO] | — | partial | partial | — | S | GT500-2370 clothing and fashion. |
| GV | Recreation. Leisure | *generic* | `RecreationOrExercise` (d4) → `Game` (Merge d5) | — | `Sport` (Merge d6), `Dancing` (Merge d5) | — | exact | mapped | — | L | — |
| H | Social sciences (General) | `SocialScience` [MILO] | *(the field itself)* | — | — | — | generic | mapped | — | RS | General/second-order unit: Subject is the field itself (H11 pattern). |
| HA | Statistics | `Statistics` [MILO] | `ProbabilityRelation` (d3); `Quantity` (d2) | — | — | — | partial | partial | — | S | — |
| HB | Economic theory. Demography | `Economics` [MILO] | `Transaction` (d4); `Group` (d4) → `GroupOfPeople` (Merge d5); `BiologicalProcess` (d4) | — | — | — | partial | partial | — | S | Economic theory (transactions) and demography (populations, birth, death). |
| HC | Economic history and conditions | `Economics` [MILO] | — | polity: `GeopoliticalArea` instance (agent reading) | `EconomicSystemAttribute` [Economy] | — | partial | partial | — | L | — |
| HD | Industries. Land use. Labor | *generic* | `Organization` (d4) → `Business` (Merge d5); `OrganizationalProcess` (d4) | — | `Industry` [MILO], `Working` [MILO] | — | partial | partial | — | RS | — |
| HE | Transportation and communications | `Economics` [MILO] | `Translocation` (d4); `Communication` (d4) | — | — | — | partial | partial | — | A+LS | Aspect class: economics of transport AND communications (HE6000-7500 postal; HE8701-9680.7 telephone). Same Subject as TF allowed; Discipline differs (rule R4). |
| HF | Commerce | *generic* | `Transaction` (d4) → `FinancialTransaction` (Merge d5); `Organization` (d4) | — | `Selling` (Merge d6), `Buying` (Merge d6), `Advertising` (Merge d6) | — | broader | mapped | — | L | — |
| HG | Finance | *generic* | `Transaction` (d4) → `FinancialTransaction` (Merge d5) | — | `FinancialInstrument` (Merge d6), `Currency` (Merge d7), `FinancialOrganization` [FinancialOntology], `InsurancePolicy` [MILO] | — | broader | mapped | — | L | — |
| HJ | Public finance | *generic* | `Transaction` (d4) → `Tax` [FinancialOntology]; `Organization` (d4) → `Government` (Merge d6) | — | — | — | broader | mapped | — | L | — |
| HM | Sociology (General) | `Sociology` [MILO] | `SocialInteraction` (d4); `Group` (d4) | — | — | — | partial | partial | — | RS | — |
| HN | Social history and conditions. Social problems. Social reform | `Sociology` [MILO] | `SocialInteraction` (d4) | — | — | — | partial | partial | — | RS | — |
| HQ | The family. Marriage. Women | *generic* | `Group` (d4) → `FamilyGroup` (Merge d6); `SocialInteraction` (d4) → `Wedding` [MILO] | — | `Woman` (Merge d7), `spouse` (Merge d?), `HumanChild` [MILO] | — | partial | partial | — | L | — |
| HS | Societies: secret, benevolent, etc. | *generic* | `Organization` (d4) → `Club` [MILO] | — | — | — | broader | mapped | — | L | — |
| HT | Communities. Classes. Races | *generic* | `Group` (d4) → `EthnicGroup` (Merge d6); `GeopoliticalArea` (d4) → `City` (Merge d5) | — | `SocialUnit` (Merge d6) | — | partial | partial | — | L | — |
| HV | Social pathology. Social and public welfare. Criminology | *generic* | `OrganizationalProcess` (d4) | — | `CriminalAction` [MILO], `Prison` [MILO], `Welfare` [MILO] | — | partial | partial | — | RS | — |
| HX | Socialism. Communism. Anarchism | *generic* | `Proposition` (d2); `Group` (d4) → `Communism` [Economy] | — | `SocialistEconomy` [Economy], `Anarchy` [Government] | — | partial | partial | — | L | — |
| J | General legislative and executive papers | *n/a (form)* | `Text` (d4); `Organization` (d4) → `Government` (Merge d6) | — | `Document` [MILO] | document-type | partial | form (no-fault) | — | L | — |
| JA | Political science (General) | `PoliticalScience` [MILO] | *(the field itself)* | — | — | — | generic | mapped | — | RS | General/second-order unit: Subject is the field itself (H11 pattern). |
| JC | Political theory | `PoliticalScience` [MILO] | `Proposition` (d2) | — | `FormOfGovernment` [MILO] | — | broader | mapped | — | RS | — |
| JF | Political institutions and public administration | *generic* | `Organization` (d4) → `GovernmentOrganization` (Merge d5); `OrganizationalProcess` (d4) → `Election` (Merge d5) | — | `Government` (Merge d6), `LegislativeOrganization` [Government] | — | broader | mapped | — | L | — |
| JJ | Political institutions and public administration (North America) | *generic* | `Organization` (d4) → `GovernmentOrganization` (Merge d5) | polity: `GeopoliticalArea` instance (agent reading) | `NorthAmerica` [Geography] | — | partial | partial | — | L | — |
| JK | Political institutions and public administration (United States) | *generic* | `Organization` (d4) → `GovernmentOrganization` (Merge d5) | polity: `GeopoliticalArea` instance (agent reading) | `UnitedStates` [CountriesAndRegions] | — | partial | partial | — | L | — |
| JL | Political institutions and public administration (Canada, Latin America, etc.) | *generic* | `Organization` (d4) → `GovernmentOrganization` (Merge d5) | polity: `GeopoliticalArea` instance (agent reading) | `Canada` [CountriesAndRegions] | — | partial | partial | — | L | — |
| JN | Political institutions and public administration (Europe) | *generic* | `Organization` (d4) → `GovernmentOrganization` (Merge d5) | polity: `GeopoliticalArea` instance (agent reading) | `Europe` [CountriesAndRegions] | — | partial | partial | — | L | — |
| JQ | Political institutions and public administration (Asia, Africa, Australia, Pacific Area, etc.) | *generic* | `Organization` (d4) → `GovernmentOrganization` (Merge d5) | polity: `GeopoliticalArea` instance (agent reading) | `Asia` [Geography], `Africa` [Geography], `Australia` [CountriesAndRegions] | — | partial | partial | — | L | — |
| JS | Local government. Municipal government | *generic* | `Organization` (d4) → `GovernmentOrganization` (Merge d5) | polity: `GeopoliticalArea` instance (agent reading) | `City` (Merge d5), `County` (Merge d5) | — | broader | mapped | — | L | — |
| JV | Colonies and colonization. Emigration and immigration. International migration | *generic* | `Translocation` (d4) → `Immigrating` [MILO] | polity: `GeopoliticalArea` instance (agent reading) | — | — | partial | partial | — | L | — |
| JX | International law (OBSOLETE: see JZ and KZ) | *generic* | — | — | — | — | none | obsolete | — | L | — |
| JZ | International relations | *generic* | `SocialInteraction` (d4) → `War` (Merge d7); `Organization` (d4) → `InternationalOrganization` [Government] | — | `Treaty` [MILO] | — | partial | partial | — | L | — |
| K | Law in general. Comparative and uniform law. Jurisprudence | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) → `DeonticAttribute` (Merge d6); `Proposition` (d2) → `Policy` [MILO]; `OrganizationalProcess` (d4) → `JudicialProcess` (Merge d6) | — | `LegalSystemAttribute` [Government] | — | partial | partial | — | S | Courts and procedure are processes; statutes and contracts are Proposition content. |
| KB | Religious law in general. Comparative religious law. Jurisprudence | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4); `Group` (d4) → `BeliefGroup` (Merge d6) | — | — | — | partial | partial | G1 | RS | — |
| KBM | Jewish law. Halakah | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | — | `Judaism` [People] | — | partial | partial | G1 | RS | — |
| KBP | Islamic law. Shariah. Fiqh | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | — | `IslamicLaw` [Government] | — | broader | mapped | — | RS | — |
| KBR | History of canon law | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | — | `RomanCanonLaw` [Government] | — | partial | partial | — | RS | — |
| KBU | Law of the Roman Catholic Church. The Holy See | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `RomanCanonLaw` [Government], `RomanCatholicChurch` [People], `HolySee` [CountriesAndRegions] | — | broader | mapped | — | RS | — |
| KD | Law of the United Kingdom and Ireland | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `UnitedKingdom` [CountriesAndRegions], `EnglishCommonLaw` [Government] | — | partial | partial | — | RS | — |
| KDC | Scotland | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Scotland` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KDE | Northern Ireland | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `NorthernIreland` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KDG | Isle of Man. Channel Islands | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `IsleOfMan` [CountriesAndRegions], `ChannelIslands` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KDK | Ireland (Eire) | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Ireland` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KDZ | America. North America | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `NorthAmerica` [Geography] | — | partial | partial | — | RS | — |
| KE | Law of Canada | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Canada` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KF | Law of the United States | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `UnitedStates` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KG | Latin America - Mexico and Central America - West Indies. Caribbean area | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Mexico` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KH | South America | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `SouthAmerica` [Geography] | — | partial | partial | — | RS | — |
| KJ | Europe | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Europe` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KJA | Roman law | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `CivilLaw` [Government] | — | partial | partial | — | RS | — |
| KJC | Regional comparative and uniform law (Europe) | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Europe` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KJE | Regional organization and integration (Europe) | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `EuropeanUnion` [Government], `InternationalOrganization` [Government] | — | partial | partial | — | RS | — |
| KK | Germany (KK-KKC); other European countries KKE-KKZ | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Germany` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KL | Asia and Eurasia: history of law, ancient Orient, Russia/Soviet Union and successor states | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Asia` [Geography], `SovietUnion` [CountriesAndRegions], `Russia` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KM | Asia: Middle East. Southwest Asia | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Asia` [Geography] | — | partial | partial | — | RS | — |
| KN | Asia: South Asia. Southeast Asia. East Asia | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `China` [CountriesAndRegions], `India` [CountriesAndRegions], `Japan` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KP | Asia: South, Southeast, East Asia (continued: Korea to Vietnam) | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Asia` [Geography] | — | partial | partial | — | RS | — |
| KQ | Africa (incl. law of indigenous peoples, KQ2010-9000) | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Africa` [Geography] | — | partial | partial | — | RS | — |
| KR | Africa (continued) | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Africa` [Geography] | — | partial | partial | — | RS | — |
| KS | Africa (continued) | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Africa` [Geography] | — | partial | partial | — | RS | — |
| KT | Africa (continued) | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Africa` [Geography] | — | partial | partial | — | RS | — |
| KU | Pacific Area: Australia, New Zealand | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Australia` [CountriesAndRegions], `NewZealand` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KV | Pacific Area jurisdictions | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Oceania` [Geography] | — | partial | partial | — | RS | — |
| KW | Pacific Area jurisdictions (continued) | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Oceania` [Geography] | — | partial | partial | — | RS | — |
| KWX | Antarctica | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) | polity: `GeopoliticalArea` instance (agent reading) | `Antarctica` [CountriesAndRegions] | — | partial | partial | — | RS | — |
| KZ | Law of nations | `FieldOfLaw` [MILO] | `NormativeAttribute` (d4) → `InternationalLaw` [MILO] | — | `Treaty` [MILO] | — | broader | mapped | — | RS | — |
| L | Education (General) | *generic* | `Guiding` (d4) → `EducationalProcess` (Merge d5) | — | `EducationalOrganization` (Merge d5) | — | broader | mapped | — | L | — |
| LA | History of education | `History` [MILO] | `Guiding` (d4) → `EducationalProcess` (Merge d5) | — | — | — | partial | partial | — | RS | — |
| LB | Theory and practice of education | *generic* | `Guiding` (d4) → `EducationalProcess` (Merge d5) | — | `Learning` (Merge d5), `Teacher` [MILO], `EducationalCourse` [MILO] | — | broader | mapped | — | L | — |
| LC | Special aspects of education | *generic* | `Guiding` (d4) → `EducationalProcess` (Merge d5) | — | — | — | partial | partial | — | L | — |
| LD | Individual institutions - United States | *generic* | `Organization` (d4) → `EducationalOrganization` (Merge d5); `GeopoliticalArea` (d4) → `UnitedStates` [CountriesAndRegions] | — | `University` [MILO], `College` [MILO], `School` [MILO] | — | broader | mapped | — | L | — |
| LE | Individual institutions - America (except United States) | *generic* | `Organization` (d4) → `EducationalOrganization` (Merge d5); `GeopoliticalArea` (d4) | — | `University` [MILO] | — | broader | mapped | — | L | — |
| LF | Individual institutions - Europe | *generic* | `Organization` (d4) → `EducationalOrganization` (Merge d5); `GeopoliticalArea` (d4) | — | `University` [MILO], `Europe` [CountriesAndRegions] | — | broader | mapped | — | L | — |
| LG | Individual institutions - Asia, Africa, Indian Ocean islands, Australia, New Zealand, Pacific islands | *generic* | `Organization` (d4) → `EducationalOrganization` (Merge d5); `GeopoliticalArea` (d4) | — | `University` [MILO] | — | broader | mapped | — | L | — |
| LH | College and school magazines and papers | *n/a (form)* | `Text` (d4) → `Periodical` [MILO]; `Organization` (d4) → `EducationalOrganization` (Merge d5) | — | — | document-type | broader | form (no-fault) | — | L | — |
| LJ | Student fraternities and societies, United States | *generic* | `Organization` (d4) → `Club` [MILO] | — | `Student` [MILO] | — | broader | mapped | — | L | — |
| LT | Textbooks | *n/a (form)* | `Text` (d4); `Guiding` (d4) → `EducationalProcess` (Merge d5) | — | — | document-type | partial | form (no-fault) | — | L | — |
| M | Music | *generic* | `ContentBearingObject` (d4) → `SheetMusic` [MILO]; `Proposition` (d2) → `Music` [MILO] | — | `MusicalComposition` [MILO], `MusicText` [MILO], `Recording` (Merge d5) | shelves-works | broader | mapped | — | A | Bearer-primary is legitimate: M shelves scores (`SheetMusic` ⊂ `ContentBearingObject`). |
| ML | Literature on music | *generic* | `Proposition` (d2) → `Music` [MILO]; `SocialInteraction` (d4) → `MusicalPerformance` [MILO] | — | — | — | partial | partial | G8 | S+R | Literature *about* music; `Text` is only the bearer. No musicology FieldOfStudy (G8), so Discipline is generic, not `Music`. |
| MT | Instruction and study | *generic* | `Guiding` (d4) → `EducationalProcess` (Merge d5) | — | `MusicalPerformance` [MILO], `MusicalInstrument` (Merge d5) | — | partial | partial | G8 | R | — |
| N | Visual arts | *generic* | `ArtWork` (d4) → `RepresentationalArtWork` (Merge d5) | — | — | — | broader | mapped | — | L | — |
| NA | Architecture | `Architecture` [MILO] | `StationaryArtifact` (d4) → `Building` (Merge d5) | — | — | — | broader | mapped | — | RS | — |
| NB | Sculpture | *generic* | `ArtWork` (d4) → `Sculpture` [MILO] | — | — | — | broader | mapped | — | L | — |
| NC | Drawing. Design. Illustration | *generic* | `ArtWork` (d4) → `Sketch` [MILO]; `Designing` (d4) | — | — | — | partial | partial | — | S | False friend: `Drawing` [MILO] is the act. |
| ND | Painting | *generic* | `ArtWork` (d4) → `PaintedPicture` [MILO]; `ContentDevelopment` (d4) → `ArtPainting` [MILO] | — | — | — | broader | mapped | — | A+LS | Never `Painting` or `Coloring`. |
| NE | Print media | *generic* | `ArtWork` (d4); `Icon` (d4) | — | — | — | partial | partial | — | L | — |
| NK | Decorative arts | *generic* | `Artifact` (d3) → `Furniture` [MILO]; `ArtWork` (d4) | — | `Pottery` [MILO], `Jewelry` [Economy] | — | broader | mapped | — | S | Decorative arts are mostly functional artifacts; the draft's own refinements (`Furniture`, `Pottery`) are ⊂ `Artifact`. |
| NX | Arts in general | *generic* | `ContentDevelopment` (d4); `ArtWork` (d4) | — | — | — | narrower | mapped | — | A | `ArtWork` is visual-only; "arts in general" includes performing and literary arts. Both critiques say narrower. |
| P | Philology. Linguistics | `Linguistics` [MILO] | `LinguisticExpression` (d4) → `Language` (Merge d5) | — | — | — | broader | mapped | — | RS | — |
| PA | Greek language and literature. Latin language and literature | `Linguistics` [MILO] | `LinguisticExpression` (d4) → `GreekLanguage` [Languages]; `Text` (d4) | language: via `expressedInLanguage` | `LatinLanguage` [Languages] | — | partial | partial | — | L | — |
| PB | Modern languages. Celtic languages | `Linguistics` [MILO] | `LinguisticExpression` (d4) → `CelticLanguage` [Languages]; `Text` (d4) | language: via `expressedInLanguage` | — | — | partial | partial | — | L | — |
| PC | Romance languages | `Linguistics` [MILO] | `LinguisticExpression` (d4) | language: via `expressedInLanguage` | — | — | broader | mapped | — | S | Languages only by caption; literatures are in PQ/PT/PR. Drop `Text`/`Literature`. |
| PD | Germanic languages. Scandinavian languages | `Linguistics` [MILO] | `LinguisticExpression` (d4) | language: via `expressedInLanguage` | `NorthGermanicLanguage` [Languages] | — | broader | mapped | — | S | Languages only by caption; literatures are in PQ/PT/PR. Drop `Text`/`Literature`. |
| PE | English language | `Linguistics` [MILO] | `LinguisticExpression` (d4) | language: via `expressedInLanguage` | — | — | broader | mapped | — | S | Languages only by caption; literatures are in PQ/PT/PR. Drop `Text`/`Literature`. |
| PF | West Germanic languages | `Linguistics` [MILO] | `LinguisticExpression` (d4) | language: via `expressedInLanguage` | — | — | broader | mapped | — | S | Languages only by caption; literatures are in PQ/PT/PR. Drop `Text`/`Literature`. |
| PG | Slavic languages. Baltic languages. Albanian language | `Linguistics` [MILO] | `LinguisticExpression` (d4) → `SlavicLanguage` [Languages]; `Text` (d4) | language: via `expressedInLanguage` | `BalticLanguage` [Languages], `AlbanianLanguage` [Languages] | — | partial | partial | — | L | — |
| PH | Uralic languages. Basque language | `Linguistics` [MILO] | `LinguisticExpression` (d4) → `UralicLanguage` [Languages]; `Text` (d4) | language: via `expressedInLanguage` | `BasqueLanguage` [Languages] | — | partial | partial | — | L | — |
| PJ | Oriental languages and literatures | `Linguistics` [MILO] | `LinguisticExpression` (d4) → `SemiticLanguage` [Languages]; `Text` (d4) | language: via `expressedInLanguage` | — | — | partial | partial | — | L | Geographic grouping, not a genetic family: expressible as a `UnionFn` of language classes, not a kind (no-fault, H6). |
| PK | Indo-Iranian languages and literatures | `Linguistics` [MILO] | `LinguisticExpression` (d4) → `IndoIranianLanguage` [Languages]; `Text` (d4) | language: via `expressedInLanguage` | — | — | partial | partial | — | L | — |
| PL | Languages and literatures of Eastern Asia, Africa, Oceania | `Linguistics` [MILO] | `LinguisticExpression` (d4) → `SinoTibetanLanguage` [Languages]; `Text` (d4) | language: via `expressedInLanguage` | `ChineseLanguage` (Merge d?), `NigerCongoLanguage` [Languages], `AustronesianLanguage` [Languages] | — | partial | partial | — | L | Geographic grouping, not a genetic family: expressible as a `UnionFn` of language classes, not a kind (no-fault, H6). |
| PM | Hyperborean, Indian, and artificial languages | `Linguistics` [MILO] | `LinguisticExpression` (d4) → `EskimoAleutLanguage` [Languages]; `Text` (d4) | language: via `expressedInLanguage` | `ArtificialLanguage` (Merge d6), `ConstructedLanguage` (Merge d7), `EsperantoLanguage` [Languages] | — | partial | partial | — | L | Geographic grouping, not a genetic family: expressible as a `UnionFn` of language classes, not a kind (no-fault, H6). |
| PN | Literature (General) | `Literature` [MILO] | `Text` (d4) → `FictionalText` (Merge d5) | — | `DramaticPlay` [MILO], `Journalist` [MILO], `MotionPicture` (Merge d5) | shelves-works | partial | partial | G2, G4 | R | — |
| PQ | French literature - Italian literature - Spanish literature - Portuguese literature | `Literature` [MILO] | `Proposition` (d2) | language: via `expressedInLanguage` | `FrenchLanguage` [Languages], `ItalianLanguage` [Languages], `SpanishLanguage` [Languages], `PortugueseLanguage` [Languages] | shelves-works | partial | partial | G2 | LS | Works shelved as `Text` → `FictionalText`; their content has no SUMO class (G2). |
| PR | English literature | `Literature` [MILO] | `Proposition` (d2) | language: via `expressedInLanguage` | `EnglishLanguage` [Languages], `UnitedKingdom` [CountriesAndRegions] | shelves-works | partial | partial | G2 | LS | — |
| PS | American literature | `Literature` [MILO] | `Proposition` (d2) | nationality: `(authors ?A ?T)` ∧ `(citizen ?A UnitedStates)` | `EnglishLanguage` [Languages], `UnitedStates` [CountriesAndRegions] | shelves-works | partial | partial | G2 | LS+S | LCC advocate said the nationality criterion is inexpressible; SUMO advocate showed `authors` + `citizen` in Merge express it. A class is missing, not the ability to state it. |
| PT | German literature - Dutch literature - Flemish literature since 1830 - Afrikaans literature - Scandinavian literature | `Literature` [MILO] | `Proposition` (d2) | language: via `expressedInLanguage` | `GermanLanguage` [Languages], `DutchLanguage` [Languages], `AfrikaansLanguage` [Languages] | shelves-works | partial | partial | G2 | LS | — |
| PZ | Fiction and juvenile belles lettres | *n/a (form)* | `Text` (d4) → `FictionalText` (Merge d5) | — | `Novel` [MILO] | audience | partial | form (no-fault) | G4 | L | — |
| Q | Science (General) | `Science` [MILO] | *(the field itself)* | — | — | — | generic | mapped | — | RS | General/second-order unit: Subject is the field itself (H11 pattern). |
| QA | Mathematics | `Mathematics` [MILO] | `Quantity` (d2); `Relation` (d2); `SetOrClass` (d2); `Graph` (d3); `ComputerProgram` (d4) | — | — | — | partial | partial | — | RS | — |
| QB | Astronomy | `Astronomy` [MILO] | `AstronomicalBody` (d3) | — | — | — | broader | mapped | — | RS | — |
| QC | Physics | `Physics` [MILO] | `Motion` (d3); `Radiating` (d4); `PhysicalQuantity` (d4) | — | — | — | partial | partial | — | RS | — |
| QD | Chemistry | `Chemistry` [MILO] | `ChemicalProcess` (d4); `Substance` (d4) | — | `Atom` (Merge d5), `Molecule` (Merge d5) | — | partial | partial | — | RS | — |
| QE | Geology | `Geology` [MILO] | `GeologicalProcess` (d4); `Substance` (d4) → `Mineral` (Merge d5) | — | — | — | partial | partial | — | RS | — |
| QH | Natural history - Biology | `Biology` [MILO] | `Organism` (d4); `BiologicalProcess` (d4) | — | — | — | partial | partial | — | RS | — |
| QK | Botany | `Botany` [MILO] | `Organism` (d4) → `Plant` (Merge d5) | — | `Fungus` (Merge d5) | — | broader | mapped | — | RS | — |
| QL | Zoology | `Zoology` [MILO] | `Organism` (d4) → `Animal` (Merge d5) | — | — | — | broader | mapped | — | RS | — |
| QM | Human anatomy | *generic* | `OrganicThing` (d4) → `AnatomicalStructure` (Merge d6) | — | `BodyPart` (Merge d7) | — | broader | mapped | — | S | — |
| QP | Physiology | `Physiology` [MILO] | `BiologicalProcess` (d4) → `PhysiologicProcess` (Merge d5) | — | — | — | broader | mapped | — | RS | — |
| QR | Microbiology | *generic* | `Organism` (d4) → `Microorganism` (Merge d5) | — | `Bacterium` (Merge d6), `Virus` (Merge d6) | — | broader | mapped | — | RS | — |
| R | Medicine (General) | `MedicalScience` [MILO] | *(the field itself)* | — | — | — | generic | mapped | — | RS | General/second-order unit: Subject is the field itself (H11 pattern). |
| RA | Public aspects of medicine | `MedicalScience` [MILO] | `OrganizationalProcess` (d4) | — | `Epidemic` [Medicine] | — | partial | partial | — | RS | — |
| RB | Pathology | *generic* | `BiologicalProcess` (d4) → `PathologicProcess` (Merge d5); `BiologicalAttribute` (d4) → `DiseaseOrSyndrome` (Merge d5) | — | — | — | partial | partial | — | RS | — |
| RC | Internal medicine | *generic* | `BiologicalAttribute` (d4) → `DiseaseOrSyndrome` (Merge d5) | — | `TherapeuticProcess` (Merge d5) | — | broader | mapped | — | RS | — |
| RD | Surgery | *generic* | `Repairing` (d4) → `Surgery` (Merge d6) | — | `TherapeuticProcess` (Merge d5) | — | broader | mapped | — | L | — |
| RE | Ophthalmology | *generic* | `OrganicThing` (d4) → `Eye` [MILO] | — | — | — | broader | mapped | — | RS | — |
| RF | Otorhinolaryngology | *generic* | `OrganicThing` (d4) → `Ear` [MILO] | — | — | — | broader | mapped | — | RS | — |
| RG | Gynecology and obstetrics | *generic* | `BiologicalProcess` (d4) → `Birth` (Merge d7) | — | `Woman` (Merge d7) | — | broader | mapped | — | RS | — |
| RJ | Pediatrics | *generic* | `OrganicThing` (d4) → `Human` (Merge d6) | — | `HumanChild` [MILO] | — | broader | mapped | — | F | Pediatrics: medicine of children. |
| RK | Dentistry | *generic* | `OrganicThing` (d4) → `Tooth` [MILO] | — | — | — | broader | mapped | — | RS | — |
| RL | Dermatology | *generic* | `OrganicThing` (d4) → `Skin` [MILO] | — | — | — | broader | mapped | — | RS | — |
| RM | Therapeutics. Pharmacology | *generic* | `Repairing` (d4) → `TherapeuticProcess` (Merge d5); `Substance` (d4) → `BiologicallyActiveSubstance` (Merge d5) | — | — | — | broader | mapped | — | L | — |
| RS | Pharmacy and materia medica | *generic* | `Substance` (d4) → `BiologicallyActiveSubstance` (Merge d5) | — | `Pharmacist` [MILO] | — | broader | mapped | — | L | — |
| RT | Nursing | *generic* | `Repairing` (d4) | — | `RegisteredNurse` [Biography] | — | partial | partial | — | RS | — |
| RV | Botanic, Thomsonian, and eclectic medicine | *generic* | — | — | — | — | none | SUMO-gap | G5 | S | "Broader" against `FieldOfStudy` was vacuous; no SUMO representation. |
| RX | Homeopathy | *generic* | — | — | — | — | none | SUMO-gap | G5 | S | — |
| RZ | Other systems of medicine | *generic* | — | — | — | — | none | SUMO-gap | G5 | S | — |
| S | Agriculture (General) | *generic* | `Maintaining` (d4) → `Agriculture` [MILO] | — | `Farm` [MILO], `Farming` [MILO] | — | broader | mapped | — | L | — |
| SB | Plant culture | *generic* | `Maintaining` (d4) → `Agriculture` [MILO]; `Organism` (d4) → `Plant` (Merge d5) | — | `Garden` [MILO] | — | broader | mapped | — | L | — |
| SD | Forestry | *generic* | `Maintaining` (d4); `GeographicArea` (d4) → `Forest` [Geography] | — | — | — | partial | partial | — | L | — |
| SF | Animal culture | `VeterinaryScience` [MILO] | `Maintaining` (d4); `Organism` (d4) → `DomesticAnimal` [MILO] | — | `Livestock` [Economy] | — | broader | mapped | — | L | — |
| SH | Aquaculture. Fisheries. Angling | *generic* | `Pursuing` (d4) → `Fishing` [Geography]; `Maintaining` (d4) | — | `Fish` (Merge d8) | — | broader | mapped | — | L | — |
| SK | Hunting sports | *generic* | `Pursuing` (d4) → `Hunting` (Merge d5); `RecreationOrExercise` (d4) | — | — | — | broader | mapped | — | L | — |
| T | Technology (General) | `Engineering` [MILO] | `Artifact` (d3) | — | — | — | broader | mapped | — | RS | — |
| TA | Engineering (General). Civil engineering | `Engineering` [MILO] | `Making` (d4) → `Constructing` (Merge d5) | — | — | — | broader | mapped | — | RS | — |
| TC | Hydraulic engineering. Ocean engineering | *generic* | `StationaryArtifact` (d4) → `Dam` [Geography]; `LiquidMotion` (d4) | — | `Canal` [Geography] | — | partial | partial | — | S | Hydraulics is fluid motion. |
| TD | Environmental technology. Sanitary engineering | *generic* | `StationaryArtifact` (d4) | — | `Sewage` [MILO], `Pollution` [Geography] | — | partial | partial | — | RS | — |
| TE | Highway engineering. Roads and pavements | `Engineering` [MILO] | `Making` (d4) → `Constructing` (Merge d5); `Transitway` (d4) | — | `Road` [MILO] | — | partial | partial | — | S | A practice takes a Process subject (rule R3). |
| TF | Railroad engineering and operation | `Engineering` [MILO] | `Translocation` (d4) → `Transportation` (Merge d5); `Transitway` (d4); `Device` (d4) | — | `RailroadTrack` [Transportation] | — | partial | partial | — | S | Caption is engineering *and operation*. |
| TG | Bridge engineering | `Engineering` [MILO] | `StationaryArtifact` (d4) → `Bridge` [Transportation]; `Making` (d4) → `Constructing` (Merge d5) | — | — | — | partial | partial | — | S | — |
| TH | Building construction | *generic* | `Making` (d4) → `Constructing` (Merge d5); `StationaryArtifact` (d4) → `Building` (Merge d5) | — | — | — | broader | mapped | — | L | — |
| TJ | Mechanical engineering and machinery | `MechanicalEngineering` [MILO] | `Device` (d4) → `Machine` (Merge d5) | — | `Engine` [MILO] | — | broader | mapped | — | L | — |
| TK | Electrical engineering. Electronics. Nuclear engineering | `ElectricalEngineering` [MILO] | `Device` (d4) → `ElectricDevice` [MILO] | — | `CommunicationDevice` [MILO] | — | broader | mapped | — | RS | — |
| TL | Motor vehicles. Aeronautics. Astronautics | *generic* | `Device` (d4) → `Vehicle` (Merge d6) | — | `Automobile` [Transportation], `Aircraft` [MILO], `Spacecraft` [MILO], `Rocket` [MILO] | — | broader | mapped | — | L | — |
| TN | Mining engineering. Metallurgy | *generic* | `Separating` (d4); `Substance` (d4) | — | `Digging` [MILO] | — | partial | partial | — | S | Extraction and refining processes. False friend: `Mining` [naics] is an IndustryAttribute. |
| TP | Chemical technology | *generic* | `ChemicalProcess` (d4) → `ChemicalSynthesis` (Merge d5) | — | `Manufacture` (Merge d5) | — | broader | mapped | — | RS | — |
| TR | Photography | *generic* | `ContentDevelopment` (d4) → `Photographing` [MILO]; `Icon` (d4) | — | `Photograph` [MILO], `Camera` [MILO] | — | broader | mapped | — | L | — |
| TS | Manufactures | *generic* | `Making` (d4) → `Manufacture` (Merge d5); `Product` (d4) | — | — | — | broader | mapped | — | L | — |
| TT | Handicrafts. Arts and crafts | *generic* | `Making` (d4); `Artifact` (d3) → `Clothing` (Merge d5); `Fabric` (d4) | — | `Sewing` [MILO] | — | broader | mapped | — | L | — |
| TX | Home economics | *generic* | `Making` (d4) → `Cooking` (Merge d5); `Maintaining` (d4) → `Cleaning` [MILO]; `SocialInteraction` (d4) → `ServiceProcess` (Merge d5) | — | — | — | partial | partial | — | S+R | Fact check: `(subclass Cooking Making)` in Merge.kif. The LCC draft (and its round-2 note) put cooking under `Maintaining`; `Food` moves to refinement (LCC own change). |
| U | Military science (General) | `MilitaryScience` [MILO] | *(the field itself)* | — | `MilitaryProcess` (Merge d5) | — | generic | mapped | — | RS | General/second-order unit: Subject is the field itself (H11 pattern). |
| UA | Armies: Organization, distribution, military situation | *generic* | `Organization` (d4) → `MilitaryOrganization` (Merge d6) | — | `Army` [MILO] | — | broader | mapped | — | L | — |
| UB | Military administration | *generic* | `OrganizationalProcess` (d4) → `Managing` (Merge d5); `Organization` (d4) → `MilitaryOrganization` (Merge d6) | — | — | — | broader | mapped | — | L | — |
| UC | Maintenance and transportation | *generic* | `Maintaining` (d4); `Translocation` (d4) → `Transportation` (Merge d5) | — | — | — | partial | partial | — | L | — |
| UD | Infantry | *generic* | `Organization` (d4) → `InfantryUnit` [Military] | — | — | — | broader | mapped | — | L | — |
| UE | Cavalry. Armor | *generic* | `Organization` (d4) → `MilitaryUnit` [MILO]; `Device` (d4) → `MilitaryVehicle` [Military] | — | — | — | partial | partial | — | L | — |
| UF | Artillery | *generic* | `Device` (d4) → `Weapon` (Merge d5); `Organization` (d4) | — | `ArtilleryGun` [MILO] | — | broader | mapped | — | L | — |
| UG | Military engineering. Air forces | *generic* | `Organization` (d4) → `AirForce` [MILO] | — | — | — | partial | partial | — | S | UG also covers military engineering; `Organization` covers only part. |
| UH | Other services | *generic* | `Organization` (d4) → `MilitaryService` [MILO]; `SocialInteraction` (d4) | — | — | — | partial | partial | — | L | — |
| V | Naval science (General) | `MilitaryScience` [MILO] | *(the field itself)* | — | — | — | generic | mapped | — | RS | General/second-order unit: Subject is the field itself (H11 pattern). |
| VA | Navies: Organization, distribution, naval situation | *generic* | `Organization` (d4) → `NavyBranchOfService` [Military] | — | — | — | broader | mapped | — | L | — |
| VB | Naval administration | *generic* | `OrganizationalProcess` (d4) → `Managing` (Merge d5); `Organization` (d4) → `NavyBranchOfService` [Military] | — | — | — | broader | mapped | — | L | — |
| VC | Naval maintenance | *generic* | `Maintaining` (d4) | — | `NavyBranchOfService` [Military] | — | partial | partial | — | L | — |
| VD | Naval seamen | *generic* | `Group` (d4) → `GroupOfPeople` (Merge d5); `SocialRole` (d4) | — | — | — | partial | partial | — | S | Seamen are people who hold a role; a role never replaces the people (rule R3). |
| VE | Marines | *generic* | `Organization` (d4) → `MarinesBranchOfService` [Military] | — | — | — | broader | mapped | — | L | — |
| VF | Naval ordnance | *generic* | `Device` (d4) → `Weapon` (Merge d5) | — | `Warship` [Military] | — | broader | mapped | — | L | — |
| VG | Minor services of navies | *generic* | `Organization` (d4) | — | — | — | partial | partial | — | L | — |
| VK | Navigation. Merchant marine | *generic* | `Guiding` (d4); `Translocation` (d4) | — | `Navigation` [NavalModeling], `MerchantMarine` [Transportation] | — | broader | mapped | — | L | — |
| VM | Naval architecture. Shipbuilding. Marine engineering | *generic* | `Making` (d4) → `Constructing` (Merge d5); `Device` (d4) → `Ship` [MILO] | — | `WaterVehicle` [MILO] | — | broader | mapped | — | L | — |
| Z | Books (General). Writing. Paleography. Book industries and trade. Libraries. Bibliography | `LibraryScience` [MILO] | `Text` (d4); `ContentDevelopment` (d4) → `Writing` (Merge d5); `Organization` (d4) → `Library` [MILO] | — | `Book` [MILO], `Publication` (Merge d5) | — | partial | partial | — | L | — |
| ZA | Information resources (General) | *generic* | `SymbolicString` (d4) → `DigitalData` [QoSontology] | — | `Database` [QoSontology], `WebSite` [Media] | — | broader | mapped | — | S | `DigitalData` ⊂ `SymbolicString` ⊂ `ContentBearingPhysical`, not `ContentBearingObject`. |

**K jurisdiction codes (263, KEA … KWW).** One pattern: Discipline `FieldOfLaw` [MILO]; Subject `NormativeAttribute` (d4) → `DeonticAttribute`; facet polity = the jurisdiction's `GeopoliticalArea` instance (agent reading). Relation `partial`. Instance-level gaps for historical polities (Bukhara, Khorezm, Transcaucasian SFSR, Confederate States) and special territories (West Bank). Full code list: `lcc_advocate_draft.md` Appendix A.

**Rule R4 check (units identical in Discipline, Subject, refinements, facets and related terms):** KJ/KJC; KM/KP; KQ/KR/KS/KT; KV/KW; LE/LG; PC/PE/PF. Each group differs only in which instance fills the facet (jurisdiction, region or language), which this table names generically. Not an aspect collision in the R4 sense.

## 4. SUMO → LCC table

Prov. codes: M SUMO draft · A agreed · SS SUMO self-correction · Lc LCC critique proposal · R coordinator ruling.

| SUMO class | d | Primary LCC | Secondary LCC | Rel | Status | Prov | Note |
|---|---|---|---|---|---|---|---|
| `Entity` | 0 | BD300-450 (Ontology) | BD10-41; AZ | partial | partial | Lc | Class A removed: A is defined by form, not by having "everything" as subject. |
| `Abstract` | 1 | BD300-450 (Ontology); BD95-131 (Metaphysics) | QA1-43; BC | partial | partial | M | Abstract objects are studied in metaphysics/ontology (universals, nominalism) and philosophy of mathematics. |
| `Physical` | 1 | QC (Physics) | BD493-701 (Cosmology); Q1-295 | partial | partial | M | Everything with spatiotemporal location; physics + philosophical cosmology are the general studies. LCC splits it over all of Q/R/S/T. |
| `Attribute` | 2 | BD300-450 (Ontology: qualities, properties) | BC | partial | partial | M | Theory of properties/qualities is ontology; no LCC unit is about "attributes" as such. |
| `Collection` | 2 | BD300-450 (whole/part, collectives) | AM (collecting) | partial | partial | A | QA248 removed: contradicted the SUMO side's own A7. |
| `List` | 2 | QA75.5-76.95 (data structures) | QA150-272.5; QA164 (unverified) | partial | partial | M | Ordered n-tuples: a formal/computational structure; shelved under computer science data structures and algebra/combinatorics. |
| `Object` | 2 | QC170-197 (constitution and properties of matter) | BD300-450; Q | partial | partial | M | Ordinary bodies; no single LCC unit; physical matter and ontology of substance are closest. |
| `PhysicalSystem` | 2 | Q300-390 (Cybernetics); TA168 (Systems engineering) | QC; QH540-549.5 | partial | partial | M | Complex physical systems are the object of systems theory/cybernetics and systems engineering. |
| `Process` | 2 | BD493-701 (Cosmology: change, causality, time) | QC120-168.85; BD300-450 | partial | partial | M | Process/change as such is a cosmological-metaphysical topic; specific processes are scattered across Q, R, T, H. |
| `Proposition` | 2 | BC (Logic) | BD143-237; content of works in all classes | broader | mapped | Lc+R | Direct subclasses include `FieldOfStudy`, `Music`, `Contract`, `Policy`, `Procedure`, `Argument`; logic studies one aspect. |
| `Quantity` | 2 | QA (Mathematics) | QC81-114 (Weights and measures) | partial | partial | SS+R | Direction ruling: QA ⊄ Quantity and Quantity ⊄ QA (physical quantities in QC) → partial. SUMO side said partial, LCC side narrower. |
| `Relation` | 2 | BC (Logic: logic of relations) | QA (set theory, algebra); BD300-450 | partial | partial | M | Relations as abstract entities belong to logic of relations and to foundational mathematics. |
| `SetOrClass` | 2 | QA (set theory, foundations) | BC131-135 (LCSH); BD300-450 | narrower | mapped | Lc | No set-theory range in the outline; set theory is a sub-topic inside QA and BC. |
| `Argument` | 3 | BC (Logic) | BC171-199; P302-302.87 (Discourse analysis) | exact | mapped | M | Arguments (premises+conclusion) are the paradigm subject of logic. |
| `Artifact` | 3 | T (Technology) | TS; NK; CC | partial | partial | SS+R | Ruling: T includes processes, `Artifact` includes art and clothing → overlap, not containment. SUMO side said partial, LCC side broader. |
| `AstronomicalBody` | 3 | QB495-903 (Descriptive astronomy) | QB500.5-785; QB799-903; QB455-456 | exact | mapped | M | Astronomical bodies are what descriptive astronomy describes. |
| `AutonomousAgent` | 3 | BF (Psychology: agency) | HM711-806; Q300-390; QA75.5-76.95 (AI) | partial | partial | M | Agents (people, organizations, AI) are scattered: psychology, sociology of organizations, AI. No LCC unit for "agent" as such. |
| `BinaryRelation` | 3 | BC (Logic of relations) | QA150-272.5 | narrower | mapped | M | Formal relation type; logic of relations / algebra of relations. |
| `CollectionOfObjects` | 3 | AM (Museums. Collectors and collecting) | HM711-806; BD300-450 | partial | partial | A | Follows A7 (both sides). |
| `CollectionOfProcesses` | 3 | — | — | none | SUMO-misfit | Lc+R | Ontology-engineering class, not a studied concept (defect D4). Not counted against LCC. |
| `ContactSite` | 3 | HE6000-7500 (Postal service); HE8701-9680.7 (Telephone) | AY (Directories) | partial | partial | M | Addressable contact points; LCC has postal/telephone services and directories, not the concept. |
| `ContentBearingPhysical` | 3 | P99-99.4 (Semiotics) | Z4-115.5; P87-96 | partial | partial | Lc+R | Ruling: semiotics also studies abstract sign relations; overlap → partial. LCC side said partial, SUMO side broader. `A` removed (form class). |
| `ContentBearingProcess` | 3 | P87-96 (Communication. Mass media) | P95-95.6 (Oral communication); PN1990-1992.92 (Broadcasting) | partial | partial | M | Content-expressing processes (speech, broadcast, sign) - communication studies. |
| `DualObjectProcess` | 3 | — (pointer) P (semantics/valency; unverified); BD | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `FieldOfStudy` | 3 | AZ (History of scholarship and learning) | Q1-295 (Science, General); each class A-Z as a whole | partial | partial | M | LCC IS a classification of fields of study; FieldOfStudy (Abstract/Proposition) corresponds to the scheme itself; AZ is where scholarship-in-general is shelved. |
| `FiniteQuantity` | 3 | QA (Mathematics) | QC81-114 | partial | partial | SS+R | Same ruling as `Quantity`. |
| `Graph` | 3 | QA164-167 (Combinatorics/graph theory; unverified range) | QA75.5-76.95 | exact | mapped | M | Graphs are studied in graph theory, under QA combinatorics (exact range unverified in outline). |
| `GraphElement` | 3 | QA164-167 (graph theory; unverified) | - | narrower | mapped | M | Nodes and arcs are components of graph theory. |
| `InheritableRelation` | 3 | — | — | none | SUMO-misfit | Lc+R | Ontology-engineering class, not a studied concept (defect D5). Not counted against LCC. |
| `IntentionalProcess` | 3 | BF (Psychology: will, motivation, action) | BJ (Ethics: human action); BD (philosophy of action) | partial | partial | M | Purposive action is studied in psychology of volition and philosophy of action. |
| `IntentionalRelation` | 3 | BF (Psychology) | BD143-237 (Epistemology); B (philosophy of mind) | partial | partial | M | Relations between an agent and the objects of its attitudes - philosophy of mind/intentionality. |
| `InternalAttribute` | 3 | BD300-450 (Ontology: intrinsic properties) | QC170-197 | partial | partial | M | Intrinsic properties as an ontological category. |
| `InternalChange` | 3 | BD493-701 (Cosmology: change) | QD; QH | partial | partial | M | Change internal to an object; studied generically in philosophy of change, specifically in chemistry/biology. |
| `Motion` | 3 | QC120-168.85 (Mechanics) | QA801-939 (Analytic mechanics); BD493-701 | exact | mapped | M | Motion is the object of mechanics. Note SUMO Motion is broader (includes weather, radiation) than LCC mechanics. |
| `NaturalProcess` | 3 | Q (Science); QH | QC; QE | partial | partial | A | Both critiques: partial. |
| `PartialValuedRelation` | 3 | — (pointer) QA (partial recursive functions; range unverified) | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Predicate` | 3 | BC (Logic: predicate logic) | QA9 mathematical logic (unverified range) | exact | mapped | M | Predicates are the subject of predicate logic. |
| `ProbabilityRelation` | 3 | QA273-280 (Probabilities. Mathematical statistics) | BC171-199 (inductive logic) | exact | mapped | M | Relations expressing probability - probability theory. |
| `Procedure` | 3 | QA75.5-76.95 (computer science: algorithms) | T57-57.97; TX642-840 (Cooking: recipes); MT | partial | partial | M | Sequence-dependent specifications (programs, recipes, scores, schedules) - abstract content. LCC splits by domain. |
| `QuaternaryRelation` | 3 | — (pointer) BC | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `QuintaryRelation` | 3 | — (pointer) BC | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Region` | 3 | G (Geography); GA (Mathematical geography) | QA440-699 (Geometry/Topology); BD493-701 (space) | partial | partial | M | Regions span geographic areas (G) and abstract places/surfaces (geometry, philosophy of space). |
| `RelationExtendedToQuantities` | 3 | — | — | none | SUMO-misfit | Lc+R | Ontology-engineering class, not a studied concept (defect D5). Not counted against LCC. |
| `RelationalAttribute` | 3 | BD300-450 (Ontology: relational properties) | HM; BC | partial | partial | M | Properties held by virtue of relations; generic ontology topic. |
| `SelfConnectedObject` | 3 | QC170-197 (properties of matter) | BD300-450 | partial | partial | M | Topologically connected bodies; mereotopology lives in ontology; matter in physics. |
| `Set` | 3 | QA (set theory; exact range unverified) | BC | exact | mapped | M | Sets are the subject of set theory. |
| `SingleAgentProcess` | 3 | — | — | none | SUMO-misfit | Lc+R | Ontology-engineering class, not a studied concept (defect D6). Not counted against LCC. |
| `SingleValuedRelation` | 3 | QA (functions; QA299.6-433 Analysis) | BC | narrower | mapped | M | Single-valued relations are functions in the mathematical sense. |
| `SpatialRelation` | 3 | QA440-699 (Geometry. Trigonometry. Topology) | BD493-701 (space); G | partial | partial | M | Spatial relations (part, connected, orientation) - geometry/topology and philosophy of space. |
| `TemporalRelation` | 3 | BD493-701 (Cosmology: time) | CE (Technical chronology. Calendar); QB | partial | partial | M | Temporal relations (before, during) - philosophy of time; chronology. |
| `TernaryRelation` | 3 | — (pointer) BC (polyadic logic) | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `TotalValuedRelation` | 3 | — (pointer) QA (total functions; range unverified) | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `UniqueList` | 3 | — (pointer) QA75.5-76.95 (data structures) | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `VariableArityRelation` | 3 | — (pointer) BC; QA75.5-76.95 | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Ambulating` | 4 | QP (Physiology: locomotion) | GV557-1198.995 (Sports: walking, running) | partial | partial | M | Walking/running studied as physiology of locomotion and as sport. |
| `AntisymmetricRelation` | 4 | — (pointer) QA150-272.5 (order/lattices; QA171.5 via LCSH) | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `ArtWork` | 4 | N (Visual arts) | NB–NK | narrower | mapped | Lc+A | N also holds NA (architecture), which `ArtWork` excludes, and art history. |
| `ArtificialIntelligenceAgent` | 4 | QA75.5-76.95 | Q300-390 (Cybernetics) | narrower | mapped | Lc | Q334-342 is not in the Q outline: stays unverified, removed from the cell. |
| `Attaching` | 4 | TJ1040-1119 (machinery); TS | TA | partial | partial | M | Fastening/joining processes appear in manufacturing technology. |
| `BinaryFunction` | 4 | QA (functions, algebra: binary operations) | QA150-272.5 | exact | mapped | M | Binary operations are algebraic objects. |
| `BinaryPredicate` | 4 | BC (Logic) | QA | narrower | mapped | M | Two-place predicates; logic of relations. |
| `BiologicalAttribute` | 4 | QH301-705.5 (Biology) | RB (Pathology); QP | partial | partial | M | Biological properties (disease, sex, developmental stage) - biology, pathology. |
| `BiologicalProcess` | 4 | QH301-705.5 (Biology); QP (Physiology) | RB (Pathology); BF (Psychology) | exact | mapped | M | Life processes - biology/physiology; PathologicProcess -> RB; PsychologicalProcess -> BF (depth 5). |
| `BodyMotion` | 4 | QP (Physiology: movement) | GV (Sports); GV1580-1799 dance (unverified) | partial | partial | M | Bodily movement - physiology/kinesiology, dance, sport. |
| `CaseRole` | 4 | P (Linguistics: syntax/semantics) | P325-325.5 (Semantics); BC | partial | partial | M | Thematic/case roles (agent, patient) are a linguistic-semantic notion (Fillmore case grammar). |
| `ChemicalProcess` | 4 | QD (Chemistry) | TP (Chemical technology) | exact | mapped | M | Chemical reactions are the subject of chemistry; industrial ones of TP. |
| `ClosedWorldPredicate` | 4 | — (pointer) QA75.5-76.95 | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Combining` | 4 | QD (Chemistry: mixtures) | TP; TS | partial | partial | M | Combining/mixing processes; scattered. |
| `CommercialAgent` | 4 | HF5001-6182 (Business) | HD2321-4730.9 (Industry); HD28-70 | exact | mapped | M | Profit-seeking agents are the subject of business/commerce. |
| `Communication` | 4 | P87-96 (Communication) | HE6000-7500; HE8701-9680.7; HF (advertising) | broader | mapped | Lc | Children include `Telephoning`, `Disseminating`. |
| `Comparing` | 4 | BF (Psychology: cognition, judgment) | BC | partial | partial | M | Mental comparison; cognitive psychology. |
| `ComputerProgram` | 4 | QA76.75-76.765 (Computer software) | QA75.5-76.95 | exact | mapped | M | Computer programs are software. |
| `ContentBearingObject` | 4 | Z4-115.5 (Books. Writing) | A; CD; CN | broader | mapped | A | Both: SUMO class is broader. |
| `ContentDevelopment` | 4 | PN (Literature (General): authorship) | Z4-115.5; QA76.75-76.765; P306-310; NC | partial | partial | M | Writing, programming, designing, translating, publishing - authorship processes; LCC splits by product. |
| `CorpuscularObject` | 4 | QC170-197 (constitution of matter) | BD300-450 | partial | partial | M | Objects with heterogeneous parts; formal mereology distinction (vs Substance). |
| `Creation` | 4 | T; TS | BD493-701 (philosophy of becoming, pointer only) | broader | mapped | Lc+R | False friend: `Creation` ⊂ `InternalChange`, child `Making`; not the doctrine of creation. |
| `Damaging` | 4 | TA495 (Disasters and engineering) | RD (Surgery: wounds and injuries); HV | partial | partial | M | Damage/injury: engineering failure, injury medicine, criminology. |
| `DeductiveArgument` | 4 | BC (Logic: deduction) | QA (mathematical logic, proof) | exact | mapped | M | Deduction is core logic. |
| `Designing` | 4 | NC (Drawing. Design. Illustration) | TA174 (Engineering design); NA; NK | partial | partial | M | Design process: NC (graphic design), TA174 engineering design, NA architectural design. |
| `Detaching` | 4 | — (pointer) TJ / TS (unverified) | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Device` | 4 | T; TJ | TK; TL; UF; VF; VM; ML (instruments); QC | broader | mapped | Lc | Dozens of direct children (`MusicalInstrument`, `Weapon`, `TransportationDevice`, `MeasuringDevice`). |
| `DirectedGraph` | 4 | QA164-167 (graph theory; unverified) | - | narrower | mapped | M | Specific graph type. |
| `DirectionChange` | 4 | QC120-168.85 (Mechanics) | VK (Navigation) | narrower | mapped | M | Change of direction; mechanics, navigation. |
| `Fabric` | 4 | TS1300-1865 (Textile industries) | TT (Handicrafts); NK (decorative textiles) | exact | mapped | M | Textiles/fabric manufacture. |
| `FiniteSet` | 4 | QA (set theory, combinatorics) | - | narrower | mapped | M | Finite sets - set theory/combinatorics. |
| `Food` | 4 | TX341-641 (Nutrition. Foods and food supply) | TP (food processing; TP368-456 unverified); TX642-840; GT (food customs) | exact | mapped | M | Food fit for humans. |
| `Function` | 4 | QA299.6-433 (Analysis) | QA150-272.5 (Algebra) | narrower | mapped | Lc | Functions are a topic within analysis and algebra. |
| `GasMotion` | 4 | QC (Physics: fluid/gas dynamics) | TL (Aeronautics: aerodynamics); QC851-999 | exact | mapped | M | Gas flow - aerodynamics/fluid mechanics. |
| `GeographicArea` | 4 | G (Geography) | GB; facet in D–F, J, K | partial | partial | Lc | Main LCC use is as a facet, not a subject. |
| `GeologicalProcess` | 4 | QE500-639.5 (Dynamic and structural geology) | QE521-545; GB400-649 | exact | mapped | M | Geological processes - dynamic geology. |
| `GeopoliticalArea` | 4 | JF/JK/JL/JN/JQ (Political institutions by country); JS (Local government) | D; E; F; G; K (jurisdictions) | partial | partial | M | Nations/states/cities: SUMO makes them both area AND agent. LCC treats them as places (D-F, G) and as polities (J, K). |
| `GraphArc` | 4 | QA164-167 (graph theory; unverified) | - | narrower | mapped | M | Edges of graphs. |
| `GraphNode` | 4 | QA164-167 (graph theory; unverified) | - | narrower | mapped | M | Vertices of graphs. |
| `Group` | 4 | HM711-806 (Groups) | GN (ethnic groups); BL–BX (belief groups); QL (animal groups; unverified) | broader | mapped | Lc | Children include `GroupOfAnimals`, `EthnicGroup`, `BeliefGroup` further down. |
| `Guiding` | 4 | LB (Theory and practice of education) | HD28-70 (Management); VK (Navigation); BF | partial | partial | M | Directing others' behavior: teaching, managing, steering. |
| `HoleRegion` | 4 | GB561-649 (caves and other landforms) | QM (anatomical openings); BD300-450 (theory of holes) | partial | partial | Lc | Was `none`. `Cave` ⊂ `HoleRegion` (verified). |
| `Icon` | 4 | P99-99.4 (Semiotics) | G1000-3122 (Atlases); G3180-9980 (Maps) | partial | partial | Lc | `Map` ⊂ `Icon` (verified); maps are the largest shelved body of icons. |
| `InductiveArgument` | 4 | BC (Logic: induction) | QA273-280; Q (scientific method) | exact | mapped | M | Inductive logic. |
| `IntentionalPsychologicalProcess` | 4 | BF (Psychology: cognition) | BD143-237 (Epistemology) | exact | mapped | M | Reasoning, learning, planning, classifying - cognitive psychology. |
| `IntransitiveRelation` | 4 | — (pointer) BC; QA150-272.5 | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `IrreflexiveRelation` | 4 | — (pointer) BC; QA150-272.5 | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Keeping` | 4 | AM; HF5484-5495 (Warehouses. Storage) | HV8301-9920.7 (Penology) | partial | partial | Lc+A | Was `none`. Child `Confining` (verified) covers imprisonment; SUMO side gave AM in A7. |
| `LineInSpace` | 4 | QA440-699 (Geometry) | - | exact | mapped | M | Lines - geometry. (No documentation string in Merge.kif.) |
| `LinguisticExpression` | 4 | P (Philology. Linguistics) | PA–PZ; Z; A (as tokens) | partial | partial | Lc | `Text` ⊂ `LinguisticExpression`, so every book is an instance; P studies language as a type. |
| `LiquidMotion` | 4 | TC (Hydraulic engineering. Ocean engineering) | GB651-2998 (Hydrology); QC (fluid mechanics) | partial | partial | M | Liquid flow - hydraulics, hydrology. |
| `Listening` | 4 | BF (Psychology: auditory perception) | P95-95.6 (Oral communication); MT (ear training) | partial | partial | M | Intentional hearing; perception psychology, speech communication. |
| `LogicalOperator` | 4 | BC (Logic) | QA (mathematical logic) | exact | mapped | M | Connectives and quantifiers - formal logic. |
| `Looking` | 4 | BF (Psychology: visual perception) | QP (Physiology of vision); RE | partial | partial | M | Intentional seeing; visual perception. |
| `Maintaining` | 4 | S (Agriculture) | TX (cleaning); UC; VC | broader | mapped | Lc | MILO children `Agriculture`, `Cleaning`, `Protecting`; S is the dominant home. |
| `Making` | 4 | TS (Manufactures) | TH; TT; TX (cooking); NB (sculpture) | broader | mapped | Lc+A | SUMO side conceded the lumping in A9; children include `Cooking`, `Constructing`, `Weaving`, `Sculpting`. |
| `Maneuver` | 4 | U164-167.5 (Tactics) | GV (Sports: tactics); GV1199-1570 (Games) | partial | partial | M | Moves within a Contest - tactics in war, sport and games. |
| `Meteoroid` | 4 | QB (Astronomy: meteors, meteorites; QB740-755 unverified) | QE (meteorites) | exact | mapped | M | Meteoroids - descriptive astronomy of the solar system. |
| `MotionDownward` | 4 | QC120-168.85 (Mechanics: falling bodies) | - | narrower | mapped | M | Downward motion - mechanics of falling bodies. |
| `MotionUpward` | 4 | QC120-168.85 (Mechanics) | - | narrower | mapped | M | Upward motion - mechanics. |
| `MultiGraph` | 4 | QA164-167 (graph theory; unverified) | - | narrower | mapped | M | Specific graph type. |
| `NonNullSet` | 4 | — (pointer) QA; BC | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `NormativeAttribute` | 4 | BJ (Ethics) | BH (Aesthetics); K (Law) | broader | mapped | Lc+A | SUMO side conceded the three-way span (A9); `Law` is an instance of `DeonticAttribute` under this class. |
| `NullSet` | 4 | — (pointer) QA (set theory; range unverified); BC | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Number` | 4 | QA101-(145) | number theory (range unverified) | exact | mapped | Lc | Range cited as printed (parenthesized end = no longer used). |
| `ObjectAttitude` | 4 | BF (Psychology: attitudes, desires) | BD (philosophy of mind) | partial | partial | M | Agent attitudes toward physical things (desires, needs). |
| `OrganicThing` | 4 | QH301-705.5 (Biology) | QD (organic chemistry; QD241-449 unverified); TS1950-1982 (Animal products) | partial | partial | M | Things produced by organisms - biology, organic chemistry, animal products. |
| `Organism` | 4 | QH301-705.5 (Biology (General)) | QK; QL; QR; QM; SB; SF | exact | mapped | M | Living organisms - biology; children Plant->QK, Animal->QL, Microorganism->QR, Fungus->QK600-638 (unverified). |
| `Organization` | 4 | HM786-806 (Organizational sociology) | HD; JF; BX; AS; LD–LG; UA/VA | broader | mapped | Lc | LCC shelves organizations by type across classes. |
| `OrganizationalProcess` | 4 | HD28-70 (Management. Industrial management) | JF (public administration); JF elections (JF1001-1191 unverified); UB | partial | partial | M | Processes of organizations: managing, hiring, elections, military/political/religious processes. |
| `PartialOrderingRelation` | 4 | QA (order theory, lattices; QA171.5 unverified) | - | exact | mapped | M | Partial orders - order theory. |
| `PerceptualAttribute` | 4 | BF (Psychology: sensation and perception) | QC350-467 (Optics: color); QC221-246 (Acoustics) | partial | partial | M | Colors, sounds, tastes as perceived qualities. |
| `PhysicalAttribute` | 4 | QC170-197 (Constitution and properties of matter) | TA401-492 (Materials, mechanics of materials) | exact | mapped | M | Physical properties of matter. |
| `PhysicalQuantity` | 4 | QC81-114 (Weights and measures) | QC1-75; T59-59.2 (Standardization) | exact | mapped | M | Measures and units - metrology. |
| `PhysicalState` | 4 | QC170-197 (properties of matter: states) | QC251-338.5 (Heat); QC310.15-319 | exact | mapped | M | Solid/liquid/gas - states of matter. |
| `Plan` | 4 | HD28-70 (Management: planning) | U150-155 (Military planning); HT (city planning, HT165-169 unverified) | partial | partial | M | Plans as abstract content; LCC files planning by domain. |
| `PlaneInSpace` | 4 | QA440-699 (Geometry) | - | exact | mapped | M | Planes - geometry. (No documentation string in Merge.kif.) |
| `PointInSpace` | 4 | QA440-699 (Geometry) | - | exact | mapped | M | Points - geometry. (No documentation string in Merge.kif.) |
| `Poking` | 4 | — (pointer) domain homes via children (TJ/TT; unverified) | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `PositionalAttribute` | 4 | QA440-699 (Geometry: orientation) | BD493-701 (space) | partial | partial | M | Orientation attributes (vertical/left) - geometry. |
| `PostalPlace` | 4 | HE6000-7500 (Postal service) | - | partial | partial | M | Places with postal addresses; postal service. |
| `Product` | 4 | TS (Manufactures) | HF5001-6182 (Business: marketing); HD9000-9999 | exact | mapped | M | Manufactured products - TS; product trade HD9000-9999. |
| `PropositionalAttitude` | 4 | BD143-237 (Epistemology: belief, knowledge) | BF (Psychology); BC | exact | mapped | M | Believing/knowing a proposition - epistemology. |
| `PseudoGraph` | 4 | QA164-167 (graph theory; unverified) | - | narrower | mapped | M | Graph with loops. |
| `Pursuing` | 4 | SK (Hunting sports) | SH (Fisheries); HF5415 shopping (unverified) | partial | partial | M | Doc examples: hunting, shopping, trawling, stalking. |
| `QuantityChange` | 4 | QA299.6-433 (Analysis: rates of change) | QC | partial | partial | M | Increase/decrease of quantity; generic. |
| `QuaternaryFunction` | 4 | — (pointer) QA150-272.5 | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `QuaternaryPredicate` | 4 | — (pointer) BC | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `QuintaryPredicate` | 4 | — (pointer) BC | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Radiating` | 4 | QC474-496.9 (Radiation physics) | QC350-467 (Optics); QC221-246 (Acoustics: RadiatingSound is a child); TK (radio) | exact | mapped | M | Emission/absorption of radiation. |
| `RecreationOrExercise` | 4 | GV (Recreation. Leisure) | GV557-1198.995 (Sports); GV1199-1570 (Games); RA (exercise, hygiene) | exact | mapped | M | Recreation and exercise - GV. |
| `ReflexiveRelation` | 4 | — (pointer) BC; QA150-272.5 | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Repairing` | 4 | TS (repair; unverified) | TJ1125-1345 (Machine shops); TL (vehicle maintenance); TX955-985 | partial | partial | M | Repair processes - scattered by object repaired. |
| `SaturationAttribute` | 4 | — (pointer) QC851-999 (humidity) | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Sensing` | 4 | TK (sensors) | QC (instruments); QA76 (AI input) | partial | partial | Lc+R | Verified: documentation scopes `Sensing` to non-biological sensors; psychology of senses → `Perception` → BF. |
| `SentientAgent` | 4 | BF (Psychology) | QL (animal behavior); BD (mind) | partial | partial | M | Agents with sentience; CognitiveAgent (depth 5) -> BF; Human (depth 6) -> GN, QM. |
| `Separating` | 4 | TP (Chemical technology: separation) | QD | partial | partial | M | Separation processes - chemical engineering unit operations. |
| `ShapeChange` | 4 | TA401-492 (Mechanics of materials: deformation) | QC | partial | partial | M | Deformation. |
| `SocialInteraction` | 4 | HM1001-1281 (Social psychology) | U (war); K (legal action); GV (sport); HF; GT; P87-96 | broader | mapped | Lc | Children `Contest`, `ChangeOfPossession`, `Ceremony`, `Communication`. |
| `SocialRole` | 4 | HM (Sociology: social roles, status) | HT (Classes); HD4801-8943 (occupations) | exact | mapped | M | Positions and statuses within groups - sociology. |
| `StateChange` | 4 | QC251-338.5 (Heat: phase transitions) | QC310.15-319 | exact | mapped | M | Melting, freezing, boiling. |
| `StationaryArtifact` | 4 | TA; TH | NA; TG; TF; TE | broader | mapped | Lc | Children include `Fence`, `Mine`, `Farm`, `Prison`, `Railway`, `Bridge`, `Building`; NA is design of a subset. |
| `StructureAttribute` | 4 | QC170-197 | BD493-701 (structure of matter); QA440-699 via `ShapeAttribute` | partial | partial | Lc | Was `none`. |
| `Substance` | 4 | QD (Chemistry) | QE351-399.2 (Mineralogy); TA401-492 (Materials); RS (materia medica) | exact | mapped | M | Homogeneous stuff - chemistry, mineralogy, materials science. |
| `Substituting` | 4 | — (pointer) HF (pointer only); false friend for economic substitution | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `SurfaceChange` | 4 | TT300-382 (Handicrafts: painting, finishing; range unverified) | TS (surface finishing); TA401-492 (corrosion, coatings) | partial | partial | M | Altering surface properties (child Coloring). MILO Painting [MILO] is a subclass of Coloring - i.e. painting a wall, NOT the art of ND. |
| `Swimming` | 4 | GV557-1198.995 (Sports: swimming; GV836.35-837.9 unverified) | QP | exact | mapped | M | Swimming as sport/physical activity. |
| `SymbolicString` | 4 | QA75.5-76.95 (computer science: strings) | P99-99.4; Z | partial | partial | M | Alphanumeric sequences - formal languages/strings in CS. |
| `SymmetricRelation` | 4 | — (pointer) BC; QA150-272.5 | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `TernaryFunction` | 4 | — (pointer) QA150-272.5 | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `TernaryPredicate` | 4 | — (pointer) BC | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Text` | 4 | Z4-115.5 (Books. Writing. Paleography) | P302-302.87 (Discourse analysis); PN; PZ; A | partial | partial | M | SUMO Text = inscribed linguistic artifact. Every literature and nearly every book is a Text instance, but LCC classes those by CONTENT. Only Z/P302 study text as such. |
| `TimeZone` | 4 | QB (Astronomy: time; QB209-224 unverified) | CE (Technical chronology) | exact | mapped | M | Time zones - practical astronomy/time determination. |
| `Transaction` | 4 | HF (Commerce) | HG; HD4801-8943 (labor) | broader | mapped | Lc | SUMO's own secondaries show the span. |
| `TransitiveRelation` | 4 | — (pointer) BC; QA150-272.5 | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `Transitway` | 4 | TE (Highway engineering. Roads and pavements) | TF; HE; VK; TA1001-1280 | partial | partial | M | Paths for travel - roads, railways, waterways, air routes. |
| `Translating` | 4 | P306-310 (Translating and interpreting) | - | exact | mapped | M | Translation. |
| `Translocation` | 4 | HE (Transportation and communications) | JV (migration); QC120-168.85 | partial | partial | Lc | `Immigrating` [MILO] ⊂ `Translocation`. |
| `TrichotomizingRelation` | 4 | — (pointer) QA150-272.5 (order); see defect D1 | — | none | granularity | A+Lc | Too abstract to shelve: no LCC unit is about one such class. No fault; excluded from coverage. |
| `TruthValue` | 4 | BC (Logic: truth; many-valued logic) | BD143-237 (theories of truth) | exact | mapped | M | True/False - logic. |
| `UnaryFunction` | 4 | QA299.6-433 (Analysis: functions) | QA | narrower | mapped | M | One-argument functions. |
| `UnitOfMeasureMultiplier` | 4 | QC81-114 (Weights and measures: metric prefixes) | - | exact | mapped | M | kilo-, milli- etc.; metrology. |
| `VisualContentBearingPhysical` | 4 | N (Visual arts) | NC; TR (Photography); P99.5-99.6; G (maps) | partial | partial | Lc | Maps are visual content bearers (same reason as `Icon`). |
| `WearableItem` | 4 | GT500-2370 (Clothing and fashion) | TT (Handicrafts: clothing; TT490-695 unverified); TS1300-1865 | exact | mapped | M | Clothing and accessories. |
| `WeatherProcess` | 4 | QC851-999 (Meteorology. Climatology) | TA197-198 (Engineering meteorology) | exact | mapped | M | Weather - meteorology. |

