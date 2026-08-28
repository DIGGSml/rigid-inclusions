# RI Codelist & Property Dictionaries — SME Review List

All dictionaries below were created or modified in the `def` repository between **2026-08-16**
and **2026-08-17** in support of the DIGGS Rigid Inclusion (RI) schema work. Each is a standalone
XML file at the URL given; open the link to see the full list of coded values (for codelists) or
parameter definitions (for property dictionaries) and their descriptions.

This is a review list, not a final vocabulary. A few entries are flagged **[SME REVIEW]** below —
either because the schema's own documentation didn't name an explicit value set and a starting
list was proposed, or because a cited value (e.g. an ASIRI domain) needs confirmation against its
source standard. Everything else transcribes a value set the schema documentation already names
explicitly.

## Codelist dictionaries

One dictionary per coded property. "Parent object" is the DIGGS object the property lives on.

| Property name (CodeType element) | Parent object | Dictionary URL |
|---|---|---|
| `targetSFType` | `TargetSamplingFeature` | https://diggsml.org/def/codes/DIGGS/0.1/samplingFeatureTypes.xml |
| `archingModel` | `ArchingCoefficients`, `RISystemBasis` | https://diggsml.org/def/codes/DIGGS/0.1/archingModel.xml |
| `gridPattern` | `RIColumnDesign` | https://diggsml.org/def/codes/DIGGS/0.1/gridPattern.xml |
| `columnType` | `RIColumn`, `RIColumnSpecification`, `RISystemBasis` (as `riTechniqueType`) | https://diggsml.org/def/codes/DIGGS/0.1/columnType.xml |
| `measurementKind` | `TargetMeasurement` | https://diggsml.org/def/codes/DIGGS/0.1/measurementKind.xml |
| `statistic` | `PerformanceCriterion`, `DesignConformanceCriterion` | https://diggsml.org/def/codes/DIGGS/0.1/statistic.xml |
| `basis` / `differentialSettlementBasis` | `PerformanceCriterion`, `DesignConformanceCriterion`, `RISystemDesign` | https://diggsml.org/def/codes/DIGGS/0.1/basis.xml |
| `designProperty` | `DesignConformanceCriterion` | https://diggsml.org/def/codes/DIGGS/0.1/designProperty.xml |
| `consequenceClass` | `RISystemBasis` | https://diggsml.org/def/codes/DIGGS/0.1/consequenceClass.xml |
| `designMethod` | `RISystemBasis` | https://diggsml.org/def/codes/DIGGS/0.1/designMethod.xml |
| `safetyFormat` | `RISystemBasis` | https://diggsml.org/def/codes/DIGGS/0.1/safetyFormat.xml |
| `supportedStructureType` | `RISystemBasis` | https://diggsml.org/def/codes/DIGGS/0.1/supportedStructureType.xml |
| `appliesTo` | `DesignFactor` | https://diggsml.org/def/codes/DIGGS/0.1/appliesTo.xml |
| `terminationOutcome` | `RIConstructionActivity` | https://diggsml.org/def/codes/DIGGS/0.1/terminationOutcome.xml |
| `installationMethod` | `RIConstructionActivity` | https://diggsml.org/def/codes/DIGGS/0.1/installationMethod.xml |
| `actionType` | `DesignAction` | https://diggsml.org/def/codes/DIGGS/0.1/actionType.xml |
| `actionNature` | `DesignAction` | https://diggsml.org/def/codes/DIGGS/0.1/actionNature.xml |
| `representativeValue` | `DesignAction` | https://diggsml.org/def/codes/DIGGS/0.1/representativeValue.xml |
| `verificationType` | `DesignVerification` | https://diggsml.org/def/codes/DIGGS/0.1/verificationType.xml |
| `method` | `DesignVerification` | https://diggsml.org/def/codes/DIGGS/0.1/verificationMethod.xml |
| `outcome` | `DesignVerification` | https://diggsml.org/def/codes/DIGGS/0.1/verificationOutcome.xml |
| `relationType` | `LoadTransferRelation` | https://diggsml.org/def/codes/DIGGS/0.1/relationType.xml |
| `formulation` | `LoadTransferRelation` | https://diggsml.org/def/codes/DIGGS/0.1/loadTransferFormulation.xml |
| `limitState` | `GeoUnitDesignQuantity` | https://diggsml.org/def/codes/DIGGS/0.1/limitState.xml |
| `tensionSource` | `DesignTension` | https://diggsml.org/def/codes/DIGGS/0.1/tensionSource.xml |
| `polymerType` | `GeosyntheticLayerDesign` | https://diggsml.org/def/codes/DIGGS/0.1/polymerType.xml |
| `reinforcementType` (geosynthetic product form) | `GeosyntheticLayerDesign` | https://diggsml.org/def/codes/DIGGS/0.1/geosyntheticReinforcementType.xml |
| `direction` | `GeosyntheticLayerDesign` (design), `Geosynthetic` (as-built) | https://diggsml.org/def/codes/DIGGS/0.1/direction.xml |
| `reinforcementType` (steel cage arrangement) | `Reinforcement` | https://diggsml.org/def/codes/DIGGS/0.1/reinforcementType.xml |
| `reinforcementPurpose` **[SME REVIEW — see below]** | `Reinforcement` | https://diggsml.org/def/codes/DIGGS/0.1/reinforcementPurpose.xml |
| `barSize` | `Reinforcement` | https://diggsml.org/def/codes/DIGGS/0.1/barSize.xml |
| `steelGrade` | `Reinforcement` | https://diggsml.org/def/codes/DIGGS/0.1/steelGrade.xml |
| `loadEfficacyDefinition` | `RILTPDesign` | https://diggsml.org/def/codes/DIGGS/0.1/loadEfficacyDefinition.xml |
| `settlementEfficacyDefinition` **[SME REVIEW — see below]** | `RISystemDesign` | https://diggsml.org/def/codes/DIGGS/0.1/settlementEfficacyDefinition.xml |
| `settlementComponent` | `PredictedSettlement` | https://diggsml.org/def/codes/DIGGS/0.1/settlementComponent.xml |

