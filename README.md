## Dataset Acknowledgement

The datasets used in this study were downloaded from the **FairData repository** under the title *“NMC, NCA, and LFP Cells Degradation Under Randomized Current Profiles.”*

- **Data identification number:** `10.23729/b07462e8-9e31-428c-bdd5-deb1890c608b`
- **Direct DOI URL:** https://doi.org/10.23729/b07462e8-9e31-428c-bdd5-deb1890c608b
- **FairData dataset page:** https://etsin.fairdata.fi/dataset/f60a7388-99b6-4637-96d5-8610a7f71612

Grateful acknowledgement is given to the **New Energy Research Center, Turku University of Applied Sciences, Turku, Finland**, for conducting the battery degradation experiments, collecting the voltage, current, temperature, and operating-profile measurements, and making the raw and processed datasets publicly available through FairData. 


## 4. Dataset Composition

The downloaded datasets contains eight physical lithium-ion cells distributed across three battery chemistries:

\[
\mathcal{C}
=
\left\{
\mathrm{LFP},
\mathrm{NCA},
\mathrm{NMC}
\right\}.
\]

| Chemistry | Physical cells | Number of cells |
|:---:|:---|---:|
| LFP | `LFP_CELL_1`, `LFP_CELL_2` | 2 |
| NCA | `NCA_CELL_1`, `NCA_CELL_2`, `NCA_CELL_3`, `NCA_CELL_4` | 4 |
| NMC | `NMC_CELL_1`, `NMC_CELL_2` | 2 |
| **Total** | — | **8** |

The total number of physical cells is therefore

\[
N_{\mathrm{cells}}
=
2_{\mathrm{LFP}}
+
4_{\mathrm{NCA}}
+
2_{\mathrm{NMC}}
=
8.
\]

Additional reference files include:

- chemistry-specific open-circuit-voltage measurements;
- ambient-temperature measurements;
- experimental comments;
- experimental protocol descriptions.

Each physical-cell file contains multiple experimental segments. One segment represents either a complete test trajectory or one stage of an experimental cycle.

Let \(N_{c}\) denote the number of registered segments for physical cell \(c\). The segment counts are summarized below.

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

\[
\begin{aligned}
N_{\mathrm{segments}}
&=
660
+
672
+
602
+
505
+
576
+
697
+
617
+
613 \\
&=
4{,}942.
\end{aligned}
\]

Total chemistry-level segment are

\[
N_{\mathrm{LFP}}
=
660+672
=
1{,}332,
\]

\[
N_{\mathrm{NCA}}
=
602+505+576+697
=
2{,}380,
\]

and

\[
N_{\mathrm{NMC}}
=
617+613
=
1{,}230.
\]

Hence,

\[
N_{\mathrm{segments}}
=
N_{\mathrm{LFP}}
+
N_{\mathrm{NCA}}
+
N_{\mathrm{NMC}}
=
1{,}332
+
2{,}380
+
1{,}230
=
4{,}942.
\]
The NCA chemistry contributes the largest number of segments. It contains four physical cells, whereas the LFP and NMC groups each contain two cells.
