


## Dataset Acknowledgement

The datasets used in this study were downloaded from the **FairData repository** under the title *“NMC, NCA, and LFP Cells Degradation Under Randomized Current Profiles.”*

- **Data identification number:** `10.23729/b07462e8-9e31-428c-bdd5-deb1890c608b`
- **Direct DOI URL:** https://doi.org/10.23729/b07462e8-9e31-428c-bdd5-deb1890c608b
- **FairData dataset page:** https://etsin.fairdata.fi/dataset/f60a7388-99b6-4637-96d5-8610a7f71612

Grateful acknowledgement is given to the **New Energy Research Center, Turku University of Applied Sciences, Turku, Finland**, for conducting the battery degradation experiments, collecting the voltage, current, temperature, and operating-profile measurements, and making the raw and processed datasets publicly available through FairData. 



# Note: Python code was written with AI assistance; however, the structure has been debugged and verified

## Pre-Processnig Plots 
####
1. Dataset Composition

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


#### Physical-Cell Positive Sampling-Interval Distributions

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

#### Calendar-Time Coverage of Decoded Datasets
<img width="1926" height="881" alt="image" src="https://github.com/user-attachments/assets/30ddefdd-1ca4-495c-9b42-180d9cf8fe51" />
This timeline summarizes the first and last decoded timestamps of every physical-cell, OCV-reference, and ambient-temperature dataset.
- **Rows** represent individual timing datasets.
- **Horizontal lines** represent the calendar interval between the earliest and latest valid timestamps.
- **Endpoint markers** identify the beginning and end of each recorded period.
- **The horizontal axis** covers approximately June to October 2024
Each horizontal line shows only the interval from the first to the last valid timestamp. Most physical-cell experiments span mid-June to late September 2024, while the OCV references occupy short periods in early June. The ambient-temperature record overlaps with most experiments, supporting later temporal alignment.


#### Standardized Voltage and Source-Current Ranges

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



#### Baseline Capacity and Accepted Reference-Capacity Events

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

#### Main Significance

The figure confirms that:
- baseline capacities are chemistry- and cell-specific;
- within-chemistry capacity estimates are consistent;
- repeated reference-capacity events are available for all cells;
- sufficient measurements exist for tracking capacity degradation and SOH evolution;
- event coverage is not identical across cells and should be considered during comparative analysis.

The baseline capacities shown here are preprocessing references. Training-only baselines are reconstructed after chronological data splitting to prevent future capacity information from entering model calibration.


#### Reference Discharge-Capacity and Event-Level SOH Evolution

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

#### Event-Level State of Health
The lower panel normalizes each capacity measurement by the corresponding cell-specific baseline:
$`\mathrm{SOH}_{c,e}=Q_{c,e}/Q_{c,\mathrm{baseline}}`$.

The dashed horizontal line at $`\mathrm{SOH}=1`$ represents the baseline condition.

- LFP cells retain approximately **89–91%** of their baseline capacity.
- NMC cells retain approximately **86–87%**.
- `NCA_CELL_1` declines to approximately **67%**.
- `NCA_CELL_2` and `NCA_CELL_3` generally remain between approximately **84% and 90%**, except for isolated irregular events.
- `NCA_CELL_4` declines to approximately **18%**, indicating exceptionally severe capacity loss or a record requiring detailed validation.

The figure illustrates clear chemistry and cell dependent degradation patterns. LFP and NMC cells show comparatively smooth and consistent capacity decline, whereas NCA cells exhibit substantially greater heterogeneity. The abrupt dip and recovery in `NCA_CELL_3` and the extreme decline in `NCA_CELL_4` should be reviewed against segment quality, discharge completeness, temperature, current integration, and event-acceptance criteria before being interpreted solely as physical degradation.

####  Chemistry-Specific Monotone OCV–SOC Curves
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



#### Chronological Primary-Split Assignment

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

#### Primary Split Composition by Physical Cell and Chemistry
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



#### LPV Model-Readiness by Physical Cell and Chemistry

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



#### Ambient-Temperature Alignment Quality

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

#### Distribution of Valid Match Lags

The lower panel shows the lag distribution only for successfully matched observations.

Most valid matches occur with lags near **0–1 s**, which is consistent with the approximately one-second sampling rate of the battery and ambient datasets. The dashed line at **2 s** marks the review threshold, while the dotted line at **10 s** marks the maximum matching tolerance. A small number of outlying valid lags are visible:
- approximately **4 s** for `LFP_CELL_1`;
- approximately **5 s** for `NCA_CELL_2`;
- approximately **7 s** for `NMC_CELL_1`.
These observations exceed the review threshold but remain below the 10-second matching tolerance. They are therefore retained as valid causal matches while remaining identifiable for sensitivity analysis. Rows classified as tolerance-exceeded are not represented in the lower box plots because those plots contain only valid matches.

The figure confirms that ambient-temperature alignment is predominantly successful and strictly causal. Most accepted matches are temporally close to the corresponding battery observations, and no future environmental measurements are introduced.



#### LPV-Identification Scheduling-Space Density

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









# Notebook 11

## Introduction

Notebook 11 constructs and audits fixed-parameter equivalent-circuit battery models using experimentally measured current, terminal voltage, temperature, elapsed time, chemistry identity, cell identity, and trajectory identity.

The implementation begins with an exact trajectory audit and chemistry-specific open-circuit-voltage preparation. It then reconstructs SOC using capacity and trapezoidal coulomb counting. Only trajectories with a directly reliable and charge-balance-consistent initial SOC are admitted to model fitting.

Two equivalent-circuit structures are estimated:

- a fixed one-RC model;
- a fixed two-RC model.

Each structure is estimated at four parameter scopes:

- one global parameter vector shared by LFP, NCA, and NMC;
- one LFP-specific parameter vector;
- one NCA-specific parameter vector;
- one NMC-specific parameter vector.

The models are fitted only on training trajectories. Calibration trajectories determine the best optimizer start and the automatic model-complexity decision. Ordinary-test and strict-test trajectories remain excluded until parameters have been frozen.

The code then performs:

- full recursive free-run prediction;
- pooled and trajectory-level error analysis;
- residual dependence analysis;
- numerical practical-identifiability analysis;
- exact objective slicing;
- trajectory-block bootstrap analysis;
- final acceptance or rejection.

> **Principal scientific question**
>
> Can one constant parameter vector, either globally or within a chemistry, provide accurate, stable, physically valid, and identifiable voltage predictions across the complete operating data?

---

## Objectives

The executable workflow has the following objectives.

### 3.1 Data-Readiness Objective

Construct an authoritative trajectory universe in which:

- sample records are correctly assigned to trajectories;
- sample times are finite and strictly increasing;
- voltage, current, and temperature are finite;
- chemistry identities are valid;
- capacities are finite and positive;
- chemistry-specific OCV functions are available.

### 3.2 State-Reconstruction Objective

Reconstruct SOC without using held-out test information and determine whether every trajectory has an initial SOC that is simultaneously:

- supported by the available initial evidence;
- consistent with the integrated current profile;
- inside the validated chemistry-specific OCV support.

### 3.3 Identification Objective

Estimate physically positive fixed ECM parameters using a bounded robust nonlinear least-squares formulation.

### 3.4 Validation Objective

Evaluate the frozen models on ordinary-test and strict-test trajectories using recursive free-run predictions.

### 3.5 Reliability Objective

Determine whether the estimated parameters are:

- locally distinguishable;
- weakly or strongly correlated;
- supported by a sufficiently curved objective;
- stable under resampling of complete training trajectories.

### 3.6 Decision Objective

Classify each frozen model as:

- `ACCEPT`;
- `ACCEPT_WITH_CAUTION`;
- `REJECT`.

---

## Data Hierarchy and Notation

Let

```math
s=1,\ldots,S
```

index trajectories or experimental segments.

Within trajectory `s`, let

```math
k=0,\ldots,N_s-1
```

index samples.

The code uses:

- `t_{s,k}` for elapsed time in seconds;
- `V_{s,k}` for measured terminal voltage;
- `I_{s,k}` for current;
- `T_{s,k}` for cell temperature;
- `z_{s,k}` for reconstructed SOC.

