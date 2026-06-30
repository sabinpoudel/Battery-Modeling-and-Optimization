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

![Reference discharge-capacity and SOH evolution](figures/step6_capacity_and_soh_evolution.png)

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

Some early SOH values slightly exceed one because the baseline is estimated from several accepted early events rather than necessarily from the single largest capacity observation.

### Main Significance

The figure reveals clear chemistry- and cell-dependent degradation patterns. LFP and NMC cells show comparatively smooth and consistent capacity decline, whereas NCA cells exhibit substantially greater heterogeneity. The abrupt dip and recovery in `NCA_CELL_3` and the extreme decline in `NCA_CELL_4` should be reviewed against segment quality, discharge completeness, temperature, current integration, and event-acceptance criteria before being interpreted solely as physical degradation.

**Figure caption:** Accepted reference-discharge capacity and normalized event-level SOH evolution for eight physical cells. LFP and NMC cells exhibit gradual and consistent degradation, while the NCA group shows stronger cell-to-cell variability, including severe decline in `NCA_CELL_4` and an isolated irregular event in `NCA_CELL_3`.

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

The figure reveals clear chemistry- and cell-dependent degradation patterns. LFP and NMC cells show comparatively smooth and consistent capacity decline, whereas NCA cells exhibit substantially greater heterogeneity. The abrupt dip and recovery in `NCA_CELL_3` and the extreme decline in `NCA_CELL_4` should be reviewed against segment quality, discharge completeness, temperature, current integration, and event-acceptance criteria before being interpreted solely as physical degradation.




 
