## Dataset Acknowledgement

The datasets used in this study were downloaded from the **FairData repository** under the title *“NMC, NCA, and LFP Cells Degradation Under Randomized Current Profiles.”*

- **Data identification number:** `10.23729/b07462e8-9e31-428c-bdd5-deb1890c608b`
- **Direct DOI URL:** https://doi.org/10.23729/b07462e8-9e31-428c-bdd5-deb1890c608b
- **FairData dataset page:** https://etsin.fairdata.fi/dataset/f60a7388-99b6-4637-96d5-8610a7f71612

Grateful acknowledgement is given to the **New Energy Research Center, Turku University of Applied Sciences, Turku, Finland**, for conducting the battery degradation experiments, collecting the voltage, current, temperature, and operating-profile measurements, and making the raw and processed datasets publicly available through FairData. 


## 1. Dataset Composition

The downloaded collection contains eight physical lithium-ion cells distributed across three battery chemistries.

```math
\mathcal{C}
=
\left\{
\mathrm{LFP},
\mathrm{NCA},
\mathrm{NMC}
\right\}.
```

| Chemistry | Physical cells | Number of cells |
|:---:|:---|---:|
| LFP | `LFP_CELL_1`, `LFP_CELL_2` | 2 |
| NCA | `NCA_CELL_1`, `NCA_CELL_2`, `NCA_CELL_3`, `NCA_CELL_4` | 4 |
| NMC | `NMC_CELL_1`, `NMC_CELL_2` | 2 |
| **Total** | — | **8** |

Additional reference files include:
- chemistry-specific open-circuit-voltage measurements;
- ambient-temperature measurements;
- experimental comments;
- experimental protocol descriptions.

Each physical-cell file contains multiple experimental segments. One segment represents either a complete test trajectory or one stage of an experimental cycle.

Let $N_c$ denote the number of registered experimental segments for physical cell $c$. The segment counts are summarized below.

| Physical cell | Chemistry | Segment count |
|:---|:---:|---:|
| `LFP_CELL_1` | LFP | 660 |
| `LFP_CELL_2` | LFP | 672 |
| `NCA_CELL_1` | NCA | 602 |
| `NCA_CELL_2` | NCA | 505 |
| `NCA_CELL_3` | NCA | 576 |
| `NCA_CELL_4` | NCA | 697 |
| `NMC_CELL_1` | NMC | 617 |
| `NMC_CELL_2` | NMC | 613 |
| **Total** | — | **4,942** |

The total number of experimental segments is
```math
\begin{aligned}
N_{\mathrm{segments}}
&=
660+672+602+505+576+697+617+613 \\
&=
4{,}942.
\end{aligned}
```
The chemistry-level segment totals are
```math
N_{\mathrm{LFP}}
=
660+672
=
1{,}332,
```
```math
N_{\mathrm{NCA}}
=
602+505+576+697
=
2{,}380,
```
and
```math
N_{\mathrm{NMC}}
=
617+613
=
1{,}230.
```
Therefore,
```math
\begin{aligned}
N_{\mathrm{segments}}
&=
N_{\mathrm{LFP}}
+
N_{\mathrm{NCA}}
+
N_{\mathrm{NMC}} \\
&=
1{,}332
+
2{,}380
+
1{,}230 \\
&=
4{,}942.
\end{aligned}
```
The NCA chemistry contributes the largest number of segments because it contains four physical cells, whereas the LFP and NMC groups each contain two cells. 

<img width="1869" height="1404" alt="image" src="https://github.com/user-attachments/assets/83d55d6c-1131-4e4e-9772-79c6974de653" />

### Segment-level current-span versus voltage-span diversity for LFP, NCA, and NMC cells. 

<img width="1876" height="724" alt="image" src="https://github.com/user-attachments/assets/16be399c-64d6-47e9-a679-4a83c37217a6" />

Each point represents one experimental segment. The horizontal axis shows the current span, $`\Delta I_s = I_{\max,s} - I_{\min,s}`$, while the vertical axis shows the corresponding terminal-voltage span, $`\Delta V_s = V_{\max,s} - V_{\min,s}`$.