The sampling interval is

```math
\Delta t_{s,k}=t_{s,k+1}-t_{s,k},
\qquad
k=0,\ldots,N_s-2.
```

**Equation (1)**

The code requires

```math
\Delta t_{s,k}>0.
```

**Equation (2)**

The current convention is explicitly fixed as

```math
I_{s,k}>0
\iff
\mathrm{discharge}.
```

**Equation (3)**

Thus, positive current reduces SOC.

Every trajectory also has:

- chemistry `c(s)` belonging to LFP, NCA, or NMC;
- cell identity;
- file identity;
- segment index;
- primary split;
- strict-test status;
- SOC-fit-eligibility status.

---

## Data Partitions and Leakage Prevention

Let the primary split be

```math
p(s)\in
\{
\mathrm{train},
\mathrm{calibration},
\mathrm{test}
\}.
```

**Equation (4)**

Let

```math
q_s^{\mathrm{strict}}\in\{0,1\}
```

indicate strict-test membership.

The evaluation-partition label is defined as follows:

| Condition | Evaluation-partition label |
|---|---|
| `q_s^{strict}=1` | `strict_test` |
| `q_s^{strict}=0` | `p(s)` |

**Equation (5)**

A fitting trajectory must satisfy all of the following:

```math
p(s)\in
\{
\mathrm{train},
\mathrm{calibration}
\}.
```

**Equation (6)**

```math
q_s^{\mathrm{strict}}=0.
```

**Equation (7)**

```math
e_s^{\mathrm{SOC}}=1.
```

**Equation (8)**

Here, `e_s^{SOC}` denotes SOC-fit eligibility.

Training and calibration trajectory UIDs are explicitly checked to be disjoint.

No strict-test trajectory is permitted in either fitting dataset.

---

## 7. Executed Data Volume

The executed notebook reports:

| Quantity | Count |
|---|---:|
| Total trajectories reconstructed and evaluated | 4,938 |
| Total sample rows in the full prediction artifact | 18,318,873 |
| SOC-fit-eligible trajectories | 4,077 |
| Evaluation-only trajectories | 861 |
| Selected training trajectories | 750 |
| Selected calibration trajectories | 300 |

The selected optimization datasets are:

| Scope | Training trajectories | Training samples | Training fit residuals | Calibration trajectories | Calibration samples | Calibration fit residuals |
|---|---:|---:|---:|---:|---:|---:|
| Global | 750 | 3,229,830 | 470,635 | 300 | 986,023 | 206,795 |
| LFP | 250 | 711,809 | 173,718 | 100 | 282,029 | 68,718 |
| NCA | 250 | 1,418,388 | 144,232 | 100 | 420,936 | 68,077 |
| NMC | 250 | 1,099,633 | 152,685 | 100 | 283,058 | 70,000 |

The global dataset is the concatenation of the three chemistry-specific selections.

---

## Chemistry-Specific OCV Representation

For chemistry `c`, the code stores a validated forward OCV grid:

```math
\{z_j^{(c)},U_j^{(c)}\}_{j=1}^{M_c}.
```

The forward OCV calculation is implemented by linear interpolation:

```math
U_{\mathrm{oc}}^{(c)}(z)
=
\mathrm{interp}
\bigl(
z;
z_{\mathrm{grid}}^{(c)},
U_{\mathrm{grid}}^{(c)}
\bigr).
```

**Equation (9)**

Before interpolation, SOC is clipped to the validated support:

```math
z_{\mathrm{OCV}}
=
\mathrm{clip}
\bigl(
z,
z_{\min}^{(c)},
z_{\max}^{(c)}
\bigr).
```

**Equation (10)**

The inverse OCV calculation is also linear interpolation:

```math
z_{\mathrm{inv}}^{(c)}(V)
=
\mathrm{interp}
\bigl(
V;
U_{\mathrm{inv}}^{(c)},
z_{\mathrm{inv}}^{(c)}
\bigr).
```

**Equation (11)**

Voltage is clipped to the validated inverse support before inversion.

The code does not fit a new OCV polynomial inside the ECM optimizer. OCV is prevalidated, reconstructed, and supplied as a fixed sample-level input.

---

## Initial-SOC Determination

The code uses a hierarchy of initial-SOC evidence.

### 8.1 Published Initial SOC

When a finite published initial SOC exists and satisfies

```math
-0.02
\le
z_{s,0}^{\mathrm{published}}
\le
1.02,
```

**Equation (12)**

it is used as a directly reliable point anchor.

### 8.2 Initial-Rest OCV Inversion

The initial window contains the first five samples:

```math
N_{\mathrm{rest}}=5.
```

A sample is considered at rest when

```math
|I_{s,k}|
\le
0.05\ \mathrm{A}.
```

**Equation (13)**

An initial-rest condition is detected only when all five required initial samples satisfy the rest threshold.

The initial-rest voltage is

```math
V_{s,0}^{\mathrm{rest}}
=
\mathrm{median}
\bigl(
V_{s,0},
\ldots,
V_{s,4}
\bigr).
```

**Equation (14)**

The chemistry-specific inverse OCV function converts this voltage to a representative SOC.

---

## Plateau-Equivalent SOC Interval

For flat or nearly flat OCV regions, the code does not assume that one voltage uniquely determines one SOC.

Let `V*` be the nearest OCV-grid voltage to the clipped initial voltage.

Define

```math
P_s
=
\{
j:
U_j^{(c)}-V^\star
\le
\varepsilon_{\mathrm{OCV}}
\}.
```

**Equation (15)**

The implemented tolerance is

```math
\varepsilon_{\mathrm{OCV}}
=
\max
\bigl(
10^{-8},
10\varepsilon_{\mathrm{mon}}
\bigr).
```

**Equation (16)**

The default monotonicity tolerance is

```math
10^{-9}\ \mathrm{V}.
```

If at least two grid points satisfy Equation (15), the equivalent initial-SOC interval is

```math
Z_s^{\mathrm{OCV}}
=
\bigl[
\min_{j\in P_s}z_j^{(c)},
\max_{j\in P_s}z_j^{(c)}
\bigr].
```

**Equation (17)**

Otherwise, the interval collapses to the representative inverse-OCV value.

---

## Nonrest Initial Terminal Voltage

When the first five samples do not satisfy the rest condition, the first terminal voltage is inverted provisionally:

```math
z_{s,0}^{\mathrm{provisional}}
=
z_{\mathrm{inv}}^{(c)}
\bigl(
V_{s,0}
\bigr).
```

**Equation (18)**

The code explicitly marks this anchor as not directly reliable. Such a trajectory may be reconstructed for evaluation but is not admitted to parameter fitting.

---

## Trapezoidal Coulomb Counting

The code uses a coulombic efficiency of

```math
\eta=1.
```

**Equation (19)**

For interval `k`, signed charge throughput in ampere-hours is

```math
\Delta q_{s,k}^{\mathrm{signed}}
=
\frac{
\Delta t_{s,k}
\bigl(
I_{s,k}+I_{s,k+1}
\bigr)
}{
7200
}.
```

**Equation (20)**

The denominator is

```math
7200=2\times3600
```

because the implementation combines:

- trapezoidal averaging, giving the factor `1/2`;
- conversion from ampere-seconds to ampere-hours, giving `1/3600`.

The absolute-throughput increment is

```math
\Delta q_{s,k}^{\mathrm{abs}}
=
\frac{
\Delta t_{s,k}
\bigl(
|I_{s,k}|+|I_{s,k+1}|
\bigr)
}{
7200
}.
```

**Equation (21)**

Cumulative signed charge is

```math
q_{s,k}^{\mathrm{signed}}
=
\sum_{\ell=0}^{k-1}
\Delta q_{s,\ell}^{\mathrm{signed}},
\qquad
q_{s,0}^{\mathrm{signed}}=0.
```

**Equation (22)**

For a positive trajectory capacity `Q_s`, the cumulative SOC drop is

