# Delay Learning in Spiking Neural Networks: A Systematic Review — Dataset

This repository contains the dataset of the paper **"Delay Learning in Spiking Neural Networks: A Systematic Review"** by Juan-Pablo Cárdenas-Rueda, José Ceardi and Javier Baladrón (Departamento de Ingeniería Informática, Universidad de Santiago de Chile), **JCC 2026 (45th International Conference of the Chilean Computer Science Society)**.

The review follows the PRISMA 2020 guidelines and covers primary, software-based studies in which the transmission delays of spiking neural networks (SNNs) are trainable parameters. The dataset lists the 42 included studies and their classification along the eight dimensions of Fig. 3 of the paper.

> [!NOTE]
> **`Surrogate Gradient` means gradient-based methods.** In this dataset and in Fig. 3(g) of the paper, the `Surrogate Gradient` category groups all gradient-based methods: surrogate-gradient training and other gradients, such as exact spike-time gradients (SpikeProp and its extensions, EventProp) and gradients computed on spike-train kernels. For each of these 24 studies, the `Notes` column starts with `Gradient-based (...)` and states the type of gradient used.

---

## Repository Structure

* `snn_delay_learning_dataset.csv`: one row per included study (42 rows, 15 columns).
* `README.md`: summary of the review method, data dictionary, taxonomy definitions and summary statistics.

---

## Review Method (PRISMA 2020)

### Research questions

1. **Taxonomy and families:** What are the predominant algorithmic families underlying the current delay-learning mechanisms in software-based SNNs?
2. **Neural dynamics:** Which spike-coding schemes and neuron models are most frequently coupled with delay learning?
3. **Structural localization of delays:** Where are learnable delays localized within the network architectures?

### Search

Databases: **Web of Science**, **Scopus** and **IEEE Xplore**. Period: January 2013 to May 2026. Web of Science was searched with the `ALL=` field tag, Scopus with `TITLE-ABS-KEY()`, and IEEE Xplore without field prefixes. For queries with an `OR` operator, the terms were searched separately and their results were merged. AI-based semantic search tools were not used.

| Query | Records |
|---|---:|
| `"delay learning" AND ("spiking neural network*" OR "SNN")` | 52 |
| `"learnable delay*" AND ("spiking neural network*" OR "SNN")` | 8 |
| `("synaptic delay*" OR "axonal delay*" OR "temporal delay*") AND ("spiking neural network*" OR "SNN")` | 175 |
| `("time delay*" OR "transmission delay*") AND ("learn*" OR "train") AND ("spiking neural network*" OR "SNN")` | 78 |
| **Total (raw counts across the three databases, including duplicates)** | **313** |

### Eligibility criteria

Inclusion:
* **Scope:** the study proposes, implements or analyzes an active algorithmic mechanism for training or optimizing delays.
* **Implementation:** the framework is implemented entirely in software, through computational simulation.
* **Neuron models:** the network uses integrative, spike-based neurons (e.g., LIF, Izhikevich).
* **Language and type of document:** primary research article (conference proceeding or journal paper) written in English.

Exclusion:
* **Hardware dependency:** the delay mechanism is constrained by or designed for specific neuromorphic hardware (e.g., FPGAs, memristive hardware).
* **Domain of the study:** the application falls strictly outside computational or artificial intelligence.
* **Delay as a static parameter:** delays are fixed (not trainable) and learning changes other parameters only.
* **Secondary literature:** surveys, reviews, tutorials or extended abstracts without a novel primary algorithmic contribution.

### Selection (Fig. 1 of the paper)

| Stage | Records |
|---|---:|
| Records identified from databases | 313 |
| Duplicate records removed before screening | 139 |
| Records screened (title and abstract) | 174 |
| Records excluded at screening | 114 |
| Reports sought for retrieval | 60 |
| Reports not retrieved | 7 |
| Reports assessed for eligibility (full text) | 53 |
| Reports excluded: no delay learning (delays are static) | 11 |
| **Studies included** | **42** |

---

## Data Dictionary