The figure characterizes the electrical excitation and voltage-response diversity of the three battery chemistries. The chemistry-specific clusters reveal differences in electrical excitation, voltage-response magnitude, and operating-domain coverage across the raw dataset.
- **LFP segments** are mainly distributed over current spans of approximately **4–18 A**, with most voltage spans concentrated near **1.1 V**. Several lower-voltage-span segments indicate comparatively mild voltage variation under some operating profiles.
- **NCA segments** form a dense cluster at current spans of approximately **6.5–8 A**. Their voltage spans are mostly between **1.35 and 1.50 V**, with several segments extending toward **1.9 V**. This pattern indicates relatively consistent current excitation but greater variation in voltage response.
- **NMC segments** cover the widest current-span range, extending to approximately **24 A**. Most NMC voltage spans are concentrated near **1.7 V**, indicating strong electrical excitation and comparatively broad terminal-voltage variation.
The chemistry-specific clusters show that current excitation and voltage response are not uniformly distributed across the dataset. NMC provides the broadest current-range coverage, NCA occupies a concentrated excitation region with variable voltage response, and LFP generally exhibits lower voltage-span values.No universal linear relationship is evident between current span and voltage span.This figure is descriptive and does not establish measurement validity or causality. Isolated or extreme segments require examination during the quality-control stage.


<img width="1934" height="1308" alt="image" src="https://github.com/user-attachments/assets/c8837261-2045-4354-ad50-798b3e184c7d" />

Timestamp decoding is generally successful because parse failures is rare and negative time steps are absent. The principal concern is the high duplicate-timestamp count. Before schema/segement harmonization, duplicate detection can be verified at the segment level to distinguish true repeated timestamps from valid clock resets between experimental segments. The ambient-temperature dataset can be disregarded at this stage. 


### Physical-Cell Positive Sampling-Interval Distributions

<img width="2189" height="863" alt="image" src="https://github.com/user-attachments/assets/d0411465-062c-4552-8f45-35faa5754005" />

This empirical cumulative distribution function compares the positive sampling intervals of the LFP, NCA, and NMC physical-cell datasets.
For consecutive valid timestamps within a segment, the sampling interval is $`\Delta t_k = t_k - t_{k-1}`$,
where only intervals satisfying $`\Delta t_k > 0`$ are included.

The LFP, NCA, and NMC curves almost completely overlap, indicating that the three chemistries use essentially the same sampling cadence.
The distributions are concentrated around **1 second**:
- a small fraction of intervals occurs near **0.999 s**;
- - the dominant proportion occurs at approximately **1.000 s**;
- the remaining small fraction occurs near **1.001 s**.

The sharp vertical increase at $`\Delta t = 1\ \mathrm{s}`$ shows that most measurements were recorded at a nominal frequency of approximately
$`f_s = \frac{1}{\Delta t} \approx 1\ \mathrm{Hz}`$.

The small deviations around one second are likely caused by timestamp precision, rounding, or numerical conversion rather than meaningful changes in the data-acquisition frequency. The horizontal axis covers only a very narrow range around one second. Its scientific-notation labels visually enlarge differences that are only about one millisecond. The near-identical curves confirm a stable and chemistry-independent nominal sampling interval. This consistency supports later cross-chemistry harmonization and dynamic model identification without requiring major sampling-rate conversion.

<img width="2189" height="881" alt="image" src="https://github.com/user-attachments/assets/da2eeb5d-2576-4bd7-a3b5-381e8da059a1" />
Empirical cumulative distributions of positive sampling intervals for the LFP, NCA, and NMC OCV references and the ambient-temperature dataset. The overlapping OCV curves indicate uniform one-second sampling, while the ambient data exhibit only negligible deviations around the same nominal interval.

