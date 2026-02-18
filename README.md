# UCS654-Probability-Density-Functions-Assignment-2

**Name:** Lovepreet Bhatia  
**Roll No:** 102303335  

This repository contains the solution for Assignment 2, which focuses on learning an unknown probability density function of a transformed random variable using a Generative Adversarial Network (GAN).

---

## Dataset

- **Feature used:** NO₂ concentration (`no2`)
- **Source:** [India Air Quality Dataset (Kaggle)](https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data)
- **Total samples after cleaning:** ~430,000
- Missing and negative values removed before processing

---

## Step 1: Transformation

Each NO₂ value `x` is transformed using:

$$z = x + a_r \cdot \sin(b_r \cdot x)$$

| Parameter | Formula | Value |
|-----------|---------|-------|
| r | Roll Number | 102303335 |
| a_r | 0.05 × (r mod 7) | 0.05 |
| b_r | 0.3 × (r mod 5 + 1) | 0.30 |

---

## Step 2: GAN Architecture

**Generator:** `1 → 32 → 64 → 32 → 1` (LeakyReLU activations)  
**Discriminator:** `1 → 32 → 64 → 32 → 1` (LeakyReLU + Sigmoid)

| Hyperparameter | Value |
|----------------|-------|
| Loss Function | Binary Cross Entropy |
| Optimizer | Adam |
| Learning Rate | 0.0002 |
| Beta1 | 0.5 |
| Epochs | 2000 |
| Batch Size | 256 |

---

## Step 3: PDF Estimation

- 10,000 samples generated from trained Generator
- KDE (Kernel Density Estimation) applied to estimate the probability density function

---

## Results

<img width="1389" height="985" alt="image" src="https://github.com/user-attachments/assets/a6cf8d2c-828e-4c7d-b710-65bbba6dc1f1" />

---

## Observations

| Metric | Value |
|--------|-------|
| Final Discriminator Loss | ~1.38 |
| Final Generator Loss | ~0.69 |
| Real z Mean | ~25.05 |
| Generated z Mean | ~22.79 |

- GAN training was stable with no mode collapse observed
- Losses converged close to theoretical equilibrium (log2 ≈ 0.693)
- Generated distribution mean closely matches real distribution mean
- KDE curves of real and generated samples align well
- GAN successfully learned the unknown PDF without any parametric assumption

---

## Conclusion

This assignment demonstrates the use of generative models for learning unknown probability density functions directly from data. The GAN-based approach effectively models the transformed NO₂ concentration values and enables PDF estimation without relying on predefined distributional assumptions.