**Note on the two `reinforcementType` dictionaries**: the element name `reinforcementType` is
reused on two unrelated objects with different vocabularies — the steel reinforcement cage
arrangement on `Reinforcement`, and the geosynthetic product form on `GeosyntheticLayerDesign`.
They are separate dictionaries with separate value sets; do not merge them.

**[SME REVIEW] `settlementEfficacyDefinition`**: unlike its sibling `loadEfficacyDefinition`, the
schema's own documentation does not name explicit competing definitions for settlement efficacy.
The two entries currently in the dictionary (`settlement_ratio`, `settlement_reduction_ratio`) are
standard ground-improvement definitions proposed as a starting point, not a citation. Please
confirm this is the right pair, or supply the definition(s) actually used in practice.

**[SME REVIEW] `reinforcementPurpose`**: three of the four entries (`tension_zone`, `bending`,
`seismic`) are stated directly in the schema documentation. The fourth, `asiri_domain_1`, cites
the ASIRI (French national research project) domain classification by name but was not built
against the ASIRI recommendations' own domain definitions directly. Please confirm the entry's
description accurately reflects ASIRI Domain 1, or correct it.

**Also worth a look**: `verificationMethod.xml` (`DesignVerification/method`) is scoped only to
the five methods the schema documentation names for the global-stability check (CWM, ESM, SRM,
PSM, numerical) — it does not yet cover methods for the other seven `verificationType` values
(buckling, shear, lateral spreading, seismic, liquefaction, punching, structural axial). Flag
during review if method vocabularies are needed for those too.

## Property dictionaries

Multi-parameter dictionaries (numeric/measured properties rather than coded values), created or
extended for RI support. Each links to the full parameter list.

