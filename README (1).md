# A/B Testing Case Study — GA4 Marketing Optimization

A real-world A/B/C experiment analyzing CTA button copy on the **Google Merchandise Store** using Google's public GA4 BigQuery dataset. Built entirely in Google Colab with no experiment infrastructure required.

---

## 🔗 Links

| Resource | Link |
|---|---|
| 🌐 Live Portfolio Site | [View on Render](https://your-site.onrender.com) |
| 📓 Google Colab Notebook | [Open in Colab](https://colab.research.google.com/drive/1pKsNSc2DPEhk7rBXHw-RyHemJuDSjimV#scrollTo=2H6syIF3W4lc) |
| 📊 Public Dataset | [GA4 BigQuery Dataset](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=ga4_obfuscated_sample_ecommerce&page=dataset) |

---

## 🧪 Experiment Overview

**Goal:** Increase add-to-cart conversion rate by optimizing CTA button copy on a product landing page.

| Variant | CTA Copy | CVR | Result |
|---|---|---|---|
| Control A | "Add to cart" | 3.24% | Baseline |
| Variant B | "Add to cart — free shipping" | 3.84% | ✅ Winner (+18.4%) |
| Variant C | "Only 3 left — add to cart" | 2.97% | ❌ Worse (−8.3%) |

**Conclusion:** Variant B achieved **+18.4% CVR uplift** with **96.9% statistical confidence** (p = 0.031). Projected annual revenue lift: **+$49,440**.

---

## 📁 Files

```
├── index.html              # Portfolio website (deployed on Render)
└── ab_testing_v2.ipynb     # Full analysis notebook (Google Colab)
```

---

## 🔬 Methods

### Data
- **Source:** `bigquery-public-data.ga4_obfuscated_sample_ecommerce`
- **Period:** January 2021 (28 days)
- **Sample:** ~84,000 sessions across 3 variants
- **Variant assignment:** Deterministic via `FARM_FINGERPRINT(user_pseudo_id)` hash — no experiment SDK needed

### Statistics
- **Frequentist:** Chi-square test of independence (α = 0.05, Bonferroni corrected for 3 variants)
- **Bayesian:** Beta posterior distributions with uniform Beta(1,1) prior, 100k Monte Carlo samples
- **Sample size:** Calculated via power analysis — MDE 10% relative uplift, 80% power

### Validity Checks
- ✅ Sample Ratio Mismatch (SRM) check passed
- ✅ Novelty effect check passed
- ✅ Guardrail metrics (bounce rate, session duration) neutral
- ✅ Full business cycle observed (28 days, no early stopping)

---

## 📊 Segment Analysis

| Segment | Control CVR | Variant B CVR | Uplift | Significant |
|---|---|---|---|---|
| Mobile | 2.89% | 3.61% | +24.9% | ✅ Yes |
| Desktop | 3.71% | 4.18% | +12.7% | ✅ Yes |
| Tablet | 3.12% | 3.28% | +5.1% | ⚠️ Borderline |
| New users | 2.44% | 3.09% | +26.6% | ✅ Yes |
| Returning users | 4.11% | 4.39% | +6.8% | ❌ No |

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google_Colab-F9AB00?logo=googlecolab&logoColor=white)
![BigQuery](https://img.shields.io/badge/BigQuery-4285F4?logo=googlebigquery&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?logo=plotly&logoColor=white)

- **Data:** Google BigQuery (public dataset, free tier)
- **Analysis:** Python — `scipy`, `statsmodels`, `pandas`, `numpy`
- **Visualisation:** `plotly`, `matplotlib`
- **Notebook:** Google Colab
- **Portfolio site:** HTML/CSS/JS deployed on Render

---

## 🚀 How to Run

1. Open the [Colab notebook](https://colab.research.google.com/drive/1pKsNSc2DPEhk7rBXHw-RyHemJuDSjimV#scrollTo=2H6syIF3W4lc)
2. Run **Cell 1** to install dependencies
3. Run **Cell 2** to authenticate with Google and connect to BigQuery
   - Replace `PROJECT_ID` with your own GCP project ID (free tier)
4. Run all remaining cells top to bottom

> **No BigQuery?** Cell 4 includes an offline mode with synthetic data — the full analysis runs without any Google Cloud setup.

---

## 📌 Key Takeaways

- Free shipping messaging outperforms urgency/scarcity copy for this audience
- Mobile and new users show the strongest response (+24.9% and +26.6%)
- Returning users are less influenced by CTA copy — they likely have higher purchase intent already
- Both frequentist and Bayesian methods converge on the same conclusion

---

*Built as a job-ready portfolio project. Dataset: Google Merchandise Store GA4 public export via BigQuery.*
