
# Integration of Social Network Analysis Into Educational Data Mining for Predicting Students' Academic Performance

**Author:** Naufal Ghifari Afdhala  
**Contact:** nghifaria@gmail.com  
**Document Type:** Working Paper (2026)  
**Full Paper (PDF):** [Download Working Paper](./Working_Paper_NaufalGhifariAfdhala.pdf)  

---

## Summary

Early prediction of student academic performance is critical for enabling timely, data-driven interventions in higher education institutions. Traditional Educational Data Mining (EDM) models primarily focus on individual Virtual Learning Environment (VLE) interaction logs and assessment histories, often omitting relational student interaction dynamics.

This study proposes a **hybrid predictive framework** that integrates:
1. **VLE Administrative & Behavioral Logs**: Interaction counts, engagement recency, and assessment submission records.
2. **Social Network Analysis (SNA)**: Forum-based graph centrality metrics (`degree_centrality` and `closeness_centrality`).
3. **Temporal Snapshots**: Comparative evaluation across observation windows ($t \le 100$ days vs. $t \le 200$ days).
4. **Explainable AI (TreeSHAP)**: Global and local feature contribution analysis for model transparency.
5. **4-Quadrant Early Warning System (EWS)**: An actionable intervention matrix using an optimized risk threshold ($p \ge 0.35$).

---

## Experimental Results Summary

### 1. Comparative Model Performance (Test Set: N = 5,983)

Evaluations were conducted on the Open University Learning Analytics Dataset (OULAD) using Decision Tree, Random Forest, and XGBoost classifiers trained with Synthetic Minority Over-sampling Technique (SMOTE).

| Observation Period | Algorithm | Accuracy | Precision | Recall | F1-Score |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **Snapshot 1** ($t \le 100$ days) | Decision Tree | 0.6724 | 0.6168 | 0.6106 | 0.6133 |
| | Random Forest | 0.7088 | 0.6541 | 0.6426 | 0.6468 |
| | **XGBoost** | **0.7160** | **0.6628** | **0.6511** | **0.6549** |
| **Snapshot 2** ($t \le 200$ days) | Decision Tree | 0.7383 | 0.6785 | 0.6803 | 0.6793 |
| | Random Forest | 0.7754 | 0.7168 | 0.7163 | 0.7148 |
| | **XGBoost** | **0.7767** | **0.7191** | **0.7179** | **0.7167** |

* **Statistical Validation**: McNemar's test for paired nominal data confirms that XGBoost's performance advantage over Random Forest at Snapshot 2 is statistically significant ($\chi^2 = 14.5000, p = 1.4016 \times 10^{-4}$).
* **Temporal Progression**: Progressing from Day 100 to Day 200 yields a +6.18 percentage point gain in F1-Score for XGBoost, demonstrating the value of accumulating longitudinal behavioral logs.

---

### 2. Feature Importance Analysis (TreeSHAP)

Global feature importance evaluated at Snapshot 2 identifies the following hierarchy:
1. **`days_since_last_click`**: Dominant predictor of student attrition (mean $\vert{}SHAP\vert{} > 3.5$). Prolonged inactivity serves as the primary precursor to withdrawal.
2. **Academic Performance Metrics**: Cumulative assessment weight (`total_weight`) and average scores (`mean_score`) form the second most critical tier.
3. **SNA Centrality Metrics**: `degree_centrality` and `closeness_centrality` provide essential relational signals that refine predictions for borderline cases.

---

### 3. Early Warning System (EWS) Intervention Zoning

Applying a decision threshold of $p \ge 0.35$ establishes an optimal equilibrium between Precision (~90%) and Recall (~90%). Combining predicted risk probabilities with VLE click volume and SNA degree centrality yields four operational intervention zones:

* **Safe Zone** ($N = 2,177$ / $36.39\%$): High VLE interaction, high SNA centrality. Passive monitoring recommended.
* **Critical Risk** ($N = 2,144$ / $35.84\%$): Low VLE interaction, low SNA centrality. Requires urgent direct outreach from academic advisors.
* **Academic Risk** ($N = 847$ / $14.16\%$): Low VLE interaction, high SNA centrality. Student is socially active but struggling with course material. Requires academic tutoring.
* **Isolation Risk** ($N = 815$ / $13.62\%$): High VLE interaction, low SNA centrality. Student is academically active but socially detached. Requires peer group integration.

Out of 5,983 test instances, the pipeline automatically flags 2,462 at-risk students ($41.15\%$) for direct intervention and exports prioritized registries.

---

## Repository Structure

```text
sna-edm-student-performance/
├── Working_Paper_NaufalGhifariAfdhala.pdf    # Full compiled research paper (PDF)
├── main_pipeline.ipynb                        # Complete Kaggle/Jupyter execution notebook
├── README.md                                  # Repository documentation
