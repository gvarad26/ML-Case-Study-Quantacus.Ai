# 📧 Email Campaign Optimizer

An end-to-end Python package to analyze email marketing performance and build a machine‑learning model to maximize click‑through rates (CTR).

---

## 🔍 Overview

`EmailCampaignOptimizer` is a single‑class solution that:

1. **Ingests** raw campaign data (opens, clicks, email metadata).  
2. **Calculates** key metrics (open rate, click rate, click‑to‑open rate).  
3. **Segments** your audience by purchase history, time of day, geography, and more.  
4. **Visualizes** performance across all dimensions (barplots, line charts, heatmaps, scatter plots).  
5. **Engineers** features for modeling (one‑hot encoding, cyclical time features).  
6. **Trains** a Random Forest classifier to predict who will click.  
7. **Estimates** the uplift in CTR by targeting top‑probability users.  
8. **Designs** an A/B test for real‑world validation.  
9. **Predicts** click probabilities on new recipient lists.  

All generated plots are saved as `.png` files in your working directory.

---

## 📂 Folder Structure

    email-campaign-optimizer/
    │
    ├── email_campaign_optimizer.py       # Main class implementation
    ├── email_opened_table.csv            # Raw “opens” events
    ├── link_clicked_table.csv            # Raw “clicks” events
    ├── email_table.csv                   # Campaign metadata (id, text, version, user info…)
    │
    ├── overall_metrics.png               # Saved plot: overall open & click rates
    ├── ctr_by_<segment>.png              # Saved plots: CTR by segment
    ├── ctr_by_type_and_personalization.png
    ├── ctr_by_hour.png
    ├── feature_importance.png
    ├── ctr_improvement.png
    ├── weekday_hour_heatmap.png
    ├── open_vs_click_scatter.png
    ├── purchase_engagement_relationship.png
    │
    └── README.md                         # This file

---

## 🛠️ Installation

1. **Clone the repo**  
       git clone https://github.com/your-username/email-campaign-optimizer.git  
       cd email-campaign-optimizer

2. **Create a virtual environment**  
       python3 -m venv venv  
       source venv/bin/activate

3. **Install dependencies**  
       pip install -r requirements.txt  

   **requirements.txt**  
       pandas  
       numpy  
       matplotlib  
       seaborn  
       scikit-learn  

---

## 🚀 Quickstart

    from email_campaign_optimizer import EmailCampaignOptimizer

    # 1. Initialize
    optimizer = EmailCampaignOptimizer()

    # 2. Load data (assumes CSVs in working directory)
    df = optimizer.load_data(
        opened_file='email_opened_table.csv',
        clicked_file='link_clicked_table.csv',
        email_file='email_table.csv'
    )

    # 3. Compute & visualize overall metrics
    metrics = optimizer.calculate_metrics()

    # 4. Segment analysis (saves per‑segment CTR plots)
    segmented_df = optimizer.analyze_segments()

    # 5. Feature engineering for ML
    email_data = optimizer.engineer_features()

    # 6. Build & evaluate model
    model = optimizer.build_model(email_data)

    # 7. Generate full visualization dashboard
    optimizer.create_visualization_dashboard()

    # 8. Print A/B test design
    optimizer.ab_test_design()

    # 9. Predict on new campaign recipients
    #    (prepare a DataFrame `new_recipients` with same schema)
    results = optimizer.predict_for_new_campaign(new_recipients)
    print(results.head())

---

## 📊 Key Methods

| Method                                           | Description                                                                                  |
|--------------------------------------------------|----------------------------------------------------------------------------------------------|
| `load_data(opened_file, clicked_file, email_file)` | Ingest opens, clicks, and email metadata; annotates `opened` & `clicked` flags.              |
| `calculate_metrics()`                            | Computes total emails, open rate, click rate, click‑to‑open; saves bar chart.                |
| `analyze_segments()`                             | Bins by purchase history & hour, then plots CTR by version, text, weekday, country, etc.     |
| `engineer_features()`                            | One‑hot encodes categorical fields; adds sine/cosine hour features; drops temp columns.      |
| `build_model(email_data)`                        | Trains a Random Forest; prints ROC‑AUC; prints classification report; saves feature importances. |
| `estimate_ctr_improvement(X_test, y_test, y_pred_proba)` | Plots CTR vs. proportion targeted; prints uplift estimates vs. baseline.                      |
| `predict_for_new_campaign(new_data)`             | Applies the trained model to score new recipients; returns sorted DataFrame with probabilities. |
| `ab_test_design()`                               | Prints recommended A/B test setup to validate the model.                                     |
| `create_visualization_dashboard()`               | Orchestrates all plots & metrics into a full dashboard.                                      |

---

## 📈 Sample Output

    Email Campaign Performance Metrics:
    Total emails sent: 50,000
    Emails opened: 28,500 (57.00%)
    Links clicked: 7,200 (14.40%)
    Click-to-open rate: 25.26%

    Cross-validation ROC AUC: 0.7482
    Test set ROC AUC: 0.7625

    Classification Report:
                  precision    recall  f1-score   support
               0       0.92      0.95      0.93     11250
               1       0.71      0.63      0.67      2850

---

## 💡 Future Improvements

- **Hyperparameter tuning** with `GridSearchCV` / `RandomizedSearchCV`.  
- **Alternative models**: XGBoost, Logistic Regression, LightGBM.  
- **NLP analysis** of email copy (token embeddings, sentiment).  
- **Integration** with Mailchimp/SendGrid APIs for live deployments.  
- **Dashboard UI** using Streamlit or Dash for interactive exploration.

---

## 🤝 Contributing

1. Fork the repository  
2. Create a feature branch (`git checkout -b feature/...`)  
3. Commit your changes (`git commit -m "feat: ..."`)  
4. Push to the branch (`git push origin feature/...`)  
5. Open a Pull Request

---

## 👤 Author

**Varad Gorantyal**  
- GitHub: https://github.com/gvarad26
- LinkedIn: https://www.linkedin.com/in/varad-gorantyal-a07520230/

Feel free to reach out with questions, feature requests, or collaboration ideas!