| Column | Description |
|---|---|
| `ID` | Row number (1–42). |
| `Title` | Title of the study as published. |
| `Algorithm` | Algorithmic family used to learn the delays (Fig. 3g). |
| `Neuronal Model` | Neuron model of the network (Fig. 3a). |
| `Type of Delay` | Location of the learnable delays (Fig. 3b). |
| `Codification` | Spike-coding scheme (Fig. 3c). |
| `Learning Type` | Learning paradigm (Fig. 3d). |
| `Problem Type` | Task addressed in the experiments (Fig. 3f). |
| `Network Type` | Network architecture (Fig. 3e). |
| `Trained Parameters` | Parameters optimized during learning (Fig. 3h). |
| `Indexation Year` | Year in which the record was indexed in the source database; it is the year used in Fig. 2. For conference papers it can be the year after the conference |
| `Source` | Journal name, or conference written as `YYYY Conference Name (ACRONYM)`. |
| `Authors` | Full names in publication order, written as `Family, Given` and separated by semicolons. |
| `Link` | DOI link, or the official proceedings page for the papers without a DOI (IDs 19, 37 and 41). |
| `Notes` | Short remarks on the classification: name of the method, type of gradient, and the reason for combined, `Other` or `Unidentified` labels. |

The file is UTF-8 (with BOM), comma-separated, with every field that contains a comma enclosed in double quotes. In spreadsheet programs configured with a semicolon as list separator, import it with the comma as delimiter (e.g., in Excel: *Data > From Text/CSV*).

---

## Taxonomy Definitions

Each study has exactly one value per column. Values joined with `+` mean that the study belongs to more than one category.

### 1. Algorithm (Fig. 3g)
Method used to learn or optimize the delays.
* **Surrogate Gradient (gradient-based methods):** gradient-descent and error-backpropagation methods. The label follows Fig. 3(g) of the paper, where this category groups every gradient-based method: surrogate-gradient training (e.g., BPTT with surrogate derivatives, SLAYER) and other gradients, such as exact spike-time gradients (SpikeProp and its extensions, EventProp) and gradients computed on spike-train kernels. The `Notes` column of each of these studies starts with `Gradient-based (...)` and states the type of gradient.
* **STDP:** local plasticity rules driven by the relative timing of pre- and postsynaptic spikes, including delay-specific variants. They are used both in unsupervised settings and in supervised schemes that add a teacher signal (e.g., ReSuMe-based methods).
* **Temporal Adjustment:** rules that shift the delays directly from temporal differences or distributions, without backpropagated gradients.
* **STDP + Temporal Adjustment:** combination of both families.
* **Neuroevolution:** evolutionary or genetic algorithms that optimize delays (and possibly weights) through the fitness of a population of networks.
* **Recursive Least Squares (RLS):** least-squares learning rules (shown as "Minimum Squares" in Fig. 3g).
* **Expectation-Maximization (EM):** probabilistic learning that approximates the Expectation-Maximization algorithm.
* **NAS:** neural architecture search over delay values and connection structure.

### 2. Neuronal Model (Fig. 3a)
* **Leaky Integrate-and-Fire (LIF):** integrate-and-fire neurons whose membrane potential decays toward rest (includes adaptive LIF variants).
* **Integrate-and-Fire (IF):** non-leaky integrate-and-fire neurons.
* **Spiking Response Model (SRM):** membrane potential expressed through response kernels (includes SRM0).
* **Izhikevich:** two-dimensional model with a membrane and a recovery variable.
* **Probabilistic Spiking Neuron (PSN):** spike generation governed by a probabilistic process.
* **Unidentified:** the study does not specify a standard neuron model, or states that the method does not depend on it.

### 3. Type of Delay (Fig. 3b)
* **Synaptic:** one learnable delay per connection between a presynaptic and a postsynaptic neuron.
* **Axonal:** one learnable delay per presynaptic neuron, applied to its output spikes before they reach all of its synapses.
* **Dendritic + Axonal:** learnable delays on the dendrites of the postsynaptic neuron (before the soma) and on the axons.
* **Synaptic + Axonal:** learnable synaptic and axonal delays in the same network.
* **Skip-connection delays:** learnable delays only on the skip connections of the network.

### 4. Codification (Fig. 3c)
* **Temporal coding:** information is carried by precise spike times (e.g., time-to-first-spike, latency coding, precise spike trains).
* **Rate coding:** information is carried by the number of spikes or the firing rate in a time window.
* **Rate coding + Temporal coding:** both schemes are used in the same model.
* **Phase coding:** spike times are relative to a background oscillation.
* **Other:** a complex or non-standard encoding that does not fit the categories above.
* **Unidentified:** the coding scheme is not specified.

