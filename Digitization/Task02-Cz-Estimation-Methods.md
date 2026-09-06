# Digital Cz estimation: proposed methods

**Task #02** (issue #4) · Digitization stage · fNIRS-emotion-VandyBH26

**Scope.** This document covers Task #02: estimating each participant's digital Cz. Sections 2 to 7 are the proposal itself; §1 gives only the background needed to judge the accuracy requirement in §2. One part reaches beyond the task as assigned and is marked where it appears: applying Method 2 to other institutions' data (§6). This is the design step; no code yet.

---

## 1. Why this task exists

### Why landmark accuracy carries the anatomy

fNIRS is the modality this study can use. Cochlear implants make fMRI impractical for the hearing-loss group, since the implant throws a large susceptibility artifact over the temporal bone, directly above auditory cortex, and scanner noise would contaminate an auditory paradigm on top of that. EEG cannot separate auditory from prefrontal contributions well enough for this hypothesis.

That choice comes at one cost which sets up this whole task: fNIRS produces no anatomical image of its own.

An fMRI study sees the brain it is measuring. An fNIRS study does not. It records from optodes on the scalp, and the question of which cortical region a given channel sampled has to be answered from outside the data, by registering the cap to the head through external landmarks.

Landmark accuracy is what gives fNIRS signals their anatomical meaning, and Cz is the landmark the rest of that registration is built on.

### Why Cz specifically

Cz anchors the montage.

In the 10-20 / 10-10 convention every scalp position is defined by proportional distances along the Nz–Iz and Lpa–Rpa geodesics, which intersect at Cz. An error in Cz is not a local error at the vertex. It displaces the assumed position of the whole optode array.

Cz also fixes the head's vertical dimension, and nothing else in the landmark set does. Nz, Iz, Lpa and Rpa lie approximately on one plane around the circumference of the head. Four roughly coplanar points describe that circumference but say almost nothing about how tall the head is above it. Cz is the fifth point and the only one above that plane.

It sits on both primary reference curves as well. The routine that generates the optode array builds those curves through Cz: the sagittal curve runs Nz → Cz → Iz, the coronal curve runs Lpa → Cz → Rpa, and every remaining position is interpolated proportionally from the two. A real head is not a sphere, so a curve fitted from Nz straight to Iz without the vertex waypoint misses the true vertex. Positions across the upper part of the array, which is most of it in this montage, inherit that discrepancy in proportion to their distance from the circumference.

The error then propagates along a chain: landmarks → optode positions → channel positions → anatomical attribution. Analysis happens on channels, not individual optodes, and each channel's position comes from the source–detector pair that forms it, so every channel inherits error from two projected optodes. With 50 optodes yielding 100 channels here (84 long channels at 3 cm separation, 16 short at 1 cm), a single Cz error displaces every unit the study analyses, and displaces them in a correlated way that averaging cannot reduce.

The burden falls on the 84 long channels, since those carry the signal attributed to cortical regions. The 16 short channels sample superficial tissue and act as regressors for systemic signal, so their anatomical attribution matters far less. Read the accuracy requirement in §2 as a requirement on the long channels.

Region attribution depends on all of this. An fNIRS channel samples a volume roughly between its source and detector, and this study states its conclusions in terms of auditory and prefrontal cortex. That attribution is only as good as the cap-to-head registration. Misplace Cz and channels are assigned to the wrong scalp coordinates, and downstream to the wrong anatomy.

The lateralization aim is the most exposed. Cz sits on the midline, so a laterally displaced Cz shifts the assumed midline and left- and right-hemisphere channels stop being symmetric about the true one. Any lateralized measure, including the lateralized index in Task #11, inherits that displacement as a systematic bias, not as random noise. This is the failure mode most likely to produce a wrong result that still looks plausible.