## Calendar-Time Coverage of Decoded Datasets
<img width="1926" height="881" alt="image" src="https://github.com/user-attachments/assets/30ddefdd-1ca4-495c-9b42-180d9cf8fe51" />
This timeline summarizes the first and last decoded timestamps of every physical-cell, OCV-reference, and ambient-temperature dataset.
- **Rows** represent individual timing datasets.
- **Horizontal lines** represent the calendar interval between the earliest and latest valid timestamps.
- **Endpoint markers** identify the beginning and end of each recorded period.
- **The horizontal axis** covers approximately June to October 2024
Each horizontal line shows only the interval from the first to the last valid timestamp. Most physical-cell experiments span mid-June to late September 2024, while the OCV references occupy short periods in early June. The ambient-temperature record overlaps with most experiments, supporting later temporal alignment.


## Standardized Voltage and Source-Current Ranges

<img width="1921" height="1111" alt="image" src="https://github.com/user-attachments/assets/4e08db59-10b8-4ea9-84ce-90beb9a760b6" />
The term **standardized** refers to consistent variable names, units, and sign conventions; it does not mean that the signals have been statistically normalized or scaled.

This figure compares the minimum-to-maximum terminal-voltage and source-current ranges of the eight physical cells after schema and unit harmonization. Negative source current denotes discharge and positive source current denotes charge Each horizontal line represents the complete observed range for one cell, while the endpoint markers indicate the corresponding minimum and maximum values.
### Terminal-Voltage Range
The upper panel shows the standardized terminal-voltage intervals.
- **LFP cells** operate over the narrowest and lowest voltage range, approximately **2.45–3.62 V**.
- **NCA cells** extend from approximately **2.38–2.50 V** to **4.20–4.38 V**.
- **NMC cells** cover approximately **2.47–4.20 V**.
The separation between LFP and the nickel-based chemistries is consistent with their different electrochemical operating windows. The similarity between cells of the same chemistry also indicates that voltage units and column definitions were harmonized consistently.
### Source-Current Range
The lower panel presents the standardized source-current intervals. The original sign convention is retained:
- negative current denotes discharge;
- positive current denotes charge.
The main observations are:
- **LFP cells** cover approximately **−15 to +3 A**;
- **NCA cells** occupy a narrower interval of approximately **−5 to +3 A**;
- **NMC cells** show the broadest excitation range, extending from approximately **−19 to +4 A**.
The wider NMC range indicates stronger discharge and charge excitation, while the NCA experiments use a more concentrated current domain.

The figure confirms that voltage and current measurements were transformed into common canonical units without removing chemistry-specific operating differences. These standardized ranges support direct cross-cell comparison and later LPV model construction.

The displayed limits are observed data ranges rather than formal quality-control thresholds. Extreme values remain subject to evaluation during the subsequent quality-control stage. 

<img width="1944" height="1434" alt="image" src="https://github.com/user-attachments/assets/dc6c2d2b-a162-4978-bf78-032a18255fc5" />
This figure presents the synchronized voltage, source-current, and cell-temperature signals for `LFP_CELL_1`, segment 601, over approximately **7,700 seconds**. All three signals use the same standardized elapsed-time coordinate, demonstrating successful schema and unit harmonization. During the first approximately **1,200 seconds**, the source current is predominantly negative and includes several pulses reaching nearly **−15 A**. Under the adopted sign convention, negative current denotes discharge.
The terminal voltage responds immediately to these load changes. Repeated current pulses produce corresponding voltage drops, with the lowest voltage approaching approximately **2.5 V**. These rapid responses reflect the combined effects of ohmic resistance and transient polarization. The cell temperature rises from approximately **28 °C** to more than **43 °C**, indicating substantial heat generation during the high-current discharge period.

After approximately **1,200 seconds**, the current returns close to zero. The voltage gradually recovers from below **2.8 V** toward approximately **3.1 V**.This recovery is consistent with relaxation after removal of the discharge load. During the same interval, the temperature decreases steadily as internally generated heat dissipates.At approximately **2,400 seconds**, the current changes to about **+3 A**. Positive current denotes charging.
The terminal voltage consequently increases from approximately **3.1 V** to the upper operating region near **3.6 V**. The relatively smooth voltage increase indicates continued charging under an approximately constant-current condition. The temperature remains considerably lower than its earlier peak and varies around **31–32 °C**, showing that the thermal response during this moderate charging period is less severe than during the initial high-current discharge pulses.Near **5,100 seconds**, a brief current transition produces a visible voltage disturbance. The current subsequently decreases toward zero, and the terminal voltage relaxes from approximately **3.6 V** to about **3.45 V**. The cell temperature also decreases gradually toward its initial level, reaching approximately **28 °C** by the end of the segment.



