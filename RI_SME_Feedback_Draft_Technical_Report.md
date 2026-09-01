Hi Mohamed/Allen - 

I'm going to be traveling for the next few days - back on Sunday evening, and so I wanted to give you a progress report and provide some feedback on the technical report - as well as leave you with a couple of to-dos and few questions.

### 1. Essential Parameters Workbook

 I am attaching an updated version of your version 2 table. Columns A - E are verbatim from your table, F is changed to reflect the true current schema location and related dictionary file, if relevent. There is also a column with the full URL to the dictionary that holds values for the specified parameters. Please click on those links to review what I've currently added to those dictionaries, and provide any necessary corrections/additions. The New element? column is changed from your original to reflect current status - existing (no changes needed), Built - Draft -draft schema/ditionary additions, Gap - not yet modeled, N/A - by design = not specifically modeled in the schema but the concept is covered - see DIGGS schema location column for the explanation as to why it isn't modeled (eg. implicit in an object structure or an easily derived value). The Definition column comes from you, whereas the last three columns are my development notes that should not go into the report. One other change from your table - a number of your parameter rows had several parameters conflated for the purpose of mapping to the schema. The revised table deconflates the parameters so that the specific DIGGS element can be attributed to it. The Orig. Row column indicates which row in your V2 workbook the parameter came from.

This is the data that should go into the tables in Chapter 4. I'll send another update once tha gaps are closed.

### 2. Report feedback

1. **The containment hierarchy in §4.1–§4.3 no longer matches the schema.** The report states that "the columns and the geosynthetics sit within a `LoadTransferPlatform`, and
the platforms sit within an `RIFoundationSystem`," and that the LTP "is itself the container for the
columns of its zone." That's no longer how it works. The system was redesigned as a **group** — its members (columns,
platforms, the treated area) each cite the group by reference (`samplingFeatureGroupRef`); nothing
contains anything. `LoadTransferPlatform` is a plain sampling feature with no children as are RICOlumn and RITreatedArea. Spatial "containment" is implied by position - The LoadTransferPlatform is contained within the treatment area as its featureExtent falls within the treatement area. An RIColumn feature is associated with the LTP that spatially contains it (a point-in-polygon association). These are all implicit in the geometries of the features - no explicit containment elements occur in the schema. I have attached a UML diagram of these features that you can use to substitute for the ones you have in Chapter 4. It's in an SVG vector format so you can edit it down if you don't want to include the property information.




2. Element names throughout Chapter 4 are out of date. The report cites the pre-extension names in several places. Current names:

| Report's name | Current name |
|---|---|
| `RigidInclusion` | `RIColumn` |
| `RIFoundationSystem` | `RigidInclusionSystem` (now a group, not a feature) |
| — | `RITreatedArea` (new — the planar feature that actually carries the support area) |
| `RISystemDesign` | `RITreatedAreaDesign` |
| `RISystemBasis` | `RIProgramBasis` |
| `RIConstructionMethod` | same, with real time data, etc. in `RIColumnConstruction` |
| `RIDesignSpec` / `ColumnSpec` / `RIPerformanceSpec` | `DesignConformanceCriterion`, `PerformanceCriterion` (built as a criterion family, not per-object spec types) |

3. The "98 existing / 15 need extension / 122 new feature" counts are stale. §2.6, §4.4 and Table 4-5 read as forward-looking, but they describe the schema as it stood *before this extension existed. Best to state that of the 295 essential parameters defined, 207 required either new objects, extensions of existing schama objects, or a dictionary definition, 75 are accmmodated by the v. 3.0.0 schema without changes, and 13 parameters are implicitly covered in the schema design, but not assigned to an explicit schema element or dictionary definition. (these are the NA-by design parameters). With regard to the schema elements, best I can estimate right now, accommodating the new parameters required the addition of 64 global elements, and 87 complex types. Of the 64 new elements, 43 are generic/core elements that will also support program design and specification development for other domains, such as exploration or other construction activities, so this project will make other construction programs easier to build in the future.

