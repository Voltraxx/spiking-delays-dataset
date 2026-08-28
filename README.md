# Systematic Mapping of Delay-Learning in Spiking Neural Networks (SNNs)

This repository contains the dataset and taxonomy for the systematic mapping study submitted to the **JCC 2026 (45th International Conference of the Chilean Computer Science Society)**. 

Our study presents a comprehensive analysis of the state-of-the-art algorithms, topologies, models and more that optimize or learn **transmission delays** in Spiking Neural Networks (SNNs) to capture temporal dynamics.

---

## Mapping Methodology Summary (PRISMA 2020)

Following the PRISMA 2020 guidelines, we searched three major databases (Web of Science, Scopus, and IEEE Xplore) using targeted query strings:
* **Records Identified:** 319 records
* **Duplicates Removed:** 145 records (intra- and inter- database)
* **Records Screened (Abstract):** 174 records
* **Full-Text Selection:** 42 papers met the strict inclusion/exclusion criteria.

---

## Repository Structure

* `snn_delay_learning_dataset.csv`: The complete dataset containing the taxonomy of the 42 selected papers.
* `README.md`: This file, which serves as a data dictionary and interactive index.

---

## Data Dictionary & Taxonomy Definitions

To ensure reproducibility and resolve common ambiguities, we define our classification schema below:

### 1. Algorithm
Defines the mathematical approach used to update/learn the connection delays:
* **Surrogate Gradient:** Backpropagation-based methods using smooth surrogate functions to bypass the non-differentiable spiking threshold (e.g., surrogate gradient descent).
* **STDP (Spike-Timing-Dependent Plasticity):** Local, unsupervised learning rules that adjust connection efficacy based on the relative timing of pre- and post-synaptic spikes.
* **Temporal Adjustment:** Heuristic, analytical, or delta-like rules that adjust delays directly based on temporal differences without formal backprop gradients.
* **NAS (Neural Architecture Search):** Search-based optimization methods used to discover discrete, optimal delay structures and configurations prior to or during training.
* **Recursive Least Squares (RLS):** An analytical, recursive optimization method that minimizes the sum of squared errors to adjust weights and delays dynamically.
* **Expectation-Maximization (EM):** A statistical, probabilistic framework used to maximize parameter likelihood in SNNs under noisy conditions.
* **Neuroevolution:** Optimization of SNN parameters (delays, weights, or topology) using evolutionary or genetic algorithms (GAs).

### 2. Neuronal Model
The mathematical model representing single-neuron dynamics:
* **LIF (Leaky Integrate-and-Fire):** Neurons with passive membrane decay.
* **IF (Integrate-and-Fire):** Simple non-decaying integrators.
* **SRM (Spiking Response Model):** Kernel-based representations of membrane potential.
* **Izhikevich Model:** A two-dimensional, biophysically plausible model capable of reproducing complex cortical firing patterns.
* **PSN (Probabilistic Spiking Neuron):** Models where spike generation is governed by stochastic or probabilistic processes rather than deterministic thresholds.
* **Not identified:** Cases where the single-neuron model is custom-designed or not explicitly standardized in the paper's text.

### 3. Type of Delay
Where the learnable/plastic delay is physically or computationally located:
* **Axonal:** Conduction delays representing the travel time of an action potential along the axon after it is generated.
* **Synaptic:** Localized delays at the synaptic cleft representing neurotransmitter release and receptor kinetics.
* **Dendritic:** Delay of transmission occurring along the dendritic branches prior to somatic integration.
* **Skip-connection delays:** Delays applied to identity or feedforward skip-connections to match temporal paths.
* **Combinations (e.g., Synaptic + Axonal, Dendritic + Axonal):** Hybrid delay locations where multiple propagation delays are co-learned or modeled.

### 4. Codification
The encoding mechanism used to convert continuous input into discrete spike times:
* **Temporal:** Information is encoded in the precise timing of individual spikes (e.g., Time-to-First-Spike, latency coding, or precise interval selectivity).
* **Rate-coding:** Information is encoded in the average firing rate or spike frequency over a given time window.
* **Phase-coding:** Information is encoded in the timing of spikes relative to an ongoing background oscillatory wave.
* **Mixed:** Hybrid encoding schemes utilizing both average frequency and precise timing channels.
* **Other / Not identified:** Custom, complex spatial mapping, or cases not explicitly detailed by the authors.

### 5. Learning Type
The paradigm under which the SNN is optimized:
* **Supervised:** SNN trained to minimize error against a target output signal or class label.
* **Unsupervised:** SNN organizes itself based on input statistics.
* **Self-supervised:** The network generates its own supervisory signals from the structure of the input data.
* **Reinforcement Learning:** Network parameters are updated based on scalar reward/punishment signals from an environment.

### 6. Problem Type
The target application or computational goal:
* **Classification:** Categorizing dynamic or static inputs into discrete classes.
* **Regression:** Predicting continuous values, forecasting time-series events, or reproducing exact multi-spike temporal patterns.
* **Control:** Closed-loop navigation, path planning, and autonomous robotic navigation.
* **Feature Extraction / Clustering:** Unsupervised learning of salient representations or dividing data into similarity groups without labels.

### 7. Network Type
The architectural topology of the SNN:
* **Feedforward:** Static layer-by-layer connections without recurrent loops.
* **Recurrent:** Connections that form directed cycles.
* **Convolutional:** Weight-sharing spatial kernels optimized for multidimensional spatial inputs.
* **Single-layer:** A single layer of processing neurons.
* **Skip-connections:** Architectures augmenting feedforward SNNs with bypass or identity skip connections (e.g., ResNet-like SNNs).
* **Graph-like SNN:** SNNs structured as graph neural networks to aggregate dynamic spatial neighborhood relationships over time.

### 8. Trained Parameters
The specific parameter sets optimized during learning:
* **Weights + Delays:** Co-learning of synaptic weights and temporal propagation delays.
* **Weights + Delays + Threshold:** Simultaneous optimization of weights, delays, and neuronal firing thresholds.
* **Weights + Delays + Topology:** Search-based co-optimization of connectivity structure, weights, and delays.
* **Delays:** Architectures where weights are kept fixed, and learning is exclusively carried out in the temporal delay domain.
* **Other:** Models where additional parameters (such as membrane time constants or adaptation thresholds) are co-learned.
