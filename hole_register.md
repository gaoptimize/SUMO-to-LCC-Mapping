# LCC ⇄ SUMO: hole register

Companion to `merged_mapping.md`. Four kinds of entry, so that no hole is blamed on the wrong side.

## 1. No-fault: granularity and form mismatches (mirror images)

The two advocates converged on this framing in round 2. SUMO has formal machinery that no shelf is about; LCC has shelves defined by form, audience or notation that no ontology should model. Neither counts against the other; both are excluded from coverage.

### 1a. SUMO side: too abstract to shelve (27 classes)

| SUMO class | d | Where a book on it would go |
|---|---|---|
| `ReflexiveRelation` | 4 | BC; QA150-272.5 |
| `IrreflexiveRelation` | 4 | BC; QA150-272.5 |
| `SymmetricRelation` | 4 | BC; QA150-272.5 |
| `AntisymmetricRelation` | 4 | QA150-272.5 (order/lattices; QA171.5 via LCSH) |
| `TransitiveRelation` | 4 | BC; QA150-272.5 |
| `IntransitiveRelation` | 4 | BC; QA150-272.5 |
| `TrichotomizingRelation` | 4 | QA150-272.5 (order); see defect D1 |
| `TernaryRelation` | 3 | BC (polyadic logic) |
| `QuaternaryRelation` | 3 | BC |
| `QuintaryRelation` | 3 | BC |
| `TernaryPredicate` | 4 | BC |
| `QuaternaryPredicate` | 4 | BC |
| `QuintaryPredicate` | 4 | BC |
| `TernaryFunction` | 4 | QA150-272.5 |
| `QuaternaryFunction` | 4 | QA150-272.5 |
| `VariableArityRelation` | 3 | BC; QA75.5-76.95 |
| `TotalValuedRelation` | 3 | QA (total functions; range unverified) |
| `PartialValuedRelation` | 3 | QA (partial recursive functions; range unverified) |
| `ClosedWorldPredicate` | 4 | QA75.5-76.95 |
| `NullSet` | 4 | QA (set theory; range unverified); BC |
| `NonNullSet` | 4 | QA; BC |
| `UniqueList` | 3 | QA75.5-76.95 (data structures) |
| `DualObjectProcess` | 3 | P (semantics/valency; unverified); BD |
| `SaturationAttribute` | 4 | QC851-999 (humidity) |
| `Poking` | 4 | domain homes via children (TJ/TT; unverified) |
| `Detaching` | 4 | TJ / TS (unverified) |
| `Substituting` | 4 | HF (pointer only); false friend for economic substitution |

### 1b. LCC side: form, audience and notational units

| LCC | Why no ontology should model it |
|---|---|
| A, AC, AI, AY | Polygraphic: defined by having no single subject. (AI, AY also have a small SUMO gap G9.) |
| J, LH, LT | Defined by document type (government papers, college periodicals, textbooks). |
| PZ | Defined by audience (juvenile literature). Genre classes are a separate SUMO gap (G4). |
| PJ, PL, PM (grouping only) | Geographic groupings of languages, not genetic families. Expressible as a `UnionFn`; not a kind. |
| CD, UG, HQ, HX, JV, Z (bundling only) | Literary-warrant co-locations; mapped as several Subjects, coded `partial`. |
| All (structure) | LCC notation, tables, Cutters, literary warrant, parenthesized ranges. Not SUMO `subclass` (rule R6). |

## 2. LCC gaps: none

The SUMO advocate initially conceded small LCC gaps (general action theory; mereotopology / holes). The LCC advocate rebutted with outline evidence: action theory is shelved at BF608-635 and BF309-499; real holes (`Cave`, `Crater`) are shelved at GB561-649; `Keeping` has AM, HF5484-5495 and HV8301-9920.7. **Ruling:** accepted (evidence-based). What has no shelf is a single motor action such as poking, which is granularity (§1a), not a gap. This is the expected result: an upper ontology's classes are general enough that some LCC shelf exists at coarse granularity.

## 3. SUMO gaps (an extension could fill them)