4. `diggs:MonitorResult` was removed from the schema — my fault, not yours.  Table 4-3 (Group C) lists it as an existing feature ("Existing: Monitor + MonitorResult"). It no longer exists in the current schema - it was an unused orphan replaced by the TemporalResult object — and it was removed during 3.1 development. The report should cite the replacement path — **`Monitor` → `outcome` → `diggs:TemporalResult`**. Everything else checks out: of the 62 existing-feature names Table 4-3 promises, this is the only one that does not resolve, and the other 61 are correct.

5. §5.5 overstates the septic-tank case-study data. It states the septic tank has "their own CMC grid and platform thickness." The grid is real
(Table 5-8: 10.0 m spacing, 2.0 × 2.0 m). The platform thickness is not — Table 5-9 lists the same six
structures as the source parameter workbook and omits it for the septic tank. (I ended up
substituting the Outdoor Equipment structure's platform levels for this element in the test instance, on the basis that it's designed to carry a comparable load. If you have source data that actually specifies LTP parameters for the septic tank, please let me know.

6. `verticallThicknessOfUnit` — typo, please don't propagate it. The schema itself shipped this element name with a doubled "l" in 3.0.0. I've since added the correctly-spelled `verticalThicknessOfUnit` alongside it (the old spelling still validates, deprecated in favor of the new one) — but the report should cite the corrected spelling **`verticalThicknessOfUnit`**, rather than propagate the original typo.

7.  `ORTD` and `DDP` are undefined. Table 3-11 lists the inclusion types each state DOT permits by acronym: CMC, GCC, CSC, APGC, APGD, ORTD, DDP, GI, VCC, CFA, DDC. Every one of these is expanded somewhere else in the report *except*
**`ORTD`** and **`DDP`** — I could confirm all the others (CMC = Controlled Modulus Column;
RI = Rigid Inclusion, also marketed as GI; GCC = GeoConcrete Column; CSC = Controlled Stiffness
Column; APGC = Augered Pressure Grout Column; VCC = vibro concrete column; CFA = continuous-flight
auger; ACIP = auger cast-in-place; DDC = drilled displacement column), but neither `ORTD` nor `DDP`
has a definition anywhere in the text.`DDP` is plausibly "drilled displacement pile" given its context at Table 3-11 ("drilled-displacement
piles, CMC, DDP, VCC or CFA") — but that's a guess, and the fact that the sentence lists CMC and DDP
side by side suggests they're *not* the same thing. `ORTD` has no contextual hint at all. I've deliberately left both out of the trade-name vocabulary rather than guess — could you confirm both definitions (and ideally where each one is used) so I can add them correctly?

8. The statement in §3.5.5: "Where the working platform built to carry the installation plant survives in place, it commonly becomes the lowest layer of the load-transfer platform, so that its material, thickness and level pass directly into the platform record (Section 3.3) - also repeated in Section 3.3 - seems wrong to me. The fill material used to construct the working platform (if present) lies below the column caps and therefore cannot serve to distribute loads to  he tops of the columns. Furthermore, the thickness of the LTP is measured from the WP elevation, which is above the fill. As we discussed, the fill used to create the working platform instead would be part of the ground model, at least based on its physical location. The current schema places the WorkingPlatform object (including any fill below it) into RITreatmentArea, and includes a property for materialtype and fill thickness (if present), along with the mandatory elevation property, since the primary purpose of the WP is to serve as the datum for column plaement. The description in the text does not model the schema design so either it should change or the WorkingPlatform needs to be put into the LTP object. Let me know if that's what you want.

Regarding construction activity info for LTP:

Based on your recommendations of where to review the report regarding construction of the LTP, I don't think there's enough construction related information to warrant making a separate construction activty object for LTP like there is for RIColumn, where there is realtime information recorded as part of their consruction. Instead, I've added a lifts property to the LTP as part of the as-built - it records each lift placement (material, thickness and location, along with the geosynthetics that I had already included. The lift object is mandatory - an LTP must have at least one lift object that defines its construction. I gather that there may be tests made either in situ or in the lab on the aggregate used for constructing the lift. Those can be handled by our standard Test object, referenced to the LTP if in-situ, or to the aggregat material sample, with an insitu test location specified in 3D within the LTP, even if internal to the platform. Samples of the aggregate used for the lift can be referenced by the lift which allows test results on the sample to be cross-referenced to the lift. If there is anything else that we need to record regarding LTP construction, let me know. 

Regardomg geosynthetic construction:

As with LTP, there is no real justification to include a construction activity object. Multiple geosynthetic layers, describing their extent and location within the LTP is held in the as-built record, as is overlap distance and direction per layer. If overlap distance or direction can change within a layer, the current schema structure cannot accommodate this. The report is not specific about what overlap is recorded (end-to-end, sidelap?) or what the direction values should be. Right now, there is currently only one parameter for overlap that I assume is universally understood by practicioners (whetehr end-to-end or side overlap) as a length measure; direction is a codelist with a dictionary. Please check the dictionary values and let me know if these are the values that are recorded or are we talking compass directions?.

Regarding my question about verticality:

The report defines verticality both as tip deviation and inclination (tables use inclination). The report also suggests there are post-construction surveys of column position and verticality alhough I don't know how that's done post construction. If inclination is measured during construction, that should be reported in a depth vs inclination (or deviation) with the "final" inclination being what is meastured at total depth. The current schema for RIColumn has meetsVerticality as a boolean verdict. I think instead we should report the bottom hole verticality in RIColumn as an inclination (angle) - assuming its determined somehow, and leave the verdict to the post-installation comparison of the as-built inclination to the design criterion for verticality. This way, we have as-built data to directly compare with design. Does this seem ok to you? Assuming so, I will change meetsVerticality to an inclination property (PlaneAngleMeasure). Regarding that - is inclination measured from vertical (eg. 0 deg = vertical, or from horizontal, like a plunge angle 90 deg = vertical). If the measured inclination is actually deviation, as one line in the report suggested might be the case in some instances, we could add a property for that, although the real test of verticality isn't just the deviation - you need to take into account the hole depth as well, so devialion/holedepth could be another way of expressing verticality. Anyway, further guidance on how this value is actually reported would be appreciated.

Still left on my plate - 

1. Closing up the 20 or so gaps. Most of these are additional test procedure objects for the post-installation phase. I'll have AI do some research on these tests and produce the objects from what it is able to glean from the relevant standards, but this will require your review. These should go pretty fast - I'll should have those done by Monday or Tuesday next week If, by early next week, you can provide feedback on the verticality issue, your review of the dictionary items (from the links in the excel workbook), along with any other feedback, that would be good.

2. Finish building the reference xml instance using the Jazeera dataset. The as-built and pre-installation parts are in, but I need to test a number of design and verification scenarios to make sure that the design, specification and verification elements work well. I'll use what we have for the Jazeera data first, although that isn't complete, so I'll need to have AI generate a number of virtual instances to supplement the Jazeera data to exercise the full schema to make sure we have everything covered. This will take some days to complete and will complete the schema design. At that point, I will push to schema-dev on Github (the public development schema).

3. With the schema and dictionaries complete, I'll be in a position to write up the schema design for the report, whick will be the next task - probably several days to complete

3. Next, I'll need to update the file inspector - the schema changes have broken its ability to display the as-builts. That will be quick to fix, but the trick will be trying to figure out how to visualize the design components within the confines of the viewer - that might take some time.

So, probably two weeks to wrap up everything except the file inspector visualization of design/spec/verification which might take a little longer.

Release 3.1 will be the formal release of the R-I schema. 3.1 has some cleanup to do around dictionaries, internal documentaion and handling of deprecated elements, plus inclusion of the lab testing program, which is complete but not exercised at all. Hopefully we can do the formal 3.1 release in October sometime along with a fully fleshed out file inspector viewer.



I don't think its worth meeting on Monday. Best to wait until I'm into or have completed step 2 above - at that point I'll have something firm to show and if there are issues that come up when testing the instances we can address then. How about Thursday next week?

Best,

Dan