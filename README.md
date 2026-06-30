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
