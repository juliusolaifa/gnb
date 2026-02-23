# 📘 PAPER 1  
# Geometric–Negative Binomial Regression for Two-Regime Count Processes

---

## 1️⃣ Core Objective

This paper answers the following foundational questions:

- Why does this model need to exist?
- How is it mathematically different from:
  - Negative Binomial regression?
  - Zero-inflated models?
  - Finite mixture NB models?
- Is the model identifiable?
- How is it estimated?
- What are its asymptotic properties?
- What new interpretable quantities does it provide?
- What happens at the boundary case $\alpha = 1$?

If this paper is done correctly, later extensions (discriminant analysis, penalized estimation, decision theory) become natural consequences.

---

# 2️⃣ Introduction & Motivation

## Scientific Problem

Many biological and biomedical count processes reflect **two persistence regimes**:

- **Transient accumulation** (rapid termination)
- **Persistent accumulation** (heterogeneity-driven growth)

Classical models assume a *single persistence structure*.

| Model | Assumes |
|-------|---------|
| Poisson | No heterogeneity |
| Negative Binomial | Single heterogeneity structure |
| Finite mixture NB | Multiple means, same mechanism |
| ZIP/ZINB | Structural zeros |
| **GNB (this paper)** | Mechanistic persistence separation |

### Key Clarifications

- This is **not** a zero-inflation model.
- This is **not** merely a mixture of two NB models.
- This is a **mechanistic decomposition of persistence**.

---

# 3️⃣ Model Formulation

We define a two-regime count process:

$$
Y_i \mid Z_i =
\begin{cases}
\text{Geom}(p_i), & Z_i = 0 \\
\text{NB}(\alpha, p_i), & Z_i = 1
\end{cases}
$$

Latent regime indicator:

$$
Z_i \sim \text{Bernoulli}(\omega_i)
$$

Regression structure:

$$
\mu_i = \exp(x_i^\top \beta)
$$

$$
\omega_i = \text{logit}^{-1}(z_i^\top \gamma)
$$

Mean–probability relationship:

$$
p_i = \frac{\alpha}{\alpha + \mu_i}
$$

### Parameterization Notes

- The geometric distribution is defined as NB with $\alpha = 1$.
- Support convention must be explicitly stated.
- If $\alpha = 1$, both regimes coincide → mixture degeneracy.
- This creates a **boundary identification problem**.

---

# 4️⃣ Likelihood and Identifiability

Marginal likelihood:

$$
f(y_i) =
(1 - \omega_i) f_{\text{Geom}}(y_i; p_i)
+
\omega_i f_{\text{NB}}(y_i; \alpha, p_i)
$$

You must establish:

- Identifiability of $\alpha$
- Identifiability of $\beta$
- Identifiability of $\gamma$
- Degeneracy when $\alpha = 1$

When:

$$
\alpha = 1
$$

the two regimes collapse → nonstandard boundary behavior.

---

# 5️⃣ EM Algorithm

## E-Step

$$
\tau_i^{(t)} =
\Pr(Z_i = 1 \mid Y_i = y_i; \theta^{(t)})
$$

## M-Step

- Weighted logistic regression update for $\gamma$
- Numerical update for $\beta$
- Profile or direct maximization update for $\alpha$

Must include:

- Complete-data log likelihood
- Score functions
- Hessian structure

---

# 6️⃣ Asymptotic Theory

Interior case ($\alpha > 1$):

- Consistency of MLE
- Asymptotic normality

Boundary case:

$$
H_0: \alpha = 1
$$

Likelihood ratio test follows Self & Liang (1987):

$$
0.5\chi^2_0 + 0.5\chi^2_1
$$

---

# 7️⃣ Variance Decomposition

Mean:

$$
E[Y_i] = \mu_i
$$

Variance decomposes into:

- Within-regime dispersion
- Between-regime mixing variance

Define interpretable quantity:

## Persistence Ratio

$$
\text{Persistence Ratio} =
\frac{\text{Between-regime variance}}
{\text{Total variance}}
$$

---

# 8️⃣ Simulation Study

Data generated under:

- True GNB
- NB misspecification
- ZINB misspecification

Metrics:

- Bias
- RMSE
- Coverage probability
- AIC/BIC recovery
- Regime recovery accuracy

---

# 9️⃣ Real Data Application

Potential applications:

- Pathogen burden
- Seizure recurrence
- Hospital readmission
- RNA-seq gene counts

Demonstrate:

- Estimated persistence parameter $\alpha$
- Interpretation of $\gamma$
- Biological implications of regime separation

---

# 🚀 Summary

This paper establishes:

- A mechanistic two-regime count model
- Boundary-aware asymptotic theory
- Identifiable parameter structure
- Interpretable persistence metrics
- A foundation for discriminant and penalized extensions
