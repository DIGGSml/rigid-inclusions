# Feedback on the Draft Technical Report — Rigid Inclusion DIGGS Extension

This is a review of the draft technical report (`RI-DIGGS_Technical_Report_Compiled.pdf`) against
the schema as actually built. Chapter 4 already flags five places "To be revised by Dan" — this
covers those, plus two smaller items. Seven items total; none blocks the report, all are worth
fixing before it's finalized or circulated further.

## 1. The containment hierarchy in §4.1–§4.3 no longer matches the schema

The report states that "the columns and the geosynthetics sit within a `LoadTransferPlatform`, and
the platforms sit within an `RIFoundationSystem`," and that the LTP "is itself the container for the
columns of its zone."

That's no longer how it works. The system was redesigned as a **group** — its members (columns,
platforms, the treated area) each cite the group by reference (`samplingFeatureGroupRef`); nothing
contains anything. `LoadTransferPlatform` is a plain sampling feature with no children.

**Fix:** rewrite §4.1–§4.3 to describe association as positional (via group membership), not
containment. Happy to supply the current class relationships if useful.

## 2. Element names throughout Chapter 4 are out of date

The report cites the pre-extension names in several places. Current names:

| Report's name | Current name |
|---|---|
| `RigidInclusion` | `RIColumn` |
| `RIFoundationSystem` | `RigidInclusionSystem` (now a group, not a feature) |
| — | `RITreatedArea` (new — the planar feature that actually carries the support area) |
| `RISystemDesign` | `RITreatedAreaDesign` |
| `RISystemBasis` | `RIProgramBasis` |
| `RIConstructionMethod` | `RIConstructionActivity` |
| `RIDesignSpec` / `ColumnSpec` / `RIPerformanceSpec` | `DesignConformanceCriterion`, `PerformanceCriterion` (built as a criterion family, not per-object spec types) |

## 3. The "98 existing / 15 need extension / 122 new feature" counts are stale

§2.6, §4.4 and Table 4-5 read as forward-looking, but they describe the schema as it stood *before*
this extension existed. The great majority of the 122 "requires new DIGGS feature" items are now
built. Worth a pass to re-tally, or at minimum a note that the counts predate the build.

## 4. `diggs:MonitorResult` was removed from the schema — our fault, not yours

Table 4-3 (Group C) lists it as an existing feature ("Existing: Monitor + MonitorResult"). It no
longer exists in the current schema, so the citation needs updating — **but the reason is on our
side and worth explaining, because it affects more than this one row.**

`MonitorResult` **was a real element in the DIGGS 3.0.0 release**, which is the version the report
was written against. It was an orphan there — already superseded by `TemporalResult` — and it was
removed during 3.1 development ("Removed orphaned MonitorResult and MonitorResultType (replaced by
TemporalResult in 3.0)"). So the report cited something that genuinely existed when it was written.

**The removal was not recorded where our own convention says it should be.** DIGGS keeps a
`deprecated/DeletedElements.xsd` file precisely so that removed elements leave a discoverable trail.
Of the 13 elements removed since 3.0.0, **11 are recorded there and `MonitorResult` is not** — so
anyone checking a 3.0.0-era citation against the current schema finds the name simply absent, with
no pointer to what replaced it. That has now caused stale `MonitorResult` references to go
undetected in four other places in *our own* materials, not just in your report.

**Two actions, both ours:** we will record the removal in `DeletedElements.xsd`, and the report
should cite the replacement path — **`Monitor` → `outcome` → `diggs:TemporalResult`**.

Everything else checks out: of the 62 existing-feature names Table 4-3 promises, this is the only one
that does not resolve, and the other 61 are correct.

## 5. §5.5 overstates the septic-tank case-study data

It states the septic tank has "their own CMC grid and platform thickness." The grid is real
(Table 5-8: 10.0 m spacing, 2.0 × 2.0 m). The platform thickness is not — Table 5-9 lists the same six
structures as the source parameter workbook and omits it for the septic tank. (We ended up
substituting the Outdoor Equipment structure's platform levels for this element in our own build
instance, on the basis that it's designed to carry a comparable load — flagging so the report doesn't
present that substitution as sourced data.)

## 6. `verticallThicknessOfUnit` — typo, please don't propagate it

The schema itself shipped this element name with a doubled "l" in 3.0.0. We've since added the
correctly-spelled `verticalThicknessOfUnit` alongside it (the old spelling still validates, deprecated
in favor of the new one) — but the report should cite the corrected spelling,
**`verticalThicknessOfUnit`**, rather than propagate the original typo.

## 7. Request: expansions for `ORTD` and `DDP`

Table 3-11 lists the inclusion types each state DOT permits by acronym: CMC, GCC, CSC, APGC, APGD,
ORTD, DDP, GI, VCC, CFA, DDC. Every one of these is expanded somewhere else in the report *except*
**`ORTD`** and **`DDP`** — we could confirm all the others (CMC = Controlled Modulus Column;
RI = Rigid Inclusion, also marketed as GI; GCC = GeoConcrete Column; CSC = Controlled Stiffness
Column; APGC = Augered Pressure Grout Column; VCC = vibro concrete column; CFA = continuous-flight
auger; ACIP = auger cast-in-place; DDC = drilled displacement column), but neither `ORTD` nor `DDP`
has a definition anywhere in the text.

`DDP` is plausibly "drilled displacement pile" given its context at Table 3-11 ("drilled-displacement
piles, CMC, DDP, VCC or CFA") — but that's a guess, and the fact that the sentence lists CMC and DDP
side by side suggests they're *not* the same thing. `ORTD` has no contextual hint at all.

We've deliberately left both out of our own trade-name vocabulary rather than guess — could you
confirm both expansions (and ideally where each one is used) so we can add them correctly?

---

*Compiled from a schema-level review dated 2026-08-26/27. Full technical detail behind each item is
available on request.*
