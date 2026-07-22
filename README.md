# FlyRank SEO Machine Learning Pipeline

[![Deployed Research Paper](https://img.shields.io/badge/Deployed_Paper-GitHub_Pages-blue?style=for-the-badge&logo=github)](https://ak8x6.github.io/flyrank-seo-ml-pipeline/)

An end-to-end Machine Learning pipeline built to predict organic search traffic decay for massive enterprise SEO portfolios. This project was developed during the **FlyRank ML Internship**, processing **79 million rows** of anonymized production search data. 

The resulting model successfully identifies and prioritizes "stale" content at high risk of traffic loss, providing SEO editorial teams with an automated, data-driven action playbook.

---

## 📊 The Project at a Glance
- **The Problem:** Managing SEO at scale leads to content sprawl. Without intervention, historical high-visibility content loses its competitive edge, leading to catastrophic traffic decay.
- **The Solution:** A Random Forest classifier that learns the non-linear relationship between content staleness (`days_since_last_update`) and engagement (`impressions_90d`, `ctr`) to flag at-risk URLs.
- **The Result:** The model achieved a **Precision@50 of 0.78** on a strict out-of-sample grouped split, beating hand-written deterministic baselines by 22 points. 

## 🛠️ Key Methodology & Techniques
This pipeline was built with a strict focus on "honest" Machine Learning practices, guarding against common industry pitfalls:
* **Data Contracts:** Verified massive datasets via DuckDB, establishing strict assumptions about GA4 tracking gaps and overlapping time windows.
* **Feature Engineering:** Extracted trailing 30-day performance metrics and content metadata without relying on future or target-derived data.
* **Leakage Auditing:** Deliberately hunted for and eliminated data leakage. Ensured no target labels or product-decision flags snuck into the training set.
* **Honest Validation (GroupShuffleSplit):** Abandoned naive random splits (which artificially inflate scores by memorizing domain traffic) in favor of grouping by `client_id` to ensure true out-of-sample generalization.
* **Action Playbooks:** Translated raw model probabilities into a prioritized queue of specific, human-readable actions (e.g., `expand_and_refresh`, `review_ctr`), complete with strict "NO-GO" automation rules.

## 💻 Tech Stack
- **Languages:** Python, SQL
- **Libraries:** `scikit-learn`, `pandas`, `numpy`, `matplotlib`, `duckdb`
- **Deployment:** GitHub Pages (Static Research Paper)
- **Environment:** Google Colab, Jupyter Notebooks

## 📂 Repository Structure
- `docs/index.html`: The fully deployed **Research Paper** summarizing the methodology, findings, and recommendations.
- `work/notebooks/`: Contains the complete, executed pipeline:
  - `w01_duckdb_hello_world.ipynb`: Data warehouse connection and exploratory querying.
  - `w02_labels_and_features.ipynb`: Feature extraction and label definition.
  - `w03_data_contract.ipynb`: Data validation, assumptions, and timeline verification.
  - `w04_baseline_score.ipynb`: Deterministic baseline creation for honest model comparison.
  - `w05_model.ipynb`: Random Forest training, evaluation, and feature importance analysis.
  - `w06_validation_audit.ipynb`: Strict leakage auditing and methodology stress-testing.
  - `w07_action_playbook.ipynb`: Generation of the prioritized editorial queue.
  - `capstone.ipynb`: The finalized research code and presentation showcase.
- `work/outputs/`: The generated action playbook CSVs.
- `work/figures/`: Exported charts and feature importance graphs used in the paper.

---

## 👨‍💻 Author
**Ahmad Kassem**  
*(Completed as part of the FlyRank AI ML Internship, 2026)*

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