## Baseline Capacity and Accepted Reference-Capacity Events

<img width="1958" height="1394" alt="image" src="https://github.com/user-attachments/assets/1cc0df38-f669-4e6e-b48b-4abdc39b7400" />

This figure summarizes two important outputs of the capacity-estimation stage for the eight physical cells.

### Cell-Specific Baseline Capacities
The upper panel presents the baseline capacity assigned to each cell:
| Physical cell | Baseline capacity |
|---|---:|
| `LFP_CELL_1` | 2.782 Ah |
| `LFP_CELL_2` | 2.769 Ah |
| `NCA_CELL_1` | 2.524 Ah |
| `NCA_CELL_2` | 2.491 Ah |
| `NCA_CELL_3` | 2.502 Ah |
| `NCA_CELL_4` | 2.521 Ah |
| `NMC_CELL_1` | 3.855 Ah |
| `NMC_CELL_2` | 3.850 Ah |

The capacities are closely matched within each chemistry but differ substantially between chemistries. NMC cells have the largest baseline capacities, followed by LFP and NCA cells. These differences mainly reflect cell design and nominal capacity rather than degradation. The cell-specific baseline is used to calculate event-level state of health:
$`\mathrm{SOH}_{c,e}=Q_{c,e}/Q_{c,\mathrm{baseline}}`$,
where $`Q_{c,e}`$ is the measured capacity of event $`e`$ and $`Q_{c,\mathrm{baseline}}`$ is the baseline capacity of cell $`c`$.
### Accepted Reference-Capacity Events
The lower panel shows the number of accepted reference-discharge events available for each cell.
The accepted-event counts range from **19** for `NCA_CELL_2` to **28** for `NCA_CELL_4`. Most cells contain between **23 and 27** accepted events, indicating repeated capacity measurements across the degradation experiment. Differences in event count indicate unequal capacity-monitoring coverage. Cells with fewer accepted events may provide lower temporal resolution for degradation and SOH analysis.

### Main Significance

The figure confirms that:
- baseline capacities are chemistry- and cell-specific;
- within-chemistry capacity estimates are consistent;
- repeated reference-capacity events are available for all cells;
- sufficient measurements exist for tracking capacity degradation and SOH evolution;
- event coverage is not identical across cells and should be considered during comparative analysis.

The baseline capacities shown here are preprocessing references. Training-only baselines are reconstructed after chronological data splitting to prevent future capacity information from entering model calibration.


## Reference Discharge-Capacity and Event-Level SOH Evolution

<img width="1916" height="1431" alt="image" src="https://github.com/user-attachments/assets/8e6585f0-c5bd-4a49-b567-ee6783a42390" />

This figure shows the evolution of accepted reference-discharge capacity events and the corresponding state of health for all eight physical cells. The horizontal axis represents the segment index at which each capacity event occurs and therefore provides the chronological position of the measurement within each cell experiment.
### Reference Discharge-Capacity Evolution
The upper panel reports the measured discharge capacity, $`Q_{c,e}`$, for capacity event $`e`$ of cell $`c`$.
- **LFP cells** begin near **2.78 Ah** and decline gradually to approximately **2.45–2.52 Ah**. Their trajectories are smooth and similar, indicating relatively consistent degradation behavior.
- **NMC cells** begin near **3.9 Ah** and decrease steadily to approximately **3.35 Ah**. The two NMC trajectories remain closely aligned throughout the experiment.
- **NCA cells** exhibit greater cell-to-cell variability.  
  - `NCA_CELL_1` decreases from approximately **2.5 Ah** to **1.7 Ah**.  
  - `NCA_CELL_2` shows moderate degradation with several local fluctuations.  
  - `NCA_CELL_3` contains a sharp temporary reduction near segment 500 followed by partial recovery.  
  - `NCA_CELL_4` displays the most severe decline, decreasing from approximately **2.6 Ah** to below **0.5 Ah**.