```math
d_{s,k}
=
\frac{
\eta q_{s,k}^{\mathrm{signed}}
}{
Q_s
}.
```

**Equation (23)**

Raw reconstructed SOC is

```math
z_{s,k}^{\mathrm{raw}}
=
z_{s,0}-d_{s,k}.
```

**Equation (24)**

The code also produces a bounded display variable:

```math
z_{s,k}^{\mathrm{bounded}}
=
\mathrm{clip}
\bigl(
z_{s,k}^{\mathrm{raw}},
0,
1
\bigr).
```

**Equation (25)**

However, the OCV input is not necessarily Equation (25). It is instead clipped to the chemistry-specific OCV support:

```math
z_{s,k}^{\mathrm{OCV}}
=
\mathrm{clip}
\bigl(
z_{s,k}^{\mathrm{raw}},
z_{\min}^{(c)},
z_{\max}^{(c)}
\bigr).
```

**Equation (26)**

---

## Charge-Balance-Consistent Initial-SOC Interval

Because

```math
z_{s,k}^{\mathrm{raw}}
=
z_{s,0}-d_{s,k},
```

the requirement that all reconstructed SOC values remain inside the chemistry-specific OCV support is

```math
z_{\min}^{(c)}
\le
z_{s,0}-d_{s,k}
\le
z_{\max}^{(c)}.
```

**Equation (27)**

Therefore, the initial SOC must satisfy

```math
z_{s,0}
\ge
z_{\min}^{(c)}
+
\max_k d_{s,k},
```

**Equation (28)**

and

```math
z_{s,0}
\le
z_{\max}^{(c)}
+
\min_k d_{s,k}.
```

**Equation (29)**

The current-profile-feasible interval is therefore

```math
Z_s^F
=
\bigl[
z_{\min}^{(c)}+\max_k d_{s,k},
z_{\max}^{(c)}+\min_k d_{s,k}
\bigr].
```

**Equation (30)**

A feasible interval exists when

```math
\underline{z}_s^F
\le
\overline{z}_s^F
+
10^{-10}.
```

**Equation (31)**

The code intersects the OCV-supported initial interval and the charge-balance interval:

```math
Z_s^I
=
Z_s^{\mathrm{OCV}}
\cap
Z_s^F.
```

**Equation (32)**

If the anchor is directly reliable and the intersection is nonempty, the selected initial SOC is

```math
z_{s,0}
=
\mathrm{clip}
\bigl(
z_{s,0}^{\mathrm{rep}},
\underline{z}_s^I,
\overline{z}_s^I
\bigr).
```

**Equation (33)**

The trajectory is fit eligible only when:

- the initial anchor is directly reliable;
- the OCV and charge-balance intervals overlap;
- no raw SOC sample violates the audit interval;
- no sample requires OCV-support clipping.

The code reports:

- 4,077 fit-eligible trajectories;
- 861 evaluation-only trajectories.

---

## Deterministic Training and Calibration Selection

The code does not fit every eligible training trajectory. It constructs a representative and computationally manageable subset.

For trajectory `s`, the excitation score is

```math
E_s
=
\log
\bigl(
1+Q_{s,\mathrm{abs}}
\bigr)
+
\log
\bigl(
1+\sigma_{I,s}
\bigr)
+
3\Delta z_s
+
0.05\Delta T_s
+
0.10\log
\bigl(
1+D_s
\bigr).
```

**Equation (34)**

Here:

- `Q_{s,abs}` is absolute ampere-hour throughput;
- `σ_{I,s}` is current standard deviation;
- `Δz_s` is reconstructed SOC span;
- `ΔT_s` is temperature span;
- `D_s` is duration.

For each chemistry, the code selects at most:

- 250 training trajectories;
- 100 calibration trajectories.

Approximately 70% of each selection is taken from the highest excitation scores:

```math
n_{\mathrm{high}}
=
\min
\Bigl[
n_{\mathrm{target}},
\max
\bigl(
1,
\mathrm{round}
(
0.70n_{\mathrm{target}}
)
\bigr)
\Bigr].
```

**Equation (35)**

The remaining 30% is selected across five excitation-percentile strata to retain broader operating coverage.

The executed selection gives, for each chemistry:

```math
175+75=250
```

training trajectories and

```math
70+30=100
```

calibration trajectories.

---

## Fitting Residual Subsampling

For a trajectory with `N_s` samples, sample zero is excluded from fitting because it is used for polarization-state initialization.

The available residual count is

```math
N_s-1.
```

**Equation (36)**

The number retained for fitting is

```math
M_s
=
\min
\bigl(
N_s-1,
700
\bigr).
```

**Equation (37)**

The code creates approximately evenly spaced integer indices:

```math
K_s
=
\mathrm{unique}
\Bigl[
\mathrm{linspace}
\bigl(
1,
N_s-1,
M_s
\bigr)
\Bigr].
```

**Equation (38)**

Thus, the optimization does not simply use the first 700 observations. It distributes fitting residuals across the entire trajectory.

---

## Trajectory and Chemistry Weighting

A trajectory with

```math
m_s=|K_s|
```

fitting residuals receives a trajectory weight

```math
w_s^{\mathrm{traj}}
=
\frac{1}{m_s}.
```

**Equation (39)**

If chemistry `c` contributes `n_c` selected trajectories, it receives chemistry weight

```math
w_c^{\mathrm{chem}}
=
\frac{1}{n_c}.
```

**Equation (40)**

The preliminary weight assigned to every selected residual of trajectory `s` is

```math
w_{s,k}
=
w_s^{\mathrm{traj}}
w_{c(s)}^{\mathrm{chem}}.
```

**Equation (41)**

Let `M` be the total number of selected fitting residuals. Define the mean preliminary weight as

```math
\bar{w}
=
\frac{1}{M}
\sum_{j=1}^{M}
w_j.
```

The normalized residual weight is

```math
w_{s,k}
\leftarrow
\frac{
w_{s,k}
}{
\bar{w}
}.
```

**Equation (42)**

This implementation reduces domination by:

- long trajectories;
- chemistries with more selected trajectories.

---

## Fixed One-RC Model

The code implements the terminal-voltage equation

```math
V_{s,k}
=
U_{s,k}
-
R_0I_{s,k}
-
v_{1,s,k}.
```

**Equation (43)**

where

```math
U_{s,k}
=
U_{\mathrm{oc}}^{(c(s))}
\bigl(
z_{s,k}^{\mathrm{OCV}}
\bigr).
```

For interval `k`, define

```math
a_{1,s,k}
=
\exp
\biggl(
-\frac{
\Delta t_{s,k}
}{
\tau_1
}
\biggr).
```

**Equation (44)**

The exact recursive update in the code is

```math
v_{1,s,k+1}
=
a_{1,s,k}v_{1,s,k}
+
R_1
\bigl(
1-a_{1,s,k}
\bigr)
I_{s,k}.
```

**Equation (45)**

After propagating Equation (45), the next voltage is evaluated using the next-sample current:

```math
V_{s,k+1}
=
U_{s,k+1}
-
R_0I_{s,k+1}
-
v_{1,s,k+1}.
```

**Equation (46)**

The parameters `R_0`, `R_1`, and `τ_1` are constant over every sample in the assigned scope.

---

## Fixed Two-RC Model

The two-RC terminal-voltage equation is

```math
V_{s,k}
=
U_{s,k}
-
R_0I_{s,k}
-
v_{1,s,k}
-
v_{2,s,k}.
```

**Equation (47)**

Define

```math
a_{1,s,k}
=
\exp
\biggl(
-\frac{
\Delta t_{s,k}
}{
\tau_1
}
\biggr),
```

**Equation (48)**

and

```math
a_{2,s,k}
=
\exp
\biggl(
-\frac{
\Delta t_{s,k}
}{
\tau_2
}
\biggr).
```

**Equation (49)**

The implemented recursions are

```math
v_{1,s,k+1}
=
a_{1,s,k}v_{1,s,k}
+
R_1
\bigl(
1-a_{1,s,k}
\bigr)
I_{s,k},
```

**Equation (50)**

and