| Property domain | Parent object | Dictionary URL |
|---|---|---|
| Arching-model-specific design coefficients (`arching_coefficient_marston`, `cap_stress_ratio`, `arching_efficiency_crown/cap/minimum`, `passive_earth_pressure_coefficient`, `critical_stress_ratio`, `lateral_earth_pressure_coefficient_ldc`, `punching_bearing_factor`, `active_earth_pressure_coefficient`) plus general RI column/LTP design ratios (`equivalent_diameter`, `column_axial_utilization`, `arching_height_ratio`, `diameter_spacing_ratio`, `spacing_aspect_ratio`, `stiffness_ratio`) | `ArchingCoefficients`, `RIColumnDesign`, `RILTPDesign` | https://diggsml.org/def/codes/DIGGS/0.1/ri_design_properties.xml |
| Partial and global safety/reduction factors (`partial_factor_permanent_unfavourable/favourable`, `partial_factor_variable_unfavourable`, `partial_factor_material_friction_angle/cohesion`, `partial_factor_resistance`, `global_factor_of_safety`, `reduction_factor_creep/installation_damage/weathering/chemical_degradation/joints_seams`, `material_partial_factor_geosynthetic`) | `DesignFactor` | https://diggsml.org/def/codes/DIGGS/0.1/design_factor_properties.xml |
| MWD/drilling process properties newly bound to the RI installation coverage record (`crowd_downward_thrust`, `crowd_pressure`, `net_crowd_pressure`) | `RIInstallationRecord` (via `RIConstructionActivity`) | https://diggsml.org/def/codes/DIGGS/0.1/mwd_properties.xml |
| Grouting/injection process properties newly bound to the RI installation coverage record (`grout_volume`, `stroke_count`, `drilling_speed`, `rotation_speed`, `torque`, `thrust`, `crowd_pressure`), plus one newly added property (`volume_overconsumption`) | `RIInstallationRecord` (via `RIConstructionActivity`) | https://diggsml.org/def/codes/DIGGS/0.1/gr_inj_properties.xml |
| Monitoring sensor and construction equipment classes (`piezometer`, `inclinometer`, `extensometer`, `settlement_cell`, `earth_pressure_cell`, `strain_gauge`, `load_cell`, `tiltmeter`, `crackmeter`, `thermistor`, `accelerometer`, `settlement_plate`, `survey_monument`, `data_logger`, `total_station` — `Sensor`; `excavator`, `dozer`, `vibratory_roller`, `plate_compactor`, `crane`, `concrete_batch_plant`, `load_test_reaction_frame`, `hydraulic_jack` — `Equipment`) | `Sensor`, `Equipment` | https://diggsml.org/def/codes/DIGGS/0.1/equipmentClass.xml |

The MWD and grouting-injection rows are pre-existing dictionaries (property lists used elsewhere
in DIGGS) — only the properties named above were newly tied to the RI installation record or
newly added; the rest of each file's content is general DIGGS infrastructure, not RI-specific,
and isn't part of this review. `equipmentClass.xml` is also pre-existing (authored before
2026-08-16) and its content is unchanged in this window — it's included here because it's part of
the RI program's working vocabulary and worth the same SME pass, even though the only thing that
happened to it in this window was picking up a companion `.xlsx` workbook.

**`ri_properties.xml`, listed in this table as of the original review window, was retired entirely
on 2026-08-19** (tasks D2, EC1, TF1, TF2): all four of its entries were promoted to typed schema
elements (`plannedEquipment`, `elementClass`, `testedFraction`, `testLoadPercentDesignLoad`, and
the `testingDensityPerLength`/`PerArea`/`PerElement` choice) once each was found to have either a
fixed set of shapes or an already-existing DIGGS measure type to carry it, leaving no dictionary
value list to review. Removed from the table above for that reason.
workbooks (S3), not a content edit.

## What's not on this list

- Nothing in `dictionary-validation.xsl` (the `validation` repo) yet checks that an instance's
  `codeSpace` actually resolves against these dictionaries for plain `gml:CodeType`/
  `parameterName` consumers (tracked separately as task **X2**) — these dictionaries are
  structurally valid XML today, not yet runtime-enforced.