### Event-Level State of Health
The lower panel normalizes each capacity measurement by the corresponding cell-specific baseline:
$`\mathrm{SOH}_{c,e}=Q_{c,e}/Q_{c,\mathrm{baseline}}`$.

The dashed horizontal line at $`\mathrm{SOH}=1`$ represents the baseline condition.

- LFP cells retain approximately **89–91%** of their baseline capacity.
- NMC cells retain approximately **86–87%**.
- `NCA_CELL_1` declines to approximately **67%**.
- `NCA_CELL_2` and `NCA_CELL_3` generally remain between approximately **84% and 90%**, except for isolated irregular events.
- `NCA_CELL_4` declines to approximately **18%**, indicating exceptionally severe capacity loss or a record requiring detailed validation.

The figure illustrates clear chemistry and cell dependent degradation patterns. LFP and NMC cells show comparatively smooth and consistent capacity decline, whereas NCA cells exhibit substantially greater heterogeneity. The abrupt dip and recovery in `NCA_CELL_3` and the extreme decline in `NCA_CELL_4` should be reviewed against segment quality, discharge completeness, temperature, current integration, and event-acceptance criteria before being interpreted solely as physical degradation.

###  Chemistry-Specific Monotone OCV–SOC Curves
<img width="1834" height="1134" alt="image" src="https://github.com/user-attachments/assets/c8cadbd9-b053-49ba-8628-a86f2d50a865" />

This figure compares the fitted open-circuit-voltage relationships for LFP, NCA, and NMC cells. The horizontal axis represents state of charge, while the vertical axis represents open-circuit voltage. The chemistry-specific relationship is written as
$`V_{\mathrm{OCV}} = f_{\mathrm{chem}}(\mathrm{SOC})`$,
where $`f_{\mathrm{chem}}`$ is constrained to be nondecreasing. This monotonicity permits stable inverse estimation of SOC from low-current voltage measurements.
The solid lines show the final monotone OCV–SOC curves, while the transparent points show the fitted voltage observations used during curve construction.
#### LFP Curve
The LFP curve extends from approximately **2.6 V** at very low SOC to approximately **3.4 V** near full charge. It contains a long, nearly flat region around **3.2–3.3 V** over much of the SOC interval. 
#### NCA Curve
The NCA curve increases from approximately **2.9 V** at low SOC to approximately **4.17 V** at full charge. Compared with LFP, the curve has a more continuous positive slope across the SOC range. The stronger voltage gradient provides greater sensitivity for voltage-based SOC correction. 
#### NMC Curve
The calibrated NMC curve begins near SOC **0.20** at approximately **3.66 V** and increases to approximately **4.18 V** at full charge. The curve rises gradually through the middle SOC range and becomes flatter near high SOC before increasing again close to full charge. 
### Fitted-Observation Deviations
Several observations lie far from the final monotone curves, including isolated high-voltage points for NCA and NMC. These observations should remain auditable rather than being interpreted automatically as equilibrium OCV values.

The figure confirms that each chemistry requires a separate OCV–SOC mapping. A common curve would incorrectly combine the LFP voltage plateau with the higher and more continuously varying NCA and NMC voltage ranges.
The monotone curves support:
- low-current SOC anchoring;
- inversion from voltage to SOC;
- chemistry-specific SOC estimation;
- detection of observations outside the calibrated SOC range;
- initialization of battery-state estimators.



## Chronological Primary-Split Assignment

<img width="1884" height="919" alt="image" src="https://github.com/user-attachments/assets/8e44a29a-b7d0-4f1c-bf3f-b75df625c138" />

This figure shows the chronological assignment of complete experimental segments to the training, calibration, and test partitions for all eight physical cells.

