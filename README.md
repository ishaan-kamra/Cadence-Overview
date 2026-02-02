# Cadence - Longitudinal Speech Feature Modeling and Cognitive Trajectory Analysis

Cadence is a continuous functional monitoring platform that leverages speech as a real-world, high-frequency signal for tracking cognitive and neurological change over time. The system is designed around the observation that meaningful change emerges through **patterns across repeated interactions**, rather than isolated assessments or single measurements.

**Trained on 750+ recordings across heterogeneous speech settings, spanning structured elicitation tasks and naturalistic long-form conversation, Cadence models cognitive change with both clinical control and real-world variability.**

This repository contains the **modeling, statistical analysis, and longitudinal inference layer** of the Cadence pipeline. It operates on speech-derived features generated from structured and unstructured speech and focuses on feature-level interpretability, model performance, and trajectory-based reasoning rather than raw audio processing.

---

## End-to-End System Context

In Cadence’s workflow, speech data is collected from both **structured speech tasks** and **naturalistic long-form conversational speech**. Audio is transcribed using **OpenAI Whisper** (via Wispr), producing timestamp-aligned transcripts that preserve temporal structure.

From these transcripts, Cadence extracts a rich set of **acoustic, lexical, semantic, and temporal features**, including pause frequency and duration, speech rate, lexical richness, pronoun usage, semantic coherence, and fundamental frequency characteristics. These features are computed consistently across speech contexts and consolidated into structured representations that serve as inputs to the modeling and longitudinal analysis pipeline implemented in this repository.

This architectural design enables Cadence to integrate controlled linguistic elicitation with real-world speech dynamics while maintaining interpretability and robustness.

---

## Scope of This Repository

This repository implements Cadence’s **core analytical logic**, spanning feature analysis, predictive modeling, and longitudinal trajectory inference.

The model is trained jointly on:

* **Structured speech tasks**, designed to elicit constrained linguistic behavior that amplifies cognitive signal, and
* **Naturalistic long-form conversational speech**, capturing unconstrained, real-world speech patterns.

By learning from both modalities, Cadence captures complementary aspects of cognitive function leveraging the sensitivity of structured tasks while retaining robustness to everyday speech variability.

---

## Feature-Level Statistical Analysis

**All figures below this point were created by me from Cadence’s end-to-end evaluation runs in model_analysis.ipynb and reflect observed model behavior across the full training/evaluation pipeline.**

Feature distributions are analyzed separately for structured and unstructured speech contexts using a combination of parametric and non-parametric statistical tests. Box-and-jitter visualizations compare control and dementia groups across multiple feature families, including lexical measures, pronoun usage, pause behavior, semantic metrics, and fundamental frequency.

![Unstructured Speech Feature Distributions](assets/Unstructured%20Speech%20Feature%20Distributions.png)

In structured speech tasks, several features exhibit strong group-level separation with high statistical significance (p < 0.001), including lexical measures, pronoun usage, pause-related features, semantic coherence, and fundamental frequency.

![Structured Speech Feature Distributions](assets/Structured%20Speech%20Feature%20Distributions.png)

These results indicate that controlled speech tasks amplify specific linguistic and temporal differences relevant to cognitive characterization. In contrast, unstructured speech exhibits fewer highly significant features, though temporal and prosodic measures, particularly pause-related metrics, remain consistently informative, highlighting the robustness of timing-based signals in unconstrained settings.

---

## Feature Significance Ranking

To summarize feature relevance across analyses, features are ranked by statistical significance using −log₁₀(p-value) representations. Pause frequency, semantic coherence, average pause duration, and speech rate emerge as the most statistically informative features, while lexical richness, syntactic complexity, and certain acoustic measures show weaker or non-significant separation.

![Speech Feature Significance Ranking](assets/Speech%20Feature%20Significance%20Ranking.png)

This ranking reinforces Cadence’s emphasis on **temporal structure and speech organization** as core signals, rather than relying exclusively on surface-level lexical counts.

---

## Predictive Modeling and Evaluation

An interpretable modeling pipeline is implemented using scikit-learn, consisting of:

* Mean imputation for missing values
* Feature standardization
* Logistic regression for binary classification

This design prioritizes transparency and coefficient interpretability over black-box performance.

Inspection of learned coefficients reveals that lexical features, pronoun usage, and fundamental frequency contribute most strongly to model predictions, while pause-related features act as stabilizing temporal signals.

![Logistic Regression Feature Coefficients](assets/Logistic%20Regression%20Feature%20Coefficients.png)

Model evaluation includes ROC analysis and standard classification metrics. The logistic regression model achieves strong discriminative performance (ROC AUC ≈ 0.92), demonstrating that interpretable models can perform competitively when paired with well-shaped speech-derived features.

![Receiver Operating Characteristic (ROC) Curve](assets/Receiver%20Operating%20Characteristic%20(ROC)%20Curve.png)

---

## Longitudinal Cognitive Trajectory Modeling

Beyond cross-sectional classification, Cadence explicitly models **cognitive trajectories over time** by estimating predicted MMSE-aligned scores across repeated speech interactions.

Individual-level trajectory plots illustrate how predicted cognitive scores evolve for each participant, revealing heterogeneous progression patterns, non-linear decline, and visit-to-visit variability that are not observable from single-timepoint predictions.

![Individual Cognitive Trajectories Over Time](assets/Individual%20Cognitive%20Trajectories%20Over%20Time.png)

### Cohort-Level Trends

Aggregated trajectories highlight divergent longitudinal trends between cohorts. Control participants exhibit relatively stable average trajectories across visits, while the dementia cohort shows a pronounced downward trend in predicted cognitive scores.

![Average Cognitive Trajectories by Cohort](assets/Average%20Cognitive%20Trajectories%20by%20Cohort.png)

This trajectory-based framing reflects Cadence’s core design philosophy:  
**tracking change over time**, rather than producing static classifications.

---

## Why This Matters

Cognitive decline is gradual, heterogeneous, and often missed until late stages.

Cadence demonstrates that:

- speech can act as a passive, repeatable monitoring signal  
- longitudinal modeling surfaces change earlier than episodic screening  
- timing and organization encode more signal than vocabulary alone  

---

## Usage

The analysis notebook can be run end-to-end to reproduce all statistical tests, model evaluations, and longitudinal visualizations.

```bash
jupyter notebook model_analysis.ipynb
```

---

## Status

Cadence is under active development, with the current system demonstrating robust longitudinal signal extraction from speech across both structured tasks and naturalistic long-form conversation.

Ongoing work focuses on expanding longitudinal depth, improving robustness to speaker and recording variability, and refining individualized baselining to increase sensitivity to subtle within-subject change.

In clinical research and pharma trial settings, this approach can support high-frequency monitoring of cognitive trajectories to evaluate treatment response and disease progression alongside amyloid-beta–targeting therapies such as lecanemab and donanemab.

---

## Data and Privacy

All data used in this repository is synthetic or anonymized. No raw audio, transcripts, or personally identifiable information are included.

---

## Intellectual Property

© 2026 Cadence. All rights reserved.

This repository is made public for demonstration and evaluation purposes only.
No license is granted for use, modification, or redistribution of the code, methods, or system design.

---
