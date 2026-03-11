# Physics-Informed-GP-Biogas-Yield-Prediction 🌱⚙️

## 🚀 Project Overview
Predicting bio-energy production is notoriously difficult due to highly non-linear biological dependencies (temperature, pH, microbial kinetics) and the frequent reality of **extreme data scarcity**. Standard "black-box" deep learning models often fail in these environments, severely overfitting or hallucinating physically impossible yields.

This project introduces a **"Grey Box" Physics-Informed Gaussian Process (PIGP) model** to predict and optimize biogas yield from a mixture of food waste and weed biomass. By mathematically embedding biological laws directly into the model's covariance kernel, the algorithm achieves an exceptional balance of theoretical constraints and data-driven flexibility.

## 🧠 The Physics-Informed Architecture
The core innovation of this repository is the custom `PhysicsInformedBioEnergyKernel`. It combines three distinct components, balanced by a tunable weight parameter ($w = 0.4$):

1. **Data-Driven Component (RBF Kernel):** Captures residual patterns and unknown interactions.
2. **Physics-Informed Component (Domain Kernel):** Restricts the model using strict biological and thermodynamic laws.
3. **White Noise Component:** Accounts for sensor and measurement uncertainty.



### Encoded Domain Knowledge
To prevent the model from making physically impossible predictions, the kernel encodes four specific biological constraints:
* **Monod Kinetics:** Models substrate saturation using Volatile Solids (VS), ensuring growth rates plateau naturally. 
* **Arrhenius Equation:** Captures thermal activation energy, using Total Solids (TS) as a proxy for bioreactor operating temperature.
* **pH-Activity Coupling:** Enforces a sharp drop in biological activity outside the optimal neutral window (pH 6.8 - 7.2).
* **Microbial Lifecycle:** Maps production across Lag, Exponential, Stationary, and Decline phases based on elapsed time.

## 📊 Performance & Results
Despite being trained on an extremely small dataset (only 40 samples), the PIGP model vastly outperformed standard standard machine learning kernels by remaining physically grounded.

* **Training $R^2$:** 1.0000
* **Testing $R^2$:** 0.9992
* **Mean Absolute Error (MAE):** 0.5947
* **Robustness:** 5-fold cross-validation confirmed stability ($R^2 = 0.9988 \pm 0.0011$).

### 🎯 The "Goldilocks" Optimal Recipe
Using a Lower Confidence Bound (LCB) optimization strategy (Maximize Yield - 0.5 * Uncertainty), the model mapped the optimization landscape to find the perfect, stable feedstock balance:

* **Food Waste:** `49%`
* **Weed Biomass:** `51%`
* **Predicted Yield:** `164.57 cm³/day`
* **95% Confidence Interval:** `[162.58, 166.55] cm³/day`

## 💡 Strategic Advantages
* **Data Efficiency:** Achieves near-perfect accuracy where deep learning fails due to small n-counts.
* **Safety First:** Predictions are bounded by physics; it cannot hallucinate yields.
* **Explainability:** Every prediction can be traced back to its kinetic, thermal, or temporal root cause.

## 📂 Generated Artifacts
When you run the notebook, it generates several analytical visualizations:
* `physics_functions.png` — Domain physics visualization
* `pigp_predictions.png` — Predicted vs Actual plots
* `kernel_comparison.png` — PIGP vs standard kernel comparison
* `residual_analysis.png` — Residual distribution & uncertainty
* `physics_feature_analysis.png` — Physics feature correlations
* `optimization_landscape.png` — Yield & uncertainty surfaces

## 🚀 Future Roadmap: The Digital Twin
The ultimate goal of this architecture is to scale it into a **Real-Time Digital Twin**. By integrating live sensor feeds (pH, Temperature) from industrial bioreactors, this model can dynamically control heaters and stirrers, optimizing bio-energy production at an industrial scale without physical risk.
