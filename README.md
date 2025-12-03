# Neural Speciation: Algorithmically Evolved Hyperparameters

![Python](https://img.shields.io/badge/Python-3.9%2B-blue) ![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-red) ![License](https://img.shields.io/badge/License-CC_BY--SA_4.0-lightgrey) ![Status](https://img.shields.io/badge/Status-Active_Research-green)

**Neural Speciation** is an evolutionary computation framework designed to discover the "Universal Laws of Generalization" in Transformer architectures.

<img width="1251" height="587" alt="image" src="https://github.com/user-attachments/assets/d97b3a39-71b0-4eae-876a-6204182e58b2" />

Instead of treating hyperparameter initialization (Learning Rates, Betas, Weight Variances) as static constants, this project treats them as a **Genome Sequence containing 17 genes**. By simulating natural selection, sexual reproduction, and mutation over thousands of generations, we evolve MicroTransformers that "Grok" (generalize) modular arithmetic tasks with superhuman efficiency.

## 🧬 The Science: Why Evolve Initialization?

In Deep Learning, we often initialize weights using standard heuristics (Xavier, Kaiming) and tune learning rates via grid search. **Neural Speciation** challenges this dogma.

By treating the configuration as a biological 17-gene genome, we look for **Co-adapted Gene Complexes**. These are parameters that only work well when paired together.
*   **The Task:** Modular Addition ($a + b \pmod{97}$). A task known for "Grokking"—where models memorize training data long before they suddenly "understand" the pattern.
*   **The Goal:** Minimize the time-to-grok and maximize stability across random seeds.
*   **The Discovery:** We have already observed "Speciation"—distinct clusters of parameters that solve the task using different internal dynamics. (e.g., High-Embed-Variance vs. High-Learning-Rate strategies).

## 🔬 The Genome (17 Genes)

The models evolve 17 distinct genes. Rather than random noise, these parameters map directly to biological concepts of metabolism, plasticity, and homeostasis.

| Gene Group | Specific Genes | Biological Analogy |
| :--- | :--- | :--- |
| **Metabolic Rate** | `Learning Rate`<br>`Weight Decay` | **Basal Metabolism:** How fast the organism burns energy (consumes data) vs. conserves resources (decay/forgetting). High LR is a hyperactive metabolism; High Decay is rapid cellular turnover. |
| **Cognitive Reflexes** | `Beta 1`<br>`Beta 2` | **Neural Reactivity:** How quickly the organism adapts to new stimuli vs. retaining memory of past gradients (momentum). |
| **Homeostasis** | `Grad Clip`<br>`Adam Epsilon` | **Stress Tolerance:** Mechanisms that prevent the organism from crashing (dying) under high-intensity shock updates (exploding gradients). |
| **Life Cycle** | `Warmup Steps`<br>`Decay Trigger (Var)`<br>`Decay Rate` | **Developmental Phases:** "Childhood" (Warmup) where learning is gentle, followed by "Adulthood" (Decay) where plasticity hardens to lock in skills once the loss landscape stabilizes. |
| **Signal Modulation** | `Dropout`<br>`Layer Scale` | **Synaptic Pruning:** Randomly disabling pathways (Dropout) or amplifying signals (Layer Scale) to prevent overfitting (habituation). |
| **Neural Plasticity (Init)** | `Init Attn QK`<br>`Init Attn V`<br>`Init FFN`<br>`Bias Scale` | **Brain Morphometry:** The initial physical structure of the brain. High variance = high initial chaos/creativity; Low variance = calm/structured start. |
| **Sensory Sensitivity** | `Init Embed`<br>`Embed Ratio` | **Sensory Gating:** `Embed Ratio` is unique here. It controls "starvation"—forcing the internal brain to work harder because the sensory inputs (embeddings) are weak. |

> **Field Note:** A surprising finding from this simulation is the emergence of `Embed Ratio > 14.0`. Standard deep learning theory suggests keeping this near 1.0. Our evolution suggests that "starving" the embeddings forces the attention heads to perform logic rather than memorization early in training.

## 🛠️ The Laboratory Modules

This repository is a unified GUI application comprising four distinct modules, each serving a specific stage in the scientific pipeline.

### 1. 🧬 The Evolutionary Lab (`evolve.py`)
<img width="1919" height="1023" alt="evolution_lab" src="https://github.com/user-attachments/assets/db94a38a-1c28-4be2-815a-a97e1fff5bad" />

The heart of the simulation. This module manages population dynamics and the "Battle Arena" where models live or die based on their ability to generalize.

*   **Ancestral Seeding (Directed Evolution):** You are not forced to start from random slime. You can inject successful genomes from the Registry or Gene Forge into Generation 1 to refine them further.
*   **Operators:** Implements Sexual Reproduction (Crossover), Asexual Cloning, and "Radiation" (Mutation).
*   **Fitness Landscapes:**
    *   *Sniper:* Selects for low variance (high reliability).
    *   *Tank:* Selects for survival (robustness against bad seeds).
    *   *Sprinter:* Selects for raw speed (steps to grok).
*   **Selection Strategies:**
    *   *3-Way / 2-Way Tournament:* Simulates sexual competition. Winners breed.
    *   *Spartan:* Ecological filtering. Automatically culls the bottom 50% of the population every generation.
*   **Population Diversity Controls:**
    *   *Aliens:* Injects completely random genomes into the population every generation to prevent inbreeding depression.
    *   *Elites:* The "Immortality" mechanic. The top N organisms are cloned into the next generation, but they suffer from **Senescence**—they must re-prove their fitness every generation. If they fail a trial due to a bad seed, they lose their Elite status and die.
*   **Population Diversity View:** Displays genetic diversity of the population as an RGB grid. The more similar the colors, the more closely related the genomes.
*   **Hall of Fame:** Hashes distinct genomes and saves the elite to the registry.
    *   *Strictness:* Setting to determine how fit a genome must be to be admitted to the Hall of Fame.

### 2. 🔨 The Gene Forge (`gene_forge.py`)
<img width="1919" height="1027" alt="gene_forge" src="https://github.com/user-attachments/assets/68707a9b-cee7-4166-a780-64a438bf8fa7" />

A tool for **Genetic Engineering** and **Horizontal Gene Transfer (HGT)**.

*   **Radar Visualization:** Real-time geometric comparison of Recipient vs. Donor genomes.
*   **Horizontal Gene Transfer:** Take the `Beta1` and `Weight_Decay` from a successful "Sprinter" species and splice them into a "Tank" species to create a hybrid super-learner.
*   **Manual Splicing:** Fine-tune specific genes (e.g., `Embed Ratio`) to test specific hypotheses before re-releasing the genome into the wild.
*   **Custom Genomes:** Supports saving custom genomes in their own directory where their .json files can be imported into the Evolution Lab or Stress Tests.

### 3. 🧪 The Stress Chamber (`stress_test.py`)
<img width="811" height="1022" alt="stress_test" src="https://github.com/user-attachments/assets/a5548785-c54c-463c-b307-9c10d592e050" />

Scientific rigor is paramount. A genome might perform well once due to a lucky random seed. This module acts as the "Peer Review" phase.

*   **Monte Carlo Validation:** Automatically runs a genome $N$ times (e.g., 200 runs) across unique seeds to map its true performance distribution.
*   **Smart Fill:** Detects existing data in the project folders. If you ask for 200 runs and 50 already exist, it only computes the missing 150.
*   **Grouping:** Supports grouping genomes by group / species or as individual genes for easy analysis.
*   **Analytics Dashboard:** Generates 7 types of charts, including Phase Transition plots (Loss vs Acc), Box Plots of convergence speed, and Success Rate histograms.
    *   *Legend Controls:* Robust legend controls, allowing showing and hiding of groups, individual genomes, lines / boxes / confidence intervals, etc to allow you to get your perfect shot of your data.

### 4. 📊 The Phylogenetic Dashboard (`neural_speciation_dashboard.py`)
<img width="1919" height="665" alt="image" src="https://github.com/user-attachments/assets/d29868b6-e392-438f-b5fb-3e727141f350" />

A hardware-accelerated 3D visualization of the fitness landscape.

*   **PCA Projection:** Maps the 17-dimensional genome into 3D space using Principal Component Analysis.
*   **Unsupervised Clustering:** Automatically detects, reveals, and names "Species" (e.g., `High-LR / Low-Decay Cluster`).
    *   New Feature: Can now choose to categorize genomes by Domain, Kingdom, Phylum, Class, Order, Family, or Genus, loosening or tightening the graph's categorization of genetic relatedness.
*   **Clipboard Integration:**
    *   Click any individual node to copy its DNA hash.
    *   Click a Species Name to copy **all** hashes within that cluster (useful for bulk-importing a species back into the Evolution Lab for further refinement or Stress Test for data analysis).

## 🚀 Installation & Usage

### Prerequisites
*   Python 3.9+
*   PyTorch (CUDA recommended)
*   Tkinter (Standard with Python)
*   Matplotlib, Seaborn, Pandas, Scikit-Learn, Plotly, PyWebView

### Quick Start

1.  **Clone the Repo**
    ```bash
    git clone https://github.com/Mmorgan-ML/Neural-Speciation.git
    cd Neural-Speciation
    ```

2.  **Install Dependencies**
    ```bash
    pip install torch numpy pandas matplotlib seaborn scikit-learn plotly pywebview
    ```

3.  **Launch the Unified Lab**
    ```bash
    python main.py
    ```
    *This launches the future Unified Command Center containing tabs for all 4 modules.*
    *Until this feature is fully implemented, modules must be opened and used separately.*

## 📈 Roadmap & Future Work

*   **Unified GUI:** Currently, the sub-modules are utilized separately, but work is being done to unify them into a single tabbed GUI interface.
*   **Advanced Speciation Dashboard Controls:** Currently, the Speciation Dashboard displays the Hall of Fame genomes using PCA 3D graphing. Plans to implement importing of .jsons for custom genome mapping.
*   **Transformer Scaling:** Experiments to test if "Grokking Genes" discovered at 10k parameters transfer to 10M+ parameter models.
*   **Mechanism Interpretability:** Hooks to visualize attention maps of evolved species to see *how* they compute modular addition differently.

## 📜 License
This work is licensed under the **Creative Commons Attribution-ShareAlike 4.0 International License**.

---
*Original Author: Michael Morgan (2025)*