```math
v_{2,s,k+1}
=
a_{2,s,k}v_{2,s,k}
+
R_2
\bigl(
1-a_{2,s,k}
\bigr)
I_{s,k}.
```

**Equation (51)**

The next-sample prediction is

```math
V_{s,k+1}
=
U_{s,k+1}
-
R_0I_{s,k+1}
-
v_{1,s,k+1}
-
v_{2,s,k+1}.
```

**Equation (52)**

No SOC, current, temperature, elapsed-time, or trajectory dependence is introduced into `R_0`, `R_1`, `R_2`, `τ_1`, or `τ_2`.

They remain fixed within the scope.

---

## Polarization-State Initialization

The simulator uses the first measured terminal voltage only to initialize the internal polarization state.

It does not reset the state at later samples.

### 16.1 One-RC Initialization

The code defines

```math
v_{1,s,0}
=
U_{s,0}
-
R_0I_{s,0}
-
V_{s,0}.
```

**Equation (53)**

Substitution into Equation (43) gives

```math
V_{s,0}=V_{s,0}.
```

**Equation (54)**

Thus, the initial prediction residual is forced to zero up to floating-point precision.

### 16.2 Two-RC Initialization

First define total initial polarization:

```math
v_{\Sigma,s,0}
=
U_{s,0}
-
R_0I_{s,0}
-
V_{s,0}.
```

**Equation (55)**

The code divides this value according to the branch resistances:

```math
v_{1,s,0}
=
\frac{
R_1
}{
R_1+R_2
}
v_{\Sigma,s,0},
```

**Equation (56)**

and

```math
v_{2,s,0}
=
\frac{
R_2
}{
R_1+R_2
}
v_{\Sigma,s,0}.
```

**Equation (57)**

Therefore,

```math
v_{1,s,0}
+
v_{2,s,0}
=
v_{\Sigma,s,0},
```

and

```math
V_{s,0}=V_{s,0}.
```

**Equation (58)**

The first sample is excluded from fitting and formal free-run evaluation.

The evaluation set for trajectory `s` is therefore

```math
E_s
=
\{
1,\ldots,N_s-1
\}.
```

**Equation (59)**

---

## Parameter Transformations

The optimizer operates in logarithmic coordinates.

### 17.1 One-RC Parameter Vector

The transformed vector is

```math
\xi_1
=
\bigl(
\log R_0,
\log R_1,
\log\tau_1
\bigr)^T.
```

**Equation (60)**

The decoded parameters are

```math
R_0=e^{\xi_1},
\qquad
R_1=e^{\xi_2},
\qquad
\tau_1=e^{\xi_3}.
```

**Equation (61)**

The derived capacitance is

```math
C_1
=
\frac{
\tau_1
}{
R_1
}.
```

**Equation (62)**

### 17.2 Two-RC Parameter Vector

The transformed vector is

```math
\xi_2
=
\bigl(
\log R_0,
\log R_1,
\log R_2,
\log\tau_1,
\log\tau_{\mathrm{gap}}
\bigr)^T.
```

**Equation (63)**

The physical parameters are

```math
R_0=e^{\xi_1},
\qquad
R_1=e^{\xi_2},
\qquad
R_2=e^{\xi_3},
```

**Equation (64)**

```math
\tau_1=e^{\xi_4},
```

**Equation (65)**

```math
\tau_{\mathrm{gap}}=e^{\xi_5},
```

**Equation (66)**

and

```math
\tau_2
=
\tau_1+\tau_{\mathrm{gap}}.
```

**Equation (67)**

The capacitances are

```math
C_1
=
\frac{
\tau_1
}{
R_1
},
```

**Equation (68)**

and

```math
C_2
=
\frac{
\tau_2
}{
R_2
}.
```

**Equation (69)**

Because

```math
\tau_{\mathrm{gap}}>0,
```

the code guarantees

```math
\tau_2>\tau_1.
```

**Equation (70)**

---

## Candidate Scopes

The code estimates fixed models for

```math
q
\in
\{
\mathrm{GLOBAL},
\mathrm{LFP},
\mathrm{NCA},
\mathrm{NMC}
\}.
```

**Equation (75)**

For the global candidate,

```math
\xi_s
=
\xi_{\mathrm{GLOBAL}}
```

for all chemistries.

For a chemistry-specific candidate,

```math
\xi_s
=
\xi_{c(s)}.
```

**Equation (76)**

The eight fitted candidate families are:

- `GLOBAL 1RC`;
- `GLOBAL 2RC`;
- `LFP 1RC`;
- `LFP 2RC`;
- `NCA 1RC`;
- `NCA 2RC`;
- `NMC 1RC`;
- `NMC 2RC`.

**Equation (77)**

---

## Voltage Residual and Robust Objective

The signed residual is

```math
e_{s,k}
=
V_{s,k}
-
\widehat{V}_{s,k}.
```

**Equation (78)**

Thus:

- `e_{s,k}>0`: predicted voltage is too low;
- `e_{s,k}<0`: predicted voltage is too high.

The weighted fitting residual is

```math
r_{s,k}
=
w_{s,k}e_{s,k}.
```

**Equation (79)**

The code uses a Huber scale of

```math
\delta=0.020\ \mathrm{V}.
```

**Equation (80)**

For residual magnitudes not exceeding the Huber scale:

```math
\ell_\delta(r)
=
\frac{1}{2}r^2,
\qquad
|r|\le\delta.
```

For residual magnitudes exceeding the Huber scale:

```math
\ell_\delta(r)
=
\delta|r|
-
\frac{1}{2}\delta^2,
\qquad
|r|>\delta.
```

**Equation (81)**

For scope `q` and model order `m`, define the objective

```math
J_{q,m}(\xi)
=
\sum_{s\in S_{\mathrm{train},q}}
\sum_{k\in K_s}
\ell_{0.020}
\Bigl(
w_{s,k}
[
V_{s,k}
-
\widehat{V}_{s,k}(\xi)
]
\Bigr).
```

The estimated parameter vector is the bounded minimizer:

```math
\widehat{\xi}_{q,m}
=
\underset{
\underline{\xi}_m
\le
\xi
\le
\overline{\xi}_m
}{
\arg\min
}
J_{q,m}(\xi).
```

**Equation (82)**

---

## Numerical Optimizer

The actual parameter-fitting cell uses:

| Setting | Implemented value |
|---|---|
| Optimizer | `scipy.optimize.least_squares` |
| Method | Trust-region reflective, `trf` |
| Jacobian | Two-point finite difference |
| Loss | Huber |
| Huber scale | 0.020 V |
| Parameter scaling | `x_scale="jac"` |
| Maximum function evaluations | 400 |
| `ftol` | 10⁻⁸ |
| `xtol` | 10⁻⁸ |
| `gtol` | 10⁻⁸ |
| Starts per scope/order | 8 |

A candidate is retained as valid when:

- decoded parameters satisfy physical validity;
- fitted transformed parameters are finite;
- optimizer cost is finite;
- training metrics are finite;
- calibration metrics are finite.

The `optimizer_success` flag is stored, but a solution can still be considered a finite valid candidate when the other required conditions are satisfied.

---

## Multi-Start Initialization

For the one-RC model, the nominal initial point is

```math
R_0=0.015\ \Omega,
\qquad
R_1=0.010\ \Omega,
\qquad
\tau_1=20\ \mathrm{s}.
```

**Equation (83)**

For the two-RC model, the nominal point is

```math
R_0=0.015\ \Omega,
\qquad
R_1=0.008\ \Omega,
\qquad
R_2=0.015\ \Omega,
\qquad
\tau_1=5\ \mathrm{s},
\qquad
\tau_2=105\ \mathrm{s}.
```

**Equation (84)**

This implies an initial gap of

```math
\tau_{\mathrm{gap}}=100\ \mathrm{s}.
```

The remaining starts are sampled uniformly in transformed log-parameter space between the transformed bounds.

The random seed is inherited from Notebook 10:

`RANDOM_SEED = 42`

**Equation (85)**

The executed model fitting comprises 64 starts.

---

## Selection of the Best Optimizer Start