| ID | Kind | Gap | Proposed fix | Agreed by | LCC units affected |
|---|---|---|---|---|---|
| G1 | SUMO gap | Religion as a tradition (doctrine, scripture, practice). There is no `Religion`, `Scripture` or `Mythology` class anywhere in the repo; religions are instances of `BeliefGroup` (a GroupOfPeople). `ChristianBible` is a subclass of `Book` (physical copies). | Add a doctrine/tradition class under `Proposition` (parallel to MILO `Music`, `Policy`, `Contract`), plus a scripture class under `Text` distinct from `Book`. | both (LCC H8, SUMO §3) | BL, BM, BP, BQ, BR, BS, KB, KBM |
| G2 | SUMO gap | No abstract content class for literary works. `FictionalText`, `NarrativeText`, `Novel` are all bearers (⊂ `Text`); only `Music` and `LyricalContent` [MILO] are content-side classes for created works. | Add a literary-work content class under `Proposition`. | LCC critique A1; not answered by SUMO | PN, PQ, PR, PS, PT |
| G3 | SUMO gap | Auxiliary sciences of history. Disciplines `Numismatics`, `Heraldry`, `Genealogy`, `Epigraphy`, `Diplomatics` are absent; so are the objects `Seal`, `Inscription`, `Archive`, `CoatOfArms`, and "Civilization". | Add MILO FieldOfStudy subclasses with `(subField X History)`; add the object classes. | both (LCC H9, SUMO §3) | C, CB, CD, CE, CJ, CN, CR, CS |
| G4 | SUMO gap | Literary genres. `Poem`, `Poetry`, `Drama`, `Epic`, `Myth` are absent; only `DramaticPlay` [MILO] ⊂ `FictionalText` exists. | Add under `FictionalText` / `NarrativeText` in MILO. | both (LCC H5, SUMO §3) | PN, PZ |
| G5 | SUMO gap (low priority) | Fringe and alternative knowledge systems: no `Astrology`, `Occult`, `Homeopathy`, alternative-medicine classes. | Add as FieldOfStudy subclasses in MILO; SUMO models disciplines regardless of validity (`MedicalField` exists). | both (LCC H12, SUMO §3) | BF, RV, RX, RZ |
| G6 | SUMO gap (instance level) | Historical and cultural regions with no instance: `RomanEmpire`, `AncientRome`, `AncientGreece`, `LatinAmerica`, `CentralAmerica`, `Caribbean`, `MiddleEast`, `Scandinavia`, `Balkans`. | Add as `GeopoliticalArea` / `GeographicArea` instances, with `holdsDuring` for dead polities. Below the top levels, so it does not count against depth-4 coverage. | both (LCC H3, SUMO §3) | DE, DF, DG, DL, DR, F |
| G7 | SUMO gap (instance level) | Peoples as an organizing axis: `EthnicGroup` exists but many peoples LCC organizes by (DX, E51-99, KQ2010-9000) have no instance. | Add `EthnicGroup` instances. | both (LCC H4, SUMO §3) | DX, E |
| G8 | SUMO gap | No musicology discipline: `Music` [MILO] is a `Proposition` (the work), not a FieldOfStudy. | Add `Musicology` as a FieldOfStudy subclass. | coordinator (from SUMO critique row ML) | ML, MT |
| G9 | SUMO gap (low priority) | Reference forms: no `Encyclopedia`, bibliographic `Index`, `Yearbook`, `Almanac`, `Directory`, `Textbook` classes. | Add under `FactualText` → `ReferenceBook` [MILO]. | both (LCC H1, SUMO §3) | AE, AI, AY |

## 4. SUMO defects to report upstream

Found while mapping; each is checked against commit `2b55bb5`.