- **Horizontal axis:** normalized cumulative lifetime progression from 0 to 1.
- **Vertical axis:** physical-cell identifier.
- **Blue:** training segments.
- **Green:** calibration segments.
- **Red:** test segments.
- **Each marker:** one complete experimental segment.

For cell \(c\), the normalized lifetime position may be interpreted as

$`\lambda_{c,s}\in[0,1]`$,

where $`\lambda_{c,s}=0`$ represents the beginning of the recorded experiment and $`\lambda_{c,s}=1`$ represents its end.
All cells follow the required chronological order:

$`\text{training}\rightarrow\text{calibration}\rightarrow\text{testing}`$.

The training partition occupies approximately the first **60%** of each cell lifetime, the calibration partition generally covers the next **20%**, and the test partition covers the final **20%**.The exact split boundaries differ slightly among cells because partition selection is based on complete segments or aging epochs and valid transition counts rather than cutting individual rows at fixed percentages. This preserves experimental integrity and prevents one trajectory from appearing in more than one partition.No calibration or test segment appears before the training region, and no training segment reappears after calibration begins. Similarly, test segments occur only after the calibration region. This confirms chronological exclusivity. Small visible gaps, particularly in several NCA trajectories, may represent spacing between normalized segment positions, excluded or embargoed units, or uneven experimental coverage. They should not automatically be interpreted as deleted observations.

#### Leakage-Control Significance

Random row-level splitting would allow temporally adjacent samples from the same experiment to appear in both training and testing data. Such overlap would produce optimistic performance estimates.

The chronological segment-level split prevents:

- samples from one segment entering multiple partitions;
- future degradation states influencing training;
- aging epochs being shared across partitions;
- calibration or test information being used to construct training features.

The final test set therefore represents later-life operating conditions that were unavailable during model fitting.

The figure confirms a consistent leakage-free partition structure across LFP, NCA, and NMC cells. Training uses early-life data, calibration uses intermediate-life data, and testing uses the latest available degradation period.

## Primary Split Composition by Physical Cell and Chemistry
<img width="1909" height="1426" alt="image" src="https://github.com/user-attachments/assets/b7aeef65-583b-4bfe-a5a8-cd28bc0851aa" />

This figure summarizes the proportion of valid dynamic transitions assigned to the training, calibration, test, and embargo partitions.

#### Physical-Cell Composition

The upper panel reports the split composition for each of the eight physical cells. Every stacked bar sums to one and therefore represents the complete set of valid transitions for that cell.
The achieved proportions are close to the intended chronological allocation:

- approximately **60–62%** for training;
- approximately **18–22%** for calibration;
- approximately **18–21%** for testing;
- a negligible or zero visible fraction for embargo.