Within each scope and model order, valid starts are sorted in the following exact order:

1. calibration trajectory-weighted RMSE;
2. calibration pooled RMSE;
3. training trajectory-weighted RMSE;
4. training pooled RMSE;
5. optimizer cost;
6. start index.

For trajectory `s`, free-run RMSE is

```math
\mathrm{RMSE}_s
=
\sqrt{
\frac{1}{N_s-1}
\sum_{k=1}^{N_s-1}
e_{s,k}^2
}.
```

**Equation (86)**

The trajectory-weighted RMSE is

```math
\mathrm{RMSE}_{\mathrm{traj}}
=
\frac{1}{S}
\sum_{s=1}^{S}
\mathrm{RMSE}_s.
```

**Equation (87)**

Every trajectory receives equal weight in Equation (87), regardless of its sample count.

---

## Calibration-Stage Model Selection

For reference model `A` and candidate model `B`, relative calibration improvement is

```math
I_{A\rightarrow B}
=
\frac{
\mathrm{RMSE}_A^{\mathrm{traj}}
-
\mathrm{RMSE}_B^{\mathrm{traj}}
}{
\mathrm{RMSE}_A^{\mathrm{traj}}
}.
```

**Equation (88)**

The code uses a minimum improvement of

```math
0.01.
```

**Equation (89)**

A global two-RC model replaces the global one-RC model only if

```math
I_{\mathrm{global\ 1RC}\rightarrow\mathrm{global\ 2RC}}
\ge
0.01.
```

**Equation (90)**

A chemistry-specific two-RC model replaces the chemistry-specific one-RC model only if

```math
I_{\mathrm{specific\ 1RC}\rightarrow\mathrm{specific\ 2RC}}
\ge
0.01.
```

**Equation (91)**

The selected chemistry-specific model replaces the selected global model only if

```math
I_{\mathrm{selected\ global}\rightarrow\mathrm{selected\ chemistry}}
\ge
0.01.
```

**Equation (92)**

This produces an automatic parsimonious candidate for each chemistry.

Separately, the code preserves the chemistry-specific two-RC model as the primary fixed baseline:

```math
M_{\mathrm{primary}}^{(c)}
=
M_{\mathrm{specific,2RC}}^{(c)}.
```

**Equation (93)**

All candidate parameters are frozen before ordinary-test and strict-test evaluation.

---

## Full Recursive Free-Run Evaluation

The full evaluation is performed on:

- 4,938 trajectories;
- 18,318,873 sample rows.

For every trajectory:

- the first measured voltage initializes polarization;
- the ECM is recursively propagated without later measurement correction;
- sample zero is marked as nonevaluated;
- samples 1 through `N_s-1` are used for reported prediction metrics.

The code saves predictions for:

- OCV-only;
- global one-RC;
- global two-RC;
- chemistry-specific one-RC;
- chemistry-specific two-RC;
- automatically selected model;
- primary fixed baseline.

---

## Prediction Metrics

Let `N` be the number of evaluated samples in a group.

### 26.1 Bias

```math
\mathrm{Bias}
=
\frac{1}{N}
\sum_{i=1}^{N}
e_i.
```

**Equation (94)**

### 26.2 Root-Mean-Square Error

```math
\mathrm{RMSE}
=
\sqrt{
\frac{1}{N}
\sum_{i=1}^{N}
e_i^2
}.
```

**Equation (95)**

### 26.3 Mean Absolute Error

```math
\mathrm{MAE}
=
\frac{1}{N}
\sum_{i=1}^{N}
|e_i|.
```

**Equation (96)**

### 26.4 Residual Standard Deviation

The code uses the population standard deviation:

```math
\sigma_e
=
\sqrt{
\frac{1}{N}
\sum_{i=1}^{N}
(e_i-\bar{e})^2
}.
```

**Equation (97)**

### 26.5 Median and Upper-Tail Absolute Errors

```math
\mathrm{MedAE}
=
\mathrm{median}
\bigl(
|e_i|
\bigr).
```

**Equation (98)**

```math
P_{95}
=
q_{0.95}
\bigl(
|e_i|
\bigr).
```

**Equation (99)**

```math
P_{99}
=
q_{0.99}
\bigl(
|e_i|
\bigr).
```

**Equation (100)**

```math
E_{\max}
=
\max_i
|e_i|.
```

**Equation (101)**

### 26.6 Normalized RMSE

Let

```math
\Delta V
=
V_{\max}-V_{\min}.
```

The implemented normalized RMSE is

```math
\mathrm{NRMSE}
=
\frac{
\mathrm{RMSE}
}{
\Delta V
}.
```

**Equation (102)**

This metric is defined when

```math
\Delta V>0.
```

The code does not compute `R²` in the fixed-ECM metric function.

### 26.7 Lag-One Residual Autocorrelation

Let

```math
\widetilde{e}_i
=
e_i-\bar{e}.
```

The implemented lag-one statistic is

```math
\rho_1
=
\frac{
\displaystyle
\sum_{i=1}^{N-1}
\widetilde{e}_{i-1}
\widetilde{e}_i
}{
\displaystyle
\sum_{i=0}^{N-1}
\widetilde{e}_i^2
}.
```

**Equation (103)**

---

## 27. Residual Operating-Regime Analysis

The code classifies current into charging, rest, and discharging regimes.

| Current condition | Regime |
|---|---|
| `I < -0.05` | `CHARGE` |
| `|I| ≤ 0.05` | `REST` |
| `I > 0.05` | `DISCHARGE` |

**Equation (104)**

SOC is divided into:

- `z<0`;
- ten intervals of width 0.1;
- `z≥1`.

Temperature is divided into:

- below 0 °C;
- 0 °C to below 10 °C;
- 10 °C to below 20 °C;
- 20 °C to below 30 °C;
- 30 °C to below 40 °C;
- 40 °C and above.

Residual dependence is evaluated against:

- current `I`;
- SOC `z`;
- temperature `T`;
- elapsed time `t`.

---

## 28. Correlation and Slope Calculation

For operating variable `x_i`, the code accumulates sufficient statistics.

Define

```math
S_{xx}
=
N\sum_i x_i^2
-
\biggl(
\sum_i x_i
\biggr)^2.
```

**Equation (105)**

Define

```math
S_{ee}
=
N\sum_i e_i^2
-
\biggl(
\sum_i e_i
\biggr)^2.
```

**Equation (106)**

Define

```math
S_{xe}
=
N\sum_i x_ie_i
-
\biggl(
\sum_i x_i
\biggr)
\biggl(
\sum_i e_i
\biggr).
```

**Equation (107)**

The residual slope is

```math
\beta_{e|x}
=
\frac{
S_{xe}
}{
S_{xx}
},
```

**Equation (108)**

when

```math
S_{xx}>0.
```

The Pearson correlation is

```math
\rho_{e,x}
=
\frac{
S_{xe}
}{
\sqrt{
S_{xx}S_{ee}
}
},
```

**Equation (109)**

when the denominator is positive.

The calculated correlation is clipped numerically to

```math
[-1,1].
```

The maximum residual dependence used in final decisions is

```math
\rho_{\max}
=
\max
\bigl(
|\rho_{e,I}|,
|\rho_{e,z}|,
|\rho_{e,T}|,
|\rho_{e,t}|
\bigr).
```

**Equation (110)**

---

## 29. Practical-Identifiability Analysis

Identifiability is evaluated using the weighted training residual vector:

```math
r(\xi).
```

The numerical Jacobian is evaluated at the frozen parameter estimate:

```math
J
=
\left[
\frac{
\partial r
}{
\partial\xi^T
}
\right]_{\xi=\widehat{\xi}}.
```

**Equation (111)**

For transformed parameter `ξ_j`, the proposed finite-difference step is

```math
h_j
=
\max
\bigl(
10^{-6},
10^{-4}
\max
(
1,
|\widehat{\xi}_j|
)
\bigr).
```

**Equation (112)**

When both sides are sufficiently far from the parameter bounds, the code uses the central-difference approximation:

```math
J_{:,j}
\approx
\frac{
r(\widehat{\xi}+h_je_j)
-
r(\widehat{\xi}-h_je_j)
}{
2h_j
}.
```

**Equation (113)**

Here, `e_j` is the unit vector associated with transformed parameter `j`.

The finite-difference step may be reduced to 45% of the available distance to either parameter bound.

Near a bound, the code uses a one-sided forward or backward difference.

Forward difference:

```math
J_{:,j}
\approx
\frac{
r(\widehat{\xi}+h_je_j)
-
r(\widehat{\xi})
}{
h_j
}.
```

Backward difference:

```math
J_{:,j}
\approx
\frac{
r(\widehat{\xi})
-
r(\widehat{\xi}-h_je_j)
}{
h_j
}.
```

---

## 30. Singular-Value and Rank Diagnostics

The code computes the singular-value decomposition:

```math
J
=
U\Sigma W^T.
```

**Equation (114)**

The singular-value matrix is

```math
\Sigma
=
\mathrm{diag}
\bigl(
\sigma_1,
\ldots,
\sigma_p
\bigr),
\qquad
\sigma_1
\ge
\cdots
\ge
\sigma_p.
```

The numerical-rank tolerance is

```math
\varepsilon_{\mathrm{num}}
=
\max
\bigl(
N,p
\bigr)
\varepsilon_{\mathrm{mach}}
\sigma_1.
```

**Equation (115)**

Here:

- `N` is the number of weighted training residuals;
- `p` is the number of transformed parameters;
- `ε_mach` is machine precision;
- `σ_1` is the largest singular value.

The practical singular-value tolerance is

```math
\varepsilon_{\mathrm{prac}}
=
10^{-6}\sigma_1.
```

**Equation (116)**

Practical rank is the number of singular values greater than the practical tolerance:

```math
r_{\mathrm{prac}}
=
\#
\{
j:
\sigma_j
>
\varepsilon_{\mathrm{prac}}
\}.
```

**Equation (117)**

The Jacobian condition number is

```math
\kappa_J
=
\frac{
\sigma_1
}{
\sigma_p
}.
```

**Equation (118)**

When the smallest singular value is zero or numerically unusable, the condition number is treated as nonfinite.

---

## 31. Local Covariance and Parameter Correlations

The local information matrix is

```math
I
=
J^TJ.
```

**Equation (119)**

The weighted residual sum of squares is

```math
\mathrm{RSS}
=
r^Tr.
```

**Equation (120)**

The residual degrees of freedom are

```math
\nu
=
N-r_{\mathrm{prac}}.
```

**Equation (121)**

The residual-variance estimate is

```math
\sigma_r^2
=
\frac{
\mathrm{RSS}
}{
\nu
}.
```

**Equation (122)**

The transformed-parameter covariance approximation is

```math
\Sigma_\xi
=
\sigma_r^2
\bigl(
J^TJ
\bigr)^+.
```

**Equation (123)**

The superscript `+` denotes the Moore-Penrose pseudoinverse.

The standard error of transformed parameter `ξ_j` is

```math
\mathrm{SE}
\bigl(
\xi_j
\bigr)
=
\sqrt{
[\Sigma_\xi]_{jj}
}.
```

**Equation (124)**

The transformed-parameter correlation is

```math
\mathrm{Corr}
\bigl(
\xi_i,
\xi_j
\bigr)
=
\frac{
[\Sigma_\xi]_{ij}
}{
\sqrt{
[\Sigma_\xi]_{ii}
[\Sigma_\xi]_{jj}
}
}.
```

**Equation (125)**

The maximum absolute off-diagonal transformed-parameter correlation is

```math
\rho_{\xi,\max}
=
\max_{i\ne j}
\left|
\mathrm{Corr}
\bigl(
\xi_i,
\xi_j
\bigr)
\right|.
```

---

## 32. Physical-Parameter Uncertainty

Let

```math
\vartheta
=
g(\xi)
```

be the decoded physical-parameter vector.

For the one-RC model:

```math
\vartheta_1
=
\bigl(
R_0,
R_1,
\tau_1,
C_1
\bigr)^T.
```

**Equation (126)**

For the two-RC model:

```math
\vartheta_2
=
\bigl(
R_0,
R_1,
R_2,
\tau_1,
\tau_2,
\tau_{\mathrm{gap}},
C_1,
C_2
\bigr)^T.
```

**Equation (127)**

Let `G` denote the Jacobian of the physical-parameter transformation:

```math
G
=
\frac{
\partial g
}{
\partial\xi^T
}.
```

**Equation (128)**

The physical-parameter covariance is computed using the delta method:

```math
\Sigma_\vartheta
=
G\Sigma_\xi G^T.
```

**Equation (129)**

The physical-parameter standard error is

```math
\mathrm{SE}
\bigl(
\vartheta_j
\bigr)
=
\sqrt{
[\Sigma_\vartheta]_{jj}
}.
```

The relative standard error is

```math
\mathrm{RSE}
\bigl(
\vartheta_j
\bigr)
=
\frac{
\sqrt{
[\Sigma_\vartheta]_{jj}
}
}{
|\vartheta_j|
}.
```

**Equation (130)**

The maximum physical relative standard error is

```math
\mathrm{RSE}_{\max}
=
\max_j
\mathrm{RSE}
\bigl(
\vartheta_j
\bigr).
```

---

## 33. Bound-Proximity Diagnostic

For transformed parameter `ξ_j` with lower bound `ℓ_j` and upper bound `u_j`, define the normalized distance from the lower bound as

```math
d_j^L
=
\frac{
\widehat{\xi}_j-\ell_j
}{
u_j-\ell_j
}.
```

**Equation (131)**

Define the normalized distance from the upper bound as

```math
d_j^U
=
\frac{
u_j-\widehat{\xi}_j
}{
u_j-\ell_j
}.
```

**Equation (132)**

The minimum relative distance to either bound is

```math
d_j^{\min}
=
\min
\bigl(
d_j^L,
d_j^U
\bigr).
```

**Equation (133)**

A parameter is considered near a bound when

```math
d_j^{\min}
\le
0.01.
```

**Equation (134)**

The code records the number and identities of transformed parameters satisfying this condition.

---

## 34. Identifiability Classification

A model is classified as `RANK_DEFICIENT` when

```math
r_{\mathrm{prac}}
<
p.
```

**Equation (135)**

For a practically full-rank model, severe weakness exists if any of the following conditions holds:

```math
\kappa_J
>
10^6,
```

**Equation (136)**

```math
\max_{i\ne j}
\left|
\mathrm{Corr}
\bigl(
\xi_i,
\xi_j
\bigr)
\right|
\ge
0.99,
```

**Equation (137)**

or

```math
\max_j
\mathrm{RSE}
\bigl(
\vartheta_j
\bigr)
\ge
1.
```

**Equation (138)**

The corresponding classification is:

`FULL_RANK_BUT_WEAK`

Moderate identifiability concern exists when any of the following conditions holds:

```math
\kappa_J
>
10^4,
```

**Equation (139)**

```math
\max_{i\ne j}
\left|
\mathrm{Corr}
\bigl(
\xi_i,
\xi_j
\bigr)
\right|
\ge
0.95,
```

**Equation (140)**

```math
\max_j
\mathrm{RSE}
\bigl(
\vartheta_j
\bigr)
\ge
0.50,
```

**Equation (141)**

or at least one transformed parameter satisfies

```math
d_j^{\min}
\le
0.01.
```

The corresponding classification is:

`FULL_RANK_MODERATE`

Otherwise, the model is classified as:

`FULL_RANK_STABLE`

---

## 35. Exact Objective Profiles

The code evaluates exact nonlinear objective slices using training residuals only.

The multiplier grid is

```math
m
\in
\{
-2,
-1.5,
-1,
-0.5,
0,
0.5,
1,
1.5,
2
\}.
```

**Equation (142)**

### 35.1 Parameter-Axis Direction

For transformed parameter `j`, the parameter-axis profile is

```math
\xi_j(m)
=
\widehat{\xi}
+
ms_je_j.
```

**Equation (143)**