| ID | Class | Defect | Raised by |
|---|---|---|---|
| D1 | `TrichotomizingRelation` | Its documentation says all ordered pairs of distinct individuals are in the relation; the axiom (Merge.kif ~l.3038) requires exactly one of R(x,y), x=y, R(y,x). Documentation contradicts axiom. | LCC critique §3 |
| D2 | `Bahai` | Typed `instance ReligiousAttribute`, while `Judaism`, `Islam`, `Buddhism`, `Christianity` are `instance BeliefGroup` [People]. | both |
| D3 | `Engineering` [MILO] | Declared `(subclass Engineering Science)`. SUMO therefore puts technology inside science; it cannot separate LCC Q from T at any level. | LCC critique A9; SUMO conceded the Q/T weakness |
| D4 | `CollectionOfProcesses` | No subclasses, garbled documentation ("a Collectionsthat has Processes as members"), placed in `Physical` beside `Process` with no stated relation to `subProcess`. | LCC critique §3 |
| D5 | `InheritableRelation`, `RelationExtendedToQuantities` | Ontology-engineering meta-classes (inference and axiom devices), not concepts of any discipline. They belong in a meta-layer, not the domain tree. | LCC critique §3 |
| D6 | `SingleAgentProcess` (weak) | Its only Merge child, `Sensing`, now allows a non-biological sensor as agent, which sits awkwardly with "exactly one agent". Typing machinery with no domain content. | LCC critique §3 |
| D7 | `Communism` [Economy] | `subclass BeliefGroup`: the same parent reused for a political ideology and for religions. | SUMO critique point 4 |

## 5. Resolved by pattern (not holes)

| Was listed as | Resolution |
|---|---|
| History of a place (D, E, F) | Discipline `History` + Subject `Process`/`PoliticalProcess` + place facet via `eventLocated`. |
| Peoples as an axis (pattern) | Discipline + people facet `EthnicGroup`; only missing instances remain (G7). |
| Period facets | `TimeInterval` linked by `holdsDuring`; a facet, not a class. |
| Aspect distinctions (HE vs TF) | Discipline slot (rule R4). |
| Second-order subjects (AZ, C, LA, KBR) | `subField` + `refers` with a FieldOfStudy as Subject; "(General)" units take Subject = the field. |
| AE, AG, AN, AP | `ReferenceBook`, `Dictionary`, `Periodical`, `Newspaper` [MILO] fit. |
| PS nationality criterion | `authors` + `citizen` in Merge express it. |

## 6. False friends (rule R6)

| SUMO term | Actually means | Do not map to |
|---|---|---|
| `Medicine` [MILO] | a drug substance | class R (Medicine) |
| `Painting` [MILO] | the generic paint-applying process; covers `ArtPainting` and painting one's kitchen (too broad, not "non-art") | ND (Painting) |
| `Index` [FinancialOntology] | a financial performance measure | AI (Indexes) |
| `Music` [MILO] | a `Proposition` (the conceived work) | M (scores), ML (literature on music) |
| `Literature` [MILO] | "the study of FictionalText of special merit" (narrow) | PN–PZ as a whole |
| `Law` | an instance of `DeonticAttribute` | class K (Law) |
| `Creation` | any coming-into-being (⊂ `InternalChange`; child `Making`) | BT/BL doctrine of creation |
| `Sensing` | non-biological input reception (sensors, software) | BF psychology of the senses (→ `Perception`) |
| `Collection` | a physical aggregate | AC (collected works); QA set theory |
| `Substituting` | replacing one object with another | economic substitution (HB) |
| `Drawing` [MILO] | the act (`ContentDevelopment`, `SurfaceChange`) | NC drawn objects (→ `Sketch`) |
| `CurrencyCoin` [MILO] | a `Text` (via `FinancialInstrument` → `Certificate`) | CJ coins as objects |
| `Industry` [MILO] | a `CollectionOfObjects` | HD industries as activity |
| `Working` [MILO] | a `FinancialTransaction` | HD labor as activity |
| `Pollution` [Geography] | a `SocialInteraction` | TD/GE pollution as a physical process |
| `Teacher`, `Sailor`, `Pharmacist` [MILO] | instances of occupation attributes, not classes of people | LB, VD, RS people |
| `Mining` [naics] | an `IndustryAttribute` | TN mining as a process |
| `ArtificialLanguage` | includes `ComputerLanguage` | PM artificial languages (computer languages are QA76) |