### 5. Learning Type (Fig. 3d)
* **Supervised:** learning from target outputs (class labels or desired spike trains).
* **Unsupervised:** learning from the statistics of the input only.
* **Supervised + Unsupervised:** the study proposes both modes.
* **Self-supervised:** the network builds its own targets from the input.
* **Reinforcement:** learning from reward or fitness signals of an environment.

### 6. Problem Type (Fig. 3f)
* **Classification:** assigning inputs to discrete classes.
* **Regression:** predicting continuous values or times, such as forecasting event sequences or reproducing target spike trains.
* **Classification + Regression:** experiments of both kinds.
* **Control:** closed-loop control and path planning of robots.
* **Clustering:** grouping inputs without labels.
* **Feature Extraction:** unsupervised learning of spatiotemporal features (shown as "Characteristics Extraction" in Fig. 3f).
* **Unidentified:** no experimental task is reported.

### 7. Network Type (Fig. 3e)
* **Feedforward:** multilayer networks without recurrent connections.
* **Single-layer:** a single layer of learning neurons.
* **Convolutional:** convolutional SNNs.
* **Feedforward + Convolutional:** networks with both convolutional and fully connected feedforward layers, or experiments with both.
* **Recurrent:** networks with recurrent connections.
* **Recurrent + Feedforward:** experiments with both recurrent and feedforward networks.
* **Skip-connections:** networks with skip connections.
* **Graph-like:** spiking graph neural networks.

### 8. Trained Parameters (Fig. 3h)
* **Weights + Delays:** synaptic weights and delays are learned together.
* **Weights + Delays + Threshold:** weights, delays and firing thresholds.
* **Weights + Delays + Topology:** weights and delays, while the connectivity also changes (pruning and rewiring, removal of redundant delays, or architecture search).
* **Delays:** only delays are learned; the weights are fixed.
* **Other:** other combinations, such as weights and delays together with membrane or synaptic time constants, thresholds or adaptation parameters, or delays at two locations (see `Notes`).

---

## Summary Statistics

All values below are computed from `snn_delay_learning_dataset.csv`.

### Counting rule

In Fig. 3 of the paper, a study with a combined value (e.g., `Synaptic + Axonal`) is counted once in each of its categories. For this reason, the totals of panels (b), (c), (d), (e), (f) and (g) are larger than 42, and the percentages of Fig. 3 are shares of those totals. The last column of each table gives the share of the 42 studies.

### Fig. 2: studies per indexation year

| Year | 2013 | 2014 | 2015 | 2016 | 2017 | 2018 | 2019 | 2020 | 2021 | 2022 | 2023 | 2024 | 2025 | 2026 | Total |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Papers | 1 | 1 | 2 | 3 | 3 | 2 | 2 | 2 | 2 | 3 | 5 | 5 | 4 | 7 | 42 |

### Fig. 3(a): Neuronal Models

| Category in Fig. 3(a) | Values in the CSV | n | Share in Fig. 3(a) (n / 42) | Papers (n / 42) |
|---|---|---:|---:|---:|
| SRM | Spiking Response Model (SRM) (17) | 17 | 40.5% | 40.5% |
| LIF | Leaky Integrate-and-Fire (LIF) (16) | 16 | 38.1% | 38.1% |
| IF | Integrate-and-Fire (IF) (4) | 4 | 9.5% | 9.5% |
| Izhikevich | Izhikevich (2) | 2 | 4.8% | 4.8% |
| Unidentified | Unidentified (2) | 2 | 4.8% | 4.8% |
| PSN | Probabilistic Spiking Neuron (PSN) (1) | 1 | 2.4% | 2.4% |
| **Total** | | **42** | **100%** | |

### Fig. 3(b): Type of Delays

| Category in Fig. 3(b) | Values in the CSV | n | Share in Fig. 3(b) (n / 44) | Papers (n / 42) |
|---|---|---:|---:|---:|
| Synaptic | Synaptic (28), Synaptic + Axonal (1) | 29 | 65.9% | 69.0% |
| Axonal | Axonal (10), Synaptic + Axonal (1), Dendritic + Axonal (1) | 12 | 27.3% | 28.6% |
| Skip-Connections | Skip-connection delays (2) | 2 | 4.5% | 4.8% |
| Dendritic | Dendritic + Axonal (1) | 1 | 2.3% | 2.4% |
| **Total** | | **44** | **100%** | |

### Fig. 3(c): Codification Types

| Category in Fig. 3(c) | Values in the CSV | n | Share in Fig. 3(c) (n / 43) | Papers (n / 42) |
|---|---|---:|---:|---:|
| Temporal-Coding | Temporal coding (35), Rate coding + Temporal coding (1) | 36 | 83.7% | 85.7% |
| Rate-Coding | Rate coding (2), Rate coding + Temporal coding (1) | 3 | 7.0% | 7.1% |
| Other | Other (2), Unidentified (1) | 3 | 7.0% | 7.1% |
| Phase-Coding | Phase coding (1) | 1 | 2.3% | 2.4% |
| **Total** | | **43** | **100%** | |

### Fig. 3(d): Learning Types

| Category in Fig. 3(d) | Values in the CSV | n | Share in Fig. 3(d) (n / 43) | Papers (n / 42) |
|---|---|---:|---:|---:|
| Supervised Learning | Supervised (33), Supervised + Unsupervised (1) | 34 | 79.1% | 81.0% |
| Unsupervised Learning | Unsupervised (6), Supervised + Unsupervised (1) | 7 | 16.3% | 16.7% |
| Auto-supervised Learning | Self-supervised (1) | 1 | 2.3% | 2.4% |
| Reinforcement Learning | Reinforcement (1) | 1 | 2.3% | 2.4% |
| **Total** | | **43** | **100%** | |

### Fig. 3(e): Network Types

| Category in Fig. 3(e) | Values in the CSV | n | Share in Fig. 3(e) (n / 47) | Papers (n / 42) |
|---|---|---:|---:|---:|
| Traditional Feedforward | Feedforward (17), Feedforward + Convolutional (3), Recurrent + Feedforward (2) | 22 | 46.8% | 52.4% |
| Single-Layer | Single-layer (11) | 11 | 23.4% | 26.2% |
| Convolutional | Convolutional (2), Feedforward + Convolutional (3) | 5 | 10.6% | 11.9% |
| Recurrent | Recurrent (3), Recurrent + Feedforward (2) | 5 | 10.6% | 11.9% |
| Skip-Connections | Skip-connections (3) | 3 | 6.4% | 7.1% |
| Graph-like | Graph-like (1) | 1 | 2.1% | 2.4% |
| **Total** | | **47** | **100%** | |

### Fig. 3(f): Type of Problem

| Category in Fig. 3(f) | Values in the CSV | n | Share in Fig. 3(f) (n / 43) | Papers (n / 42) |
|---|---|---:|---:|---:|
| Classification | Classification (33), Classification + Regression (1) | 34 | 79.1% | 81.0% |
| Regression | Regression (3), Classification + Regression (1) | 4 | 9.3% | 9.5% |
| Control | Control (2) | 2 | 4.7% | 4.8% |
| Clustering | Clustering (1) | 1 | 2.3% | 2.4% |
| Characteristics Extraction | Feature Extraction (1) | 1 | 2.3% | 2.4% |
| Unidentified | Unidentified (1) | 1 | 2.3% | 2.4% |
| **Total** | | **43** | **100%** | |

### Fig. 3(g): Algorithms

| Category in Fig. 3(g) | Values in the CSV | n | Share in Fig. 3(g) (n / 43) | Papers (n / 42) |
|---|---|---:|---:|---:|
| Surrogate Gradient (gradient-based methods) | Surrogate Gradient (24) | 24 | 55.8% | 57.1% |
| STDP | STDP (9), STDP + Temporal Adjustment (1) | 10 | 23.3% | 23.8% |
| Neuroevolution | Neuroevolution (3) | 3 | 7.0% | 7.1% |
| Temporal Adjustment | Temporal Adjustment (2), STDP + Temporal Adjustment (1) | 3 | 7.0% | 7.1% |
| Minimum Squares | Recursive Least Squares (RLS) (1) | 1 | 2.3% | 2.4% |
| EM | Expectation-Maximization (EM) (1) | 1 | 2.3% | 2.4% |
| NAS | NAS (1) | 1 | 2.3% | 2.4% |
| **Total** | | **43** | **100%** | |

### Fig. 3(h): Trained Parameters