Here:

- `ξ̂` is the frozen transformed-parameter estimate;
- `m` is the profile multiplier;
- `s_j` is the profile scale for parameter `j`;
- `e_j` is the unit vector for parameter `j`.

The profile scale is reduced when necessary so that all evaluated profile points remain inside the transformed parameter bounds.

### 35.2 Weakest Joint Direction

Let `v_min` be the right singular vector associated with the smallest singular value of the weighted residual Jacobian.

The code gives `v_min` a deterministic sign by requiring its component with the largest absolute magnitude to be positive.

The weakest-direction profile is

```math
\xi_w(m)
=
\widehat{\xi}
+
ms_wv_{\min}.
```

**Equation (144)**

The direction is normalized so that

```math
\|v_{\min}\|_2=1.
```

The scale `s_w` is reduced when necessary so that every weakest-direction profile point remains inside the transformed parameter bounds.

The parameter-axis and weakest-direction profiles are conditional objective slices. All transformed parameters not included in the selected direction remain fixed at their frozen values.

---

## 36. Exact and Linearized Profile Objectives

For perturbation

```math
\Delta\xi
=
msd,
```

**Equation (145)**

the exact weighted residual is

```math
r_{\mathrm{exact}}(m)
=
r
\bigl(
\widehat{\xi}
+
\Delta\xi
\bigr).
```

**Equation (146)**

The local linearized residual is

```math
r_{\mathrm{lin}}(m)
=
r_0
+
J\Delta\xi.
```

**Equation (147)**

The exact weighted residual sum of squares is

```math
\mathrm{RSS}_{\mathrm{exact}}(m)
=
r_{\mathrm{exact}}(m)^T
r_{\mathrm{exact}}(m).
```

**Equation (148)**

The exact Huber objective is

```math
H_{\mathrm{exact}}(m)
=
\sum_i
\ell_{0.020}
\bigl(
r_{\mathrm{exact},i}(m)
\bigr).
```

**Equation (149)**

The change in residual sum of squares is

```math
\Delta\mathrm{RSS}(m)
=
\mathrm{RSS}_{\mathrm{exact}}(m)
-
\mathrm{RSS}_0.
```

**Equation (150)**

The likelihood-ratio-style statistic is

```math
\Lambda(m)
=
\frac{
\Delta\mathrm{RSS}(m)
}{
\sigma_r^2
}.
```

**Equation (151)**

The relative change in the Huber objective is

```math
\Delta H_{\mathrm{rel}}(m)
=
\frac{
H_{\mathrm{exact}}(m)-H_0
}{
H_0
}.
```

**Equation (152)**

These are conditional slices. Other parameters remain fixed; the code does not reoptimize nuisance parameters at each profile point.

---

## 37. Objective-Profile Classification

A profile is classified `CENTER_NOT_SLICE_MINIMUM` when a noncentral point has a lower Huber objective than the frozen center beyond tolerance.

Otherwise, define

```math
\Lambda_{\mathrm{outer}}
=
\min_{|m|=2}
\Lambda(m).
```

**Equation (153)**

The profile is classified `VERY_FLAT` when

```math
\Lambda_{\mathrm{outer}}
<
0.25.
```

**Equation (154)**

The profile is classified `WEAK` when

```math
0.25
\le
\Lambda_{\mathrm{outer}}
<
1.
```

**Equation (155)**

The profile is classified `MODERATE` when

```math
1
\le
\Lambda_{\mathrm{outer}}
<
4.
```

**Equation (156)**

The profile is classified `SHARP` when

```math
\Lambda_{\mathrm{outer}}
\ge
4.
```

**Equation (157)**

The executed notebook evaluates:

- 32 parameter-axis directions;
- 288 parameter-axis profile rows;
- 72 weakest-direction profile rows.

---

## 38. Exact Trajectory-Block Bootstrap

The bootstrap operates only on training trajectories.

Let the base weighted residual vector be divided into trajectory blocks:

```math
r
=
\bigl(
r_1^T,
r_2^T,
\ldots,
r_S^T
\bigr)^T.
```

**Equation (158)**

For bootstrap replicate `b`, the code draws `S` trajectory indices with replacement:

```math
s_1^{(b)},
s_2^{(b)},
\ldots,
s_S^{(b)}.
```

**Equation (159)**

The bootstrap residual vector is formed by direct residual-block indexing:

```math
r^{(b)}(\xi)
=
\bigl(
r_{s_1^{(b)}}(\xi)^T,
r_{s_2^{(b)}}(\xi)^T,
\ldots,
r_{s_S^{(b)}}(\xi)^T
\bigr)^T.
```

**Equation (160)**

If a trajectory is sampled twice, its complete residual block appears twice.

This is an exact block-resampling implementation for the robust objective; it is not a sample-level independent bootstrap.

Each bootstrap estimate solves

```math
\widehat{\xi}^{(b)}
=
\underset{\xi}{\arg\min}
\sum_i
\ell_{0.020}
\bigl(
r_i^{(b)}(\xi)
\bigr).
```

**Equation (161)**

The frozen estimate initializes each bootstrap fit.

The full run uses:

- 30 replicates for each candidate;
- eight fitted candidates;
- 240 bootstrap refits.

---

## 39. Bootstrap Optimizer

The primary bootstrap optimization uses:

- trust-region reflective method, `trf`;
- two-point finite-difference Jacobian;
- Huber scale of 0.020 V;
- Jacobian-based parameter scaling;
- a maximum of 300 function evaluations;
- optimization tolerances of 10⁻⁸.

When the first attempt does not report success, the code performs a fallback fit using:

- the first estimate as the starting point when it is finite;
- three-point finite differences;
- unit parameter scaling;
- up to 600 function evaluations;
- tolerances no tighter than 10⁻⁷.

A finite, physically valid result can be retained as usable even when the optimizer success flag is false.

Usability and formal convergence are reported separately.

---

## 40. Bootstrap Statistics

For parameter `θ_j`, using `B_u` usable bootstrap replicates, the bootstrap mean is

```math
\theta_j^*
=
\frac{1}{B_u}
\sum_{b=1}^{B_u}
\theta_j^{(b)}.
```

**Equation (162)**

Bootstrap bias is

```math
\mathrm{Bias}_j^*
=
\theta_j^*
-
\theta_j.
```

**Equation (163)**

Relative bootstrap bias is

```math
\mathrm{RBias}_j^*
=
\frac{
\mathrm{Bias}_j^*
}{
|\theta_j|
}.
```

**Equation (164)**

Bootstrap standard deviation is

```math
s_j^*
=
\sqrt{
\frac{1}{B_u-1}
\sum_{b=1}^{B_u}
\bigl(
\theta_j^{(b)}
-
\theta_j^*
\bigr)^2
}.
```

**Equation (165)**

Relative bootstrap standard deviation is

```math
\mathrm{RSD}_j^*
=
\frac{
s_j^*
}{
|\theta_j|
}.
```

**Equation (166)**

The percentile interval is

```math
\Bigl[
q_{0.025}
\bigl(
\theta_j^{(b)}
\bigr),
q_{0.975}
\bigl(
\theta_j^{(b)}
\bigr)
\Bigr].
```

**Equation (167)**

Near-bound frequency is

```math
f_{j,\mathrm{bound}}^*
=
\frac{1}{B_u}
\sum_{b=1}^{B_u}
\mathbf{1}
\bigl[
d_{j,b}^{\min}
\le
0.01
\bigr].
```

**Equation (168)**

---

## 41. Bootstrap Stability Classification

The minimum usable fraction is

```math
f_{\mathrm{usable}}
\ge
0.80.
```

**Equation (169)**

The minimum converged fraction is

```math
f_{\mathrm{conv}}
\ge
0.50.
```

**Equation (170)**

A candidate is classified `STABLE` when

```math
\max_j
\mathrm{RSD}_j^*
\le
0.20,
```

**Equation (171)**

and

```math
\max_j
f_{j,\mathrm{bound}}^*
\le
0.20.
```

**Equation (172)**

A candidate is classified `MODERATE` when