The small differences among cells arise because partition boundaries are selected using complete experimental segments or aging epochs rather than cutting individual samples at exact percentage thresholds. NCA_CELL_2` and `NCA_CELL_4` contain slightly larger training shares, while some other cells contain marginally larger calibration or test shares. These differences are small and do not indicate substantial partition imbalance.

#### Chemistry-Level Composition

The lower panel aggregates valid transitions across all cells within each chemistry. The chemistry-level proportions remain close to the target structure:

$`\text{Training} \approx 60\%`$,

$`\text{Calibration} \approx 20\%`$,

and

$`\text{Testing} \approx 20\%`$.

LFP, NCA, and NMC therefore contribute comparable relative proportions to each partition despite differences in the number of physical cells, experimental segments, and total samples.

#### Embargo Interpretation

Although embargo is included in the legend, no substantial orange region is visible. This indicates that the saved primary split either contains no embargo transitions or contains a fraction too small to be visually distinguishable. The absence of a large embargo region does not imply data leakage. Leakage prevention is primarily achieved through chronological ordering, segment-level assignment, and aging-epoch exclusivity.

The figure confirms that the chronological splitting procedure achieved balanced training, calibration, and test coverage at both the cell and chemistry levels. This supports fair cross-cell and cross-chemistry model comparison while preserving complete experimental units.

The plotted fractions are based on valid dynamic transitions rather than raw rows:

$` p_{c,r} = \frac{N_{c,r}^{\mathrm{transition}}} {\sum_{q}N_{c,q}^{\mathrm{transition}}},`$

where $`p_{c,r}`$ is the transition fraction assigned to partition $`r`$ for cell $`c`$.



## LPV Model-Readiness by Physical Cell and Chemistry

<img width="1934" height="1351" alt="image" src="https://github.com/user-attachments/assets/b5c6bbee-e1cd-46e6-83ed-c572cca8c490" />

This figure reports the fraction of saved rows that satisfy three progressively different model-readiness conditions:

- **Scheduling variables complete:** all required scheduling variables—SOC, transformed current, temperature, and SOH—are available.
- **LPV identification valid:** the row contains complete scheduling information and satisfies the conditions required for LPV parameter identification.
- **Strict voltage evaluation valid:** the row also satisfies the additional requirements imposed for strict terminal-voltage evaluation.

#### Physical-Cell-Level Results
The upper panel shows that complete scheduling-variable coverage varies between approximately **27% and 38%** across the eight cells.
- `NCA_CELL_4` has the highest readiness, at approximately **37–38%**.
- `LFP_CELL_1` and `LFP_CELL_2` provide approximately **35–37%** valid coverage.
- `NCA_CELL_2` provides approximately **32%**.
- `NCA_CELL_1`, `NCA_CELL_3`, and `NMC_CELL_2` provide approximately **28–29%**.
- `NMC_CELL_1` has the lowest coverage, at approximately **27%**.

The blue and orange bars are nearly identical for every cell. This indicates that almost every row with complete scheduling variables also satisfies the LPV-identification mask. Consequently, the principal limitation is the availability of complete SOC, temperature, current, and SOH information rather than an additional identification-stage exclusion.

#### Chemistry-Level Results

The lower panel aggregates the same quantities by chemistry:

- **LFP:** approximately **36%** model-ready rows;
- **NCA:** approximately **32%**;
- **NMC:** approximately **28%**.

LFP therefore provides the largest relative proportion of usable LPV-identification rows, while NMC provides the smallest. These percentages describe relative coverage.

#### Strict Voltage-Evaluation Coverage

The green bars are almost zero for all cells and chemistries. Only a very small fraction appears for `NCA_CELL_1`. This result indicates that the strict voltage-evaluation mask is substantially more restrictive than the LPV-identification mask. Possible limiting requirements include:

- valid next-step voltage targets;
- valid consecutive dynamic transitions;
- complete split-safe state information;
- acceptable timing intervals;
- exclusion of segment boundaries;
- absence of review or leakage flags;
- availability of all required evaluation variables.

The figure shows that approximately one-third of the saved observations are suitable for LPV identification. The similarity between scheduling completeness and LPV validity confirms that missing or unavailable scheduling-state information is the dominant restriction. However, the almost absent strict voltage-evaluation subset is a critical diagnostic result.



## Ambient-Temperature Alignment Quality

<img width="1934" height="1433" alt="image" src="https://github.com/user-attachments/assets/b6d9c355-2a79-44be-b961-cab48415ed76" />

This figure evaluates the causal alignment of ambient-temperature observations with the battery measurements.
For battery timestamp $`t_k`$, the backward matching lag is

$`\Delta t_k^{\mathrm{ambient}} = t_k - t_k^{\mathrm{ambient}}`$,

where causal alignment requires

$`\Delta t_k^{\mathrm{ambient}} \geq 0`$.


#### Ambient-Alignment Outcomes
The upper panel reports three row-level fractions:

- **Valid causal match:** an earlier ambient observation was found within the permitted tolerance;
- **Tolerance exceeded:** no sufficiently recent ambient observation was available;
- **Future match:** an ambient observation from the future was assigned.

Most cells achieve high valid-match coverage:

- `NCA_CELL_4` reaches approximately **100%** valid alignment;
- LFP and NMC cells achieve approximately **96%**;
- `NCA_CELL_1` and `NCA_CELL_3` achieve approximately **90%**;
- `NCA_CELL_2` has the lowest coverage at approximately **78%**.

The tolerance-exceeded fraction is largest for `NCA_CELL_2`, at approximately **22%**, indicating weaker temporal overlap with the ambient-temperature record.
No visible future-match fraction occurs for any cell. This confirms that the alignment procedure preserves temporal causality.

### Distribution of Valid Match Lags

The lower panel shows the lag distribution only for successfully matched observations.

Most valid matches occur with lags near **0–1 s**, which is consistent with the approximately one-second sampling rate of the battery and ambient datasets. The dashed line at **2 s** marks the review threshold, while the dotted line at **10 s** marks the maximum matching tolerance. A small number of outlying valid lags are visible:
- approximately **4 s** for `LFP_CELL_1`;
- approximately **5 s** for `NCA_CELL_2`;
- approximately **7 s** for `NMC_CELL_1`.
These observations exceed the review threshold but remain below the 10-second matching tolerance. They are therefore retained as valid causal matches while remaining identifiable for sensitivity analysis. Rows classified as tolerance-exceeded are not represented in the lower box plots because those plots contain only valid matches.

The figure confirms that ambient-temperature alignment is predominantly successful and strictly causal. Most accepted matches are temporally close to the corresponding battery observations, and no future environmental measurements are introduced.



## LPV-Identification Scheduling-Space Density

<img width="1901" height="618" alt="image" src="https://github.com/user-attachments/assets/fa833476-8e1f-480e-a8c1-fc00ece2eadc" />

This figure shows the operating-space coverage of rows accepted for LPV identification for the LFP, NCA, and NMC chemistries. The horizontal axis represents split-safe state of charge, while the vertical axis represents the transformed current scheduling variable:

$`\rho_I=\log\left(1+\frac{|I|}{I_{\mathrm{ref}}}\right)`$.

Therefore, larger vertical-axis values indicate greater current magnitude, regardless of whether the original source current represents charging or discharging. Current direction is retained separately by the scheduling-direction variable.

The color scale represents $`\log(1+n)`$, where $`n`$ is the number of valid LPV rows within a scheduling-space bin:

- black regions contain no or very few observations;
- dark red regions indicate low density;
- orange and yellow regions indicate progressively higher density.

####  LFP Scheduling Coverage
The LFP data form several narrow horizontal bands near transformed-current values of approximately 0, 0.45, 0.77, and 1.20. These bands indicate repeated operation at discrete current levels. A descending family of trajectories appears near high SOC, approximately from SOC 1.0 to slightly above 1.0. This structure reflects the relationship between SOC evolution and current changes during particular charging or discharge protocols. LFP coverage is concentrated along specific operating trajectories rather than uniformly distributed throughout the two-dimensional domain.

#### NCA Scheduling Coverage

NCA provides the broadest and most heterogeneous scheduling-space coverage. Valid observations extend over a wide SOC interval and include numerous current levels.
The densest region occurs approximately between:
- SOC 0.4–1.0;
- transformed current 0.2–0.7.
Several horizontal bands and curved trajectories are visible, indicating repeated current setpoints together with dynamically changing current profiles. Compared with LFP and NMC, NCA provides the richest excitation diversity for identifying SOC- and current-dependent LPV parameters.

#### NMC Scheduling Coverage

NMC exhibits several dominant horizontal bands near transformed-current values of approximately 0, 0.57, 0.93, and 1.40. A pronounced descending trajectory appears near high SOC. However, the intermediate and low-SOC regions contain substantially less coverage than the corresponding NCA panel.

The figure demonstrates that the scheduling variables are not sampled uniformly. Identification reliability is expected to be strongest in high-density regions and weaker in black or sparsely populated regions.

The narrow bands also show that much of the dataset follows predefined experimental current levels. Consequently, apparent coverage over a broad SOC range does not necessarily imply equally broad current excitation at every SOC value.

NCA provides the broadest two-dimensional excitation coverage, while LFP and NMC are more strongly concentrated along discrete current bands and high-SOC trajectories. The figure therefore identifies where LPV parameter estimation is data-supported and where predictions would involve interpolation or extrapolation.
