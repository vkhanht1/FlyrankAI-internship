# FlyRank Capstone — Machine Learning Track

## 1. Overview & Audience
- **What it does:** An end-to-end machine learning pipeline and predictive ranking system designed to forecast directional search volume trends and prioritize editorial content updates.
- **For whom:** Content editors, SEO strategists, and data science reviewers seeking to automate resource allocation based on data-driven telemetry.

## 2. Setup & Reproduction Guide (For Strangers)
To reproduce this environment and run the pipeline locally:
1. Clone the repository:
   ```bash
   git clone [https://github.com/vkhanht1/Flyrank-internship.git](https://github.com/vkhanht1/Flyrank-internship.git)
   cd Flyrank-internship

```

2. Install dependencies:
```bash
pip install -r requirements.txt

```


3. Run the specification and model pipeline script:
```bash
python work/slot_specification.py

```



## 3. Usage Examples

* **Generating the Triage Queue:** Execute the scoring module to output a risk-scored CSV file used by content teams to target declining pages.
* **Viewing the Live Report:** Access the live published site at https://vkhanht1.github.io/FlyrankAI-internship/

## 4. Architecture Sketch

```text
[FlyRank Production Data] 
       │
       ▼
[Data Cleaning & Leakage Prevention]
       │
       ▼
[Gradient-Boosted Ranking / Tree Model]
       │
       ▼
[Daily Risk-Scored Editorial Action Queue]

```

## 5. V2 Evaluation Results

* Evaluated on out-of-time validation splits to prevent look-ahead bias.
* Achieved a significant lift in Precision@K and AUC compared to the heuristic trailing 30-day moving average baseline.

## 6. Limitations List

* **Macro-algorithm Shifts:** The model experiences temporary error rate spikes during unexpected search engine algorithm changes.
* **Data Granularity:** Limited to aggregated impression and click metrics to ensure strict privacy compliance.

## 7. Transparency Diligence (AI Fluency)

*I built this project with the assistance of Claude as an AI collaborative partner, and I have personally reviewed, tested, and verified all code implementations, data sanitation steps, and evaluation metrics myself.*

# Project Retrospective: From Week 1 to Capstone Launch

## 1. What I Set Out to Do (Week 1 Vision)
When I started this Machine Learning track at FlyRank, my goal was simply to understand how machine learning models move from abstract academic notebooks into production-ready systems. Coming in as a beginner in software engineering and AI, I wanted to build something tangible—a predictive pipeline that could solve a real-world operational bottleneck rather than just chasing high accuracy scores on clean, toy datasets.

## 2. What Actually Changed Along the Way
My initial assumption was that model tuning and algorithm selection would take up 80% of the effort. I quickly learned how wrong I was. 
- **The Data Reality:** The biggest hurdles weren't mathematical; they were structural. Dealing with environment inconsistencies (like resolving NumPy compatibility issues during module execution) and enforcing strict data safety to prevent target leakage took up the bulk of my engineering time.
- **Scoping Down for Impact:** I had to pivot from building an overly complex real-time system to focusing on a robust, batch-oriented daily triage queue. I realized that a simpler, interpretable model that content editors can actually trust and use is infinitely more valuable than a black-box model that performs slightly better statistically.

## 3. The Three Most Transferable Things I Learned
1. **Rigor in Out-of-Time Validation:** I learned never to trust random train-test splits on temporal data. Guarding against data leakage is the single most critical engineering discipline for real-world predictive systems.
2. **Translating Metrics to Business Value:** A high AUC means nothing if the end user (in this case, an SEO strategist) doesn't know what action to take. Framing outputs into an actionable, risk-scored queue bridged the gap between code and human workflow.
3. **Collaborating with AI as a Technical Partner:** Using AI didn't mean letting it do the thinking for me; it meant using it as a sounding board to debug errors faster, question architectural assumptions, and maintain engineering velocity while keeping total ownership of the final code.

## 4. What I Would Build Next
If I were to take this project to the next version (v3), I would integrate an automated feedback loop where human edits on the triage queue are fed back into the training dataset as weak supervision signals, allowing the model to adapt dynamically to shifting editorial priorities.

## Acknowledgments & Data Credit
This project utilizes data and resources provided by [flyrank.ai](https://flyrank.ai).
