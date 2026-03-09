# Deep Transfer Learning (SDTL) for Cross-Scenario SOH Estimation of Lithium-Ion Batteries

## I. Introduction

With the explosive growth of electric vehicles and energy storage systems, accurate estimation of the **State of Health (SOH)** of lithium-ion batteries is crucial for ensuring system safety and extending battery lifespan.

However, in practical applications, we face two major challenges:

- **Complex and Variable Environment**: Different cathode materials (such as NCM, NCA), dramatic fluctuations in ambient temperature, and diverse charge-discharge protocols.
- **Data Silos and Sample Scarcity**: New batteries have extremely limited data during their early service period, while traditional deep learning models often require massive labeled data to achieve good generalization ability.

To address these challenges, a paper published in the prestigious journal *Journal of Power Sources* titled ***Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials*** presents the latest research findings: a **Deep Transfer Learning (SDTL)** method based on a **Self-Attention Mechanism**.

## II. SDTL Framework

The study proposes an efficient SDTL system with three core components: **feature extraction**, **pre-training**, and **fine-tuning**:

<p align="center">
  <img src="/docs/public/fig1.png" style="width: 100%; margin: 0 auto; display: block;">
</p>
<p align="center" style="color: grey">System Architecture of Deep Transfer Learning (SDTL) Based on Self-Attention Mechanism</p>

### 1. Multi-Source Health Indicator (HI) Extraction

The researchers extracted **18 health indicators** from charge voltage/current, discharge voltage/current, and incremental capacity (IC) curves. By using **Pearson Correlation Coefficient (PCC)** to filter out features highly correlated with SOH (such as HI3, HI5, HI11, etc.), they ensured the physical interpretability and representation capability of the input data.

<p align="center">
  <img src="/docs/public/fig2.png" style="width: 100%; margin: 0 auto; display: block;">
</p>
<p align="center" style="color: grey">Pearson Correlation Coefficient (PCC) Analysis Between Extracted Health Indicators (HIs) and SOH</p>

### 2. Self-Attention Mechanism

Unlike traditional RNN or LSTM, SDTL employs a **Multi-Head Self-Attention Mechanism**. It captures global dependencies at different positions in time series and automatically assigns weights to more critical degradation features, enabling more accurate identification of battery degradation patterns under different operating conditions.

<p align="center">
  <img src="/docs/public/fig3.png" style="width: 100%; margin: 0 auto; display: block;">
</p>
<p align="center" style="color: grey">Multi-Head Self-Attention Module Architecture Diagram</p>

### 3. Deep Transfer Learning

- **Pre-training (Offline)**: Utilizing large amounts of historical battery data (source domain) for pre-training, enabling the model to learn general battery degradation patterns.
- **Fine-tuning (Online)**: For new battery tasks (target domain), only the first 10% of early-cycle data is required to complete online adaptation. By freezing the lower-layer feature extraction layers and updating only the output layer parameters, fast and cost-effective cross-scenario transfer is achieved.

## III. Experimental Validation

To verify the generalization performance of SDTL, the researchers conducted extremely rigorous experimental tests:

<p align="center">
  <img src="/docs/public/fig8.png" style="width: 100%; margin: 0 auto; display: block;">
</p>
<p align="center" style="color: grey">SOH Estimation Results of SDTL Model on Experimental Battery Data</p>

- **Comprehensive Dataset Coverage**: Includes self-built NCM battery datasets (1C/2C rates) and publicly available NASA NCA battery datasets (covering 24°C and 4°C ambient temperatures).
- **Performance Results**: Experimental results show that even under challenging conditions such as low temperature (4°C) and high discharge rates, SDTL demonstrates extremely high estimation accuracy and robustness.
- **Comparative Advantages**: Compared to mainstream deep learning algorithms and other transfer learning methods, SDTL exhibits clear advantages in small-sample scenarios, eliminating the high cost of training models from scratch.

<p align="center">
  <img src="/docs/public/fig9.png" style="width: 100%; margin: 0 auto; display: block;">
</p>
<p align="center" style="color: grey">Comparison of Prediction Performance Between SDTL and Mainstream Models (CNN-LSTM, GRU, ResNet)</p>

## IV. Conclusion

The paper's contributions are primarily reflected in:

- **Efficiency**: Quick online adaptation can be achieved with only 10% of the data.
- **Broad Applicability**: Can handle different cathode materials (NCM vs NCA) and environmental temperature variations.
- **Engineering Value**: Provides a practical, lightweight, and high-precision SOH online estimation solution for BMS (Battery Management Systems).

---

## Reference Information

- **Title**: Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials, ambient temperature and charge-discharge protocols
- **Journal**: Journal of Power Sources (2025)
- **DOI**: 10.1016/j.jpowsour.2025.237503
- **Link**: [https://doi.org/10.1016/j.jpowsour.2025.237503](https://doi.org/10.1016/j.jpowsour.2025.237503)
