# Capstone Report — Machine Learning Track

- **Author:** Van Khanh Tran
- **Lane:** Machine Learning
- **Repo:** [https://github.com/vkhanht1/Flyrank-internship](https://github.com/vkhanht1/FlyrankAI-internship)
- **Date:** September 2026

## 0. Abstract
This study investigates how machine learning can accurately forecast directional search volume trends to optimize content publishing workflows. Utilizing the FlyRank production dataset comprising historical search metrics, we applied a gradient-boosted decision tree methodology to evaluate feature importance and rank optimization targets. The model achieves a significant lift in precision compared to naive baselines on out-of-time validation splits. Ultimately, the output serves as a decision-support queue for content strategists to prioritize high-impact SEO updates.

## 1. Problem framing
This project supports the decision of content editors and SEO strategists in allocating scarce editorial resources. The unit of analysis is the individual web page evaluated over a structured time window. The output is a risk-scored and ranked action queue indicating which pages require immediate metadata optimization or content refreshment. A false positive results in wasted editorial effort, while a false negative misses an opportunity to intercept downward traffic trends. Machine learning helps by synthesizing multi-dimensional performance signals at scale, far exceeding manual tracking capacities.

## 2. Data safety
We utilized production search data releases from the FlyRank environment, focusing on aggregated metrics such as impression counts, click-through rates, and historical rankings. Columns containing direct user identifiers or private client names were strictly excluded to ensure complete public safety. Special care was taken to prevent data leakage by isolating label-derived fields (e.g., future trend indicators) from feature sets, using pseudonymous IDs solely for entity grouping. No client-identifying information or private queries exist within the `work/` directory.

## 3. Baseline
To establish a rigorous comparison, we built a transparent heuristic baseline based on trailing 30-day moving averages of traffic change. This baseline represents a fair, standard industry approach that assumes past trajectory continues linearly. Our evaluation confirms that the machine learning model outperforms this baseline on the same validation split, demonstrating superior discrimination and lower error rates.

## 4. Model / analysis
We implemented a gradient-boosted classification and ranking framework suitable for tabular search telemetry data. The feature list includes historical impression velocity, click-through rate variance, and structural metadata flags, while omitting volatile short-term noise variables. The target variable is defined as the directional traffic shift exceeding a defined stability threshold over a forward-looking evaluation window.

## 5. Evaluation
Data was split using a time-aware validation strategy to prevent temporal leakage and simulate real-world deployment conditions. Evaluation metrics prioritize Area Under the ROC Curve (AUC) and Precision@K lift over the base rate. Error analysis indicates that model misclassifications primarily occur during sudden, unpredictable algorithm updates or macro-seasonality shifts.

## 6. Interpretation
The model successfully isolated key drivers of search performance, highlighting content staleness and internal linking gaps as primary predictors of traffic decline. Feature importance analysis confirms that impression velocity shifts serve as leading indicators. Negative results regarding superficial metadata tweaks were also noted, providing valuable guardrails against ineffective optimization efforts.

## 7. Recommendation
The ranked action queue supports three core interventions: metadata optimization for declining pages, content refreshing for stale assets, and technical latency audits. A FlyRank editor can review this queue daily to triage high-priority tasks. These insights are strictly decision-support tools and should be interpreted with an awareness of external search engine volatility.

## 8. Reproducibility
To re-run the entire analysis from a fresh clone, execute the following commands in the repository root:
```bash
pip install -r requirements.txt
python work/scripts/run_pipeline.py
```

## Acknowledgments & Data Credit

This project uses data from [flyrank.ai](https://flyrank.ai).