| Category in Fig. 3(h) | Values in the CSV | n | Share in Fig. 3(h) (n / 42) | Papers (n / 42) |
|---|---|---:|---:|---:|
| Delays + Weights | Weights + Delays (28) | 28 | 66.7% | 66.7% |
| Delays | Delays (4) | 4 | 9.5% | 9.5% |
| Others | Other (4) | 4 | 9.5% | 9.5% |
| D. + W. + Thresholds | Weights + Delays + Threshold (3) | 3 | 7.1% | 7.1% |
| D. + W. + Topology | Weights + Delays + Topology (3) | 3 | 7.1% | 7.1% |
| **Total** | | **42** | **100%** | |

---

## Errata

The counts (n) reported in the paper match this dataset, except for the PSN neuron model. The table lists the passages of the paper whose numbers differ from the values computed above. The last row clarifies the definition of `Surrogate Gradient`.

| Section of the paper | Published text | Value from this dataset |
|---|---|---|
| IV-1 (neuron models) | "Specialized dynamics, such as the Probabilistic Spiking Neuron (PSN), comprise the remaining 5% (n = 2) of the corpus." | PSN: n = 1 (2.4%). The remaining 3 studies (7.1%) are PSN (1) and Unidentified (2, 4.8%). |
| IV-1 and V (neuron models) | Izhikevich: "5% (n = 2)" | 4.8% (2 of 42), rounded to 5% in the text. |
| IV-2 (delays) | "Synaptic Delays account for 65.9% (n = 29) of the papers"; "Axonal Delays comprises 27.3% (n = 12)" | 65.9% and 27.3% are shares of the 44 delay labels of Fig. 3(b). As shares of the 42 studies: Synaptic 69.0%, Axonal 28.6%. |
| IV-2 (delays) | "The remaining 7% (n = 3) covers specialized structural paradigms, including combined Synaptic+Axonal layers, Dendritic+Axonal compartmental boundaries, or specialized skip-connection transmission buffers." | The remaining 3 labels (6.8%) are Dendritic (1) and Skip-connection delays (2). The Synaptic + Axonal study is counted under Synaptic and Axonal, and the Dendritic + Axonal study under Dendritic and Axonal. |
| IV-3 (coding) | "Rate-Coding paradigms are strictly confined to 7% (n = 3) of the corpus, with an additional 2.5% (n = 1) implementing a hybrid Rate-Coding + Temporal scheme." | The n = 3 already includes the hybrid study (2 Rate coding + 1 Rate coding + Temporal coding). The hybrid study is 1 of 43 labels: 2.3%. |
| IV-3 (coding) | "Phase-Coding layouts comprise 2.5% (n = 1)" | 2.3% (1 of 43). |
| IV-4 (learning) | Reinforcement and self-supervised learning: "combined representing only 5% (n = 2)" | 4.7% (2 of 43), rounded to 5% in the text. |
| IV-5 (networks) | "The final 8.6% (n = 4) consists of emerging architectural variations" | 8.5% (4 of 47). |
| II-A, II-F and V (algorithms) | II-A: "surrogate gradient methods that approximate the non-differentiable spike activation with smooth, continuous functions during the backward pass" (II-F gives the same definition); V: "supervised surrogate gradient descent represents the predominant training paradigm at 55.8% of the literature, it relies on continuous approximations of non-differentiable spike activations" | This definition is narrower than the `Surrogate Gradient` category of Fig. 3(g). The category groups all gradient-based methods: besides surrogate-gradient training, it includes other gradients, such as exact spike-time gradients (SpikeProp and its extensions, EventProp) and gradients computed on spike-train kernels. The count in IV-7 and Fig. 3(g) (n = 24, 55.8%) is correct for this category. The `Notes` column states the type of gradient used by each study. |

---

## Citation

```bibtex
@inproceedings{cardenasrueda2026delay,
  title     = {Delay Learning in Spiking Neural Networks: A Systematic Review},
  author    = {C{\'a}rdenas-Rueda, Juan-Pablo and Ceardi, Jos{\'e} and Baladr{\'o}n, Javier},
  booktitle = {45th International Conference of the Chilean Computer Science Society (JCC 2026)},
  publisher = {IEEE},
  year      = {2026}
}
```

---

## Acknowledgment

This work was supported by the National Agency for Research and Development (ANID) of Chile through FONDECYT Regular Grant No. 1251455 "NeuroMetaEvo: Integrating Metaheuristic Techniques with Neuroscience for Advanced Neuromorphic Algorithm Design".