The error also reaches every downstream task. MNI projection (#04) uses the landmarks as anchors, atlas-based labelling (#05) inherits whatever MNI coordinates it is given, and channel–anatomy matching (#07) inherits both.

Inconsistency across participants costs statistical power. If Cz is estimated differently from one participant to the next, a given channel index corresponds to a slightly different cortical location in each person. Averaging then blurs the signal and inflates between-subject variance.

### Why the cap makes this hard

Cz is defined as the intersection of the Nz→Iz and Lpa→Rpa scalp geodesics, which is straightforward on a bare head. Two problems appear once the cap is fitted.

First, the cap does not conform identically to every head. After seating it by the standard 10% Nz–Iz measurement, the position printed on the cap as "Cz" no longer sits over the participant's true anatomical Cz, and the offset differs per participant according to scalp shape.

Second, the worn cap cannot be re-measured geometrically. The obvious fix, 3D-scanning the worn cap and re-deriving Cz, fails because the grommets make the cap surface irregular in exactly the region that would need scanning.

Of the four landmarks Cz depends on, three remain accessible after the cap is on:

| Landmark | Accessible post-cap? | How |
|---|---|---|
| Nz | Yes | Visible/palpable at the brow, below the cap edge |
| Lpa | Yes | Palpate the preauricular point during jaw movement |
| Rpa | Yes | Same as Lpa |
| **Iz** | **No** | Sits under the back of the cap, in the grommet-covered region |

Iz is the bottleneck. Both methods below exist because of it.

### Why a pre-cap measurement alone is not sufficient

The anatomical Cz does not move, so why not measure it before the cap goes on?

Because this task's deliverable is a *digital* Cz: a Cz expressed in the same digitized coordinate frame as the optode positions. Optodes are digitized with the cap on. A Cz measured in a separate pre-cap session sits in a different frame, and relating the two requires exactly the registration this task is meant to establish. The estimate has to be produced with the cap in place.

A pre-cap measurement is still valuable as independent ground truth for validation (§5.5). It just cannot substitute for the post-cap estimate.

### Definitions

- **C7 (7th cervical vertebra)** — the bony bump at the base of the neck, where the neck meets the upper back. A standard external anatomical reference: easy to palpate, stable relative to the skull at a fixed head posture, and, critically here, below the cap, so it stays accessible whether the cap is on or off.
- **Theoretical Cz** — the Cz predicted by the standard 10% Nz–Iz calculation, before any per-participant correction.
- **True Cz** — the participant's actual anatomical vertex, which the theoretical Cz approximates with unknown per-participant error.

---

## 2. Accuracy requirement

The validation plans below report error in millimetres. That number means nothing without a threshold, and the threshold should come from downstream impact, not from feel.

Set an acceptable error before validation runs, so that validation tests a criterion instead of describing an outcome. Two bounds frame the range:

- An error approaching the long-channel separation, 30 mm in this montage, is clearly unacceptable. It can shift a channel's attribution to a neighbouring region entirely.
- Sub-millimetre precision is unnecessary, far below the spatial resolution fNIRS itself offers.

Set the threshold inside that range by asking: how much Cz displacement would change which cortical region a long channel is assigned to, given our montage and our ROIs? For the lateralization aim, set the tolerance on lateral (left–right) displacement separately and more tightly than on anterior–posterior displacement, since lateral error biases the lateralized index directionally.

**Open item:** this threshold has not been set. It needs the montage geometry and should be agreed with the team before validation begins.

---

## 3. Existing approaches and why they fall short here

This section situates the proposal against standard practice. It needs completing with the team's knowledge of what equipment is available.

3D electromagnetic digitizers (Polhemus-type systems) are the established tool for optode co-registration and would give landmark positions directly. Where one is available and the landmark is physically reachable, it is the better option. It does not solve the problem here: Iz is under the cap and cannot be touched with a stylus once the cap is fitted. Access is also its own constraint, in cost, availability and session time, for a project meant to be reproducible at other sites.

Photogrammetry and structured-light scanning of the worn cap are defeated directly by the grommet problem described in §1.

Accepting the theoretical Cz uncorrected is current practice, and it is the baseline both methods below should be compared against. A method that does not beat this baseline is not worth its added complexity, and that comparison belongs in the validation.

**Open item:** confirm what co-registration equipment this lab has access to, and check the fNIRS co-registration literature for prior work on post-cap landmark recovery, so this proposal is positioned against what already exists.

---

## 4. Overview: two complementary methods

These solve different problems. They are not alternatives.

| | Method 1 | Method 2 |
|---|---|---|
| **Target** | Participants recruited from now on | Historical records; other institutions' data |
| **Approach** | Direct physical measurement | Statistical correction from head-shape features |
| **Requires** | Access to the participant | Only features already on record |
| **Cost** | Low; no special equipment | None beyond analysis |
| **Status** | Ready to test | Descriptive pilot; not yet a fitted model |

Decision path: if the participant can be measured, use Method 1. Method 2 exists for records where that is impossible.

The two are linked in one direction. Every participant processed through Method 1 produces a new labeled example for Method 2 (§6.5).

---

## 5. Method 1: C7-referenced landmark placement

*For participants recruited from now on.*

### 5.1 Rationale

Nz, Lpa and Rpa are all locatable with the cap on; only Iz is not. Instead of recovering the whole landmark set, this method recovers Iz alone, using a reference point the cap does not cover.

C7 is that reference. The path from C7 to Iz runs up the back of the neck and carries no grommets, so it stays measurable with the cap on, unlike any path crossing the cap's optode field.

### 5.2 Procedure

1. **Before the cap is fitted:** measure the scalp-surface (curved) distance from C7 to Iz on the bare head. Record it, along with the head posture used.
2. **Fit the cap** using the standard procedure.
3. **After the cap is fitted,** place markers at:
   - **Nz:** located directly at the brow.
   - **Lpa / Rpa:** located by palpating the preauricular point while the participant opens and closes their jaw.
   - **Iz:** palpate C7 (still exposed below the cap), then measure out the distance recorded in step 1 along the midline and place the marker there.
4. **Digitize** the four marker positions.
5. **Compute Cz** as the intersection of the Nz–Iz and Lpa–Rpa geodesics.
6. **Place a marker at the computed Cz on top of the cap.** A manual step performed after the calculation returns coordinates. It makes Cz visually locatable on the worn cap, which helps the physical-marker task (#01) and photo QC, and checks that the computed point lands plausibly on the cap surface.

### 5.3 Assumptions

- C7 does not shift relative to the skull between the pre-cap and post-cap measurement. This requires a consistent, controlled head posture at both time points, specified in the protocol and not left to the operator.
- The C7–Iz distance is measured as a curved, scalp-surface distance, matching the arc-distance convention the 10-20 system and the Cz calculation assume.
- Preauricular palpation is repeatable enough to place Lpa/Rpa consistently.

### 5.4 Known issues

**(a) The post-cap path runs above the pre-cap path.** Quantified below, and negligible at this cap thickness.

The distance is measured on bare scalp before the cap. Afterwards the final portion of that path runs over cap fabric, one thickness above the scalp. Tracing the same numeric distance therefore covers a slightly smaller angular span, so the marker falls short of the true Iz by a systematic amount.

For a path of length *L* traced at an elevation *t* above a surface of radius *R*, the shortfall measured on the scalp is approximately **L · t / R**.

With the cap thickness at t = 1 mm, the head radii implied by the two cap sizes in use (54 cm and 58 cm circumference, giving R ≈ 86–92 mm), and *L* taken as the portion of the path covered by fabric (on the order of 40 mm from the cap edge down to Iz), the shortfall is 0.43–0.47 mm. In the worst case, where the entire ~120 mm C7–Iz path ran over fabric, it would be 1.3–1.4 mm.

Both figures are an order of magnitude below the accuracy that matters for channel attribution (§2), and below the plausible repeatability of locating C7 by palpation. At 1 mm this effect is negligible, and palpation repeatability is the limiting error source instead (§5.5).

The residual concern is local bunching or tenting of the fabric, which adds path length beyond what the calculation above bounds. The fix is procedural: press the tape flat while measuring, and confirm the fabric lies smooth along the midline path before marking.

**(b) Two corrections for the cap were considered and deliberately not applied.**

*Path-length compensation.* Tracing a fixed length over a raised surface falls short of the target, so any compensating adjustment to the traced distance would have to be added, not subtracted. Its magnitude is L·t/R ≈ 0.4 mm, not the 1 mm cap thickness. Thickness does not map one-to-one onto positional error; it is scaled by the angular span of the covered path (≈ 0.44 rad here). Subtracting the full thickness would move the marker the wrong way and roughly triple the error it was meant to remove.

*Radial offset of the Iz marker.* The Iz marker sits on the cap surface, one thickness outside the scalp, while the Nz, Lpa and Rpa markers go on bare skin. The four landmarks therefore mix two reference surfaces, and the Iz point could in principle be projected 1 mm inward along the radius to make them consistent. That projection's effect on the computed Cz is again sub-millimetre.

*Why neither is applied.* Both terms are an order of magnitude smaller than the dominant error source: palpation of C7 and the preauricular points, realistically repeatable to a few millimetres at best. A correction below the noise floor does not improve accuracy. It adds a step to the protocol, another chance for operator error, and an impression of precision the measurement does not have. Both corrections are recorded here as evaluated and quantified, and left unimplemented.

This decision is conditional. Revisit it if validation (§5.5) shows palpation repeatability to be much better than assumed, since the relative size of these terms against palpation error is the entire basis for ignoring them.

**(c) Distance convention.** If the existing Cz calculation assumes arc distance but C7–Iz is captured with a straight tape, the derived Cz carries a systematic error. Confirm this against the geodesic calculation before running on participants. It affects Method 2's features equally.

**(d) Scope.** This method addresses Iz recovery only. Post-cap Nz/Lpa/Rpa placement is assumed reliable, not separately validated.

### 5.5 Validation plan

- **Baseline comparison:** report the error of the uncorrected theoretical Cz alongside the Method 1 estimate. The method must beat this baseline to justify itself (§3).
- **Accuracy:** for each participant, obtain an independent ground-truth Cz by marking all four landmarks and computing Cz *before* the cap is fitted, or with a digitizer where available. Report mean and maximum deviation (mm) against the threshold set in §2.
- **Systematic offset:** report the signed deviation, not only its magnitude, so any directional bias is visible instead of hidden inside an average error. Per §5.4(a) the cap-thickness contribution should be sub-millimetre, so a signed bias materially larger than that points elsewhere: fabric bunching, a posture change between the two measurements, or the distance-convention mismatch in §5.4(c).
- **Note on the error budget:** with cap geometry ruled out as a major contributor, landmark palpation should dominate the total error. The two reliability checks below therefore carry most of the validation's weight and are not optional extras.
- **Intra-rater repeatability:** same operator runs the full procedure twice on the same participant.
- **Inter-rater reliability:** two operators run the procedure on the same participant independently. C7 and preauricular palpation are both operator-dependent, and a method intended for use at other sites must survive a change of hands.
- **Sample size:** to be pre-specified with the team.

---

## 6. Method 2: feature-based Cz correction

*For historical records and other institutions' data, where the participant cannot be re-measured.*

Recovering Cz for our own historical records sits inside Task #02. Extending the same correction to other institutions is a proposed extension beyond the assigned task, and is treated as one throughout.

### 6.1 Rationale

Most historical participants have no confirmed Cz. The cap was fitted using the theoretical measurement, which carries the per-participant error described in §1, and those participants are no longer available.

Four are an exception. Participants #2, #3, #6 and #8 have a surgical marker placed at the grommet position corresponding to Cz, giving a directly confirmed Cz for those four.

If the relationship between recorded head-shape features and the true Cz can be characterised from those cases, it can be applied to records where only the features exist.

### 6.2 What is predicted: the deviation, not the coordinate

The target is the deviation vector between the theoretical Cz and the true Cz, not the absolute Cz coordinate.

The theoretical Cz already explains most of the variance: a larger head has a higher Cz, and the 10% calculation captures that. What it misses is the per-participant residual caused by scalp-shape variation. That residual has far smaller variance and is easier to characterise from few cases. The approach also fails safely. With no usable signal it degrades to applying the mean deviation, which still improves on no correction.

### 6.3 Tiered application by available features

Different records carry different measurements. Requiring one fixed feature set would make the method inapplicable to most of the data it targets, so the correction degrades in defined tiers:

| Tier | Available features | Approach | Expected accuracy |
|---|---|---|---|
| **A** | Landmark distances (Nz–Iz, Lpa–Rpa) **and** head circumference | Standardize features, reduce with PCA, regress the deviation on the components | Highest |
| **B** | **Head circumference only** — confirmed available for part of our historical set | Single-predictor regression: deviation as a function of head size | Intermediate |
| **C** | No usable head-shape features | Apply the population mean deviation from the labeled set — a constant correction | Lowest, but still better than no correction |

Two things follow from that, and both are what make the method practical.

- **Wider applicability.** Another institution needs only to check which tier its data supports, without matching our exact measurement protocol.
- **Tier tagging is mandatory.** Every estimate must be tagged with the tier that produced it, so downstream analyses can weight, flag, or exclude records by the quality of their Cz estimate instead of treating all estimates as equivalent. Without the tag, tiering hides uncertainty instead of managing it.

One further predictor may do better than circumference alone. Caps come in discrete sizes (54 cm and 58 cm here); heads do not. A participant with a 55 cm head in a 58 cm cap has considerably more slack than one with a 57.5 cm head in the same cap, and that slack is plausibly the mechanism producing the deviation this method is trying to predict. The mismatch between a participant's head circumference and the nominal size of the cap they wore is therefore a more direct candidate than circumference alone, and it is cheap to compute wherever both values are on record. Record cap size alongside every measurement for this reason.

Express features as dimensionless ratios (for example Nz–Iz ÷ head circumference) instead of raw centimetres. Ratios cancel differences in absolute scale and measurement instrument, which is what makes cross-site application plausible at all.

PCA appears only in Tier A, as a feature-reduction step for the strong intercorrelation among distance measures: a larger head increases nearly all of them together. PCA is not the predictor. The prediction comes from the regression fitted on the components. Plain PCA, not FAMD, since the predictors are continuous; FAMD would only be warranted if categorical predictors such as sex or cap size were added.

### 6.4 Current status: descriptive pilot, not a fitted model

With n=4 confirmed cases, no model should be fitted or reported as one. PCA on four samples yields at most three non-trivial components with essentially arbitrary loadings, and leave-one-out cross-validation returns four error estimates whose variance is too large to support inference.

The defensible step available now is descriptive:

1. Compute the deviation between theoretical and true Cz for each of the four confirmed cases.
2. Report their mean, range, and direction, including whether the deviations share a systematic direction, which would already justify a Tier C constant correction.
3. Relate each deviation to that participant's head circumference, and report the four points without fitting a line through them.
4. State how many labeled cases would be needed before Tiers A and B are worth fitting, and how they will be obtained (§6.5).

This is a weaker claim than "we built a predictive model," and it is the claim the evidence supports. It also makes the eventual model defensible once the sample grows, instead of retrofitted.

Applicability to other institutions is at this stage a future aim conditional on data, not a demonstrated property. It requires external validation that has not been performed.

### 6.5 Growing the labeled set

Method 1 is Method 2's data engine. Every participant processed through Method 1 produces a new confirmed-Cz label. The n=4 constraint is a starting point, not a ceiling: running Method 1 as standard procedure grows this set as a side effect, at no additional data-collection cost.

Two further routes:

- **Additional historical labels:** check whether any other historical participants received a surgical marker at the Cz grommet.
- **External head-shape data:** there is an established line of work on estimating 10-20 positions from head-surface geometry, so public MRI or anthropometric datasets may allow deriving scalp landmarks and Cz at scale. This has not been verified for this project. If a suitable dataset exists it would be the fastest route past the sample-size bottleneck, with our confirmed cases used for calibration and validation instead of training.

### 6.6 Assumptions

- The surgical marker on participants #2/#3/#6/#8 is an accurate ground truth for Cz.
- Features are measured comparably across every dataset the correction touches. Ratio features (§6.3) reduce but do not eliminate this exposure.
- A head-shape-to-deviation relationship characterised from a handful of individuals generalizes to others. This is the central and least-tested assumption.

### 6.7 Open issues

- **Sample size,** as above: the binding constraint.
- **Cross-institution comparability.** A model will emit a confident-looking estimate on non-comparable input without complaint. Mitigations: ratio features, publishing an explicit measurement SOP alongside any released model, tier tagging, and, where a target site can supply even a few confirmed cases, fitting a site-level offset.
- **Distance convention,** per §5.4(c), applied consistently across training features and any external data.

### 6.8 Validation plan

- **Now (n=4):** descriptive reporting per §6.4, plus the baseline comparison. How much of the error does a constant Tier C correction remove, relative to no correction at all? This is answerable at n=4 and is the most useful thing the current data can support.
- **Once the labeled set grows:** leave-one-out cross-validation as an interim check, then a properly held-out set once n permits. Metric: distance error (mm) between predicted and confirmed Cz, the same metric as Method 1, so both appear in one table.
- **Per tier:** report accuracy separately for each tier, so the cost of missing features is quantified instead of assumed.
- **Before any external application:** confirm the target site's features are comparably measured.

---

## 7. Summary

| | Method 1 | Method 2 |
|---|---|---|
| Solves | Cz for new participants | Cz for records that cannot be re-measured |
| Mechanism | C7 as a stable reference to recover Iz, then geodesic intersection | Correction of the theoretical Cz using recorded head-shape features, tiered by availability |
| Blocking issue | Distance convention; cap-thickness offset | Labeled sample size (n=4) |
| Dependency | — | Fed by Method 1's output |

Method 1 is the primary recommendation going forward. Method 2 is a secondary capability for legacy and cross-site data, currently at descriptive-pilot stage, whose viability improves automatically as Method 1 runs.

---

## 8. Open items for the team

1. **Set the accuracy threshold** (§2). Both methods' validation depends on it.
2. **Confirm the distance convention,** curved or straight-line, assumed by the existing Cz calculation (§5.4c). Blocks both methods.
3. **Confirm available co-registration equipment and check prior work** on post-cap landmark recovery (§3), so this proposal is positioned against standard practice.
4. **Audit the historical records** for which head-shape features are present, to establish how many records fall into each tier (§6.3).
5. **Check for additional confirmed-Cz cases** beyond #2/#3/#6/#8.
6. **Decide sequencing:** pursue Method 2 now, or prioritise accumulating labels via Method 1 first.
7. **Note for other Digitization tasks:** the post-cap landmark recovery in §5.2 (steps 1–4) is not Cz-specific. Tasks #01 (physical marker) and #03 (optode labelling) need the same landmark set and may be able to consume it directly instead of solving it separately.