```math
\max_j
\mathrm{RSD}_j^*
\le
0.50,
```

**Equation (173)**

and the maximum near-bound frequency remains at most 0.20.

Otherwise, the candidate is classified `WEAK`.

---

## 42. Final Acceptance Thresholds

The exact final thresholds are:

| Diagnostic | Warning | Rejection or severe level |
|---|---:|---:|
| Ordinary-test pooled RMSE | 0.030 V | 0.050 V |
| Strict-test pooled RMSE | 0.050 V | 0.075 V |
| Absolute pooled bias | 0.010 V | 0.020 V |
| Maximum residual correlation | 0.25 | 0.50, severe warning |
| Transformed-parameter correlation | 0.95 | — |
| Physical relative standard error | 0.50 | 1.00, severe warning |
| Bootstrap usable fraction | — | below 0.80, hard failure |
| Bootstrap converged fraction | below 0.50 | warning |
| Bootstrap relative standard deviation | 0.50 | 1.00, severe warning |

Residual correlation above 0.50 is treated as a severe warning, not as an independent hard failure.

---

## 43. Hard-Failure Logic

A hard failure is generated when any of the following occurs:

- frozen parameters violate physical constraints;
- ordinary-test samples are absent;
- ordinary-test RMSE exceeds 0.050 V;
- ordinary-test absolute bias exceeds 0.020 V;
- strict-test RMSE exceeds 0.075 V;
- strict-test absolute bias exceeds 0.020 V;
- practical Jacobian rank is below the parameter count;
- identifiability status is `RANK_DEFICIENT`;
- a parameter-axis profile has a lower noncentral objective;
- the weakest-direction profile has a lower noncentral objective;
- bootstrap usable fraction is below 0.80.

Warnings are generated for:

- elevated but nonrejection predictive errors;
- residual dependence;
- high condition number;
- strong parameter correlation;
- high relative uncertainty;
- near-bound parameter estimates;
- flat objective profiles;
- high bootstrap variability;
- low bootstrap convergence.

---

## 44. Final Decision and Score

Let `H` be the number of unique hard-failure reasons and `W` be the number of unique warning reasons.

The decision rule is:

| Condition | Decision |
|---|---|
| `H>0` | `REJECT` |
| `H=0` and `W>0` | `ACCEPT_WITH_CAUTION` |
| `H=0` and `W=0` | `ACCEPT` |

**Equation (174)**

The acceptance score is

```math
A
=
\min
\bigl(
100,
\max
(
0,
100-30H-5W
)
\bigr).
```

**Equation (175)**

A high score cannot override a hard failure.

Any hard failure forces rejection.

---

## 45. Final Executed Candidate Results

The final executed candidate table reports:

| Scope | Order | Test RMSE | Test bias | Strict-test RMSE | Maximum test residual correlation | Practical rank | Parameter count | Final decision |
|---|---|---:|---:|---:|---:|---:|---:|---|
| Global | 1RC | 0.431969 V | 0.167777 V | 0.605432 V | 0.908850 | 3 | 3 | `REJECT` |
| Global | 2RC | 0.431971 V | 0.167780 V | 0.605449 V | 0.908849 | 4 | 5 | `REJECT` |
| LFP | 1RC | 0.164429 V | 0.020858 V | 0.392642 V | 0.732742 | 3 | 3 | `REJECT` |
| LFP | 2RC | 0.164360 V | 0.020995 V | 0.392646 V | 0.734132 | 5 | 5 | `REJECT` |
| NCA | 1RC | 0.528546 V | 0.256501 V | 0.629874 V | 0.908469 | 3 | 3 | `REJECT` |
| NCA | 2RC | 0.528548 V | 0.256503 V | 0.629890 V | 0.908467 | 4 | 5 | `REJECT` |
| NMC | 1RC | 0.240987 V | 0.036885 V | 0.520619 V | 0.824230 | 3 | 3 | `REJECT` |
| NMC | 2RC | 0.402613 V | 0.110771 V | 0.520990 V | 0.932332 | 5 | 5 | `REJECT` |

Every ordinary-test RMSE exceeds 0.050 V.

Every strict-test RMSE exceeds 0.075 V.

Therefore, every candidate has at least two predictive hard failures before considering identifiability, objective profiles, or bootstrap stability.

---

## 46. Executed Identifiability Results

The code reports:

| Candidate | Practical rank | Parameter count | Condition number | Status |
|---|---:|---:|---:|---|
| Global 1RC | 3 | 3 | 1.9450 × 10⁴ | `FULL_RANK_BUT_WEAK` |
| Global 2RC | 4 | 5 | 5.2732 × 10⁷ | `RANK_DEFICIENT` |
| LFP 1RC | 3 | 3 | 4.1798 × 10⁴ | `FULL_RANK_BUT_WEAK` |
| LFP 2RC | 5 | 5 | 2.7733 × 10⁴ | `FULL_RANK_BUT_WEAK` |
| NCA 1RC | 3 | 3 | 6.8383 × 10³ | `FULL_RANK_BUT_WEAK` |
| NCA 2RC | 4 | 5 | 2.8883 × 10⁸ | `RANK_DEFICIENT` |
| NMC 1RC | 3 | 3 | 6.2259 × 10² | `FULL_RANK_BUT_WEAK` |
| NMC 2RC | 5 | 5 | 4.3986 × 10² | `FULL_RANK_BUT_WEAK` |

The global two-RC and NCA two-RC models are practically rank deficient.

The other six models are full rank but classified as weak because of severe transformed-parameter correlation or large physical-parameter uncertainty.

---

## 47. Executed Objective-Profile Results

The weakest joint direction is classified as `VERY_FLAT` for all eight candidates.

The dominant weak directions include:

- compensation between `log R_0` and `log R_1` in several one-RC models;
- compensation between `log R_1` and `log R_2` in the global and NCA two-RC models;
- a weak direction dominated by `log τ_1` and `log R_1` for the NMC two-RC model.

The NMC two-RC parameter-axis analysis also produces a `CENTER_NOT_SLICE_MINIMUM` result, creating an additional hard failure.

---

## 48. Executed Bootstrap Results

The code performs all 240 planned bootstrap refits.

For the displayed final decision table:

```math
f_{\mathrm{usable}}=1.0
```

and

```math
f_{\mathrm{conv}}=1.0
```

for all eight candidates.

Therefore, the bootstrap procedure itself completes successfully.

However, every candidate receives the bootstrap stability classification:

`WEAK`

The weakness is caused by large physical-parameter variability or frequent proximity to parameter bounds, not by an insufficient number of usable bootstrap runs.

For example, the NCA two-RC time-constant gap has a relative bootstrap standard deviation exceeding

```math
2.09.
```

This means that its bootstrap standard deviation is more than twice the magnitude of the frozen estimate.

---

## 49. Final Executed Decisions

The final output is:

| Decision class | Number of candidates |
|---|---:|
| `ACCEPT` | 0 |
| `ACCEPT_WITH_CAUTION` | 0 |
| `REJECT` | 8 |

The candidate-level results are:

| Candidate | Hard failures | Warnings | Acceptance score | Decision |
|---|---:|---:|---:|---|
| Global 1RC | 4 | 9 | 0 | `REJECT` |
| Global 2RC | 6 | 10 | 0 | `REJECT` |
| LFP 1RC | 4 | 9 | 0 | `REJECT` |
| LFP 2RC | 4 | 9 | 0 | `REJECT` |
| NCA 1RC | 4 | 9 | 0 | `REJECT` |
| NCA 2RC | 6 | 10 | 0 | `REJECT` |
| NMC 1RC | 4 | 9 | 0 | `REJECT` |
| NMC 2RC | 5 | 8 | 0 | `REJECT` |

The chemistry-level best available fixed candidates are:

| Chemistry | Best available fixed candidate | Outcome |
|---|---|---|
| LFP | LFP-specific 2RC | `REJECTED` |
| NCA | Global 1RC | `REJECTED` |
| NMC | NMC-specific 1RC | `REJECTED` |

The primary chemistry-specific two-RC baseline is rejected for all three chemistries.
