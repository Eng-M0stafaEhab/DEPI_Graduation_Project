# DEPI_Graduation_Project

## Sales Forecasting and Demand Prediction

This repository hosts the code and documentation for a deep learning project focused on predicting customer next-action events (e.g., view, cart, purchase) in an online cosmetics retail environment. By analyzing sequences of user behavior, the goal is to develop a proactive system for identifying high-value users and mitigating customer churn in real-time.

The core solution is a Hybrid Convolutional Neural Network (CNN) and Bidirectional Gated Recurrent Unit (BiGRU) model, selected for its superior ability to capture both short-term intent and long-term temporal dependencies in the event stream.

---

## 💾 Dataset

The project utilizes a publicly available, real-world dataset.

- **Dataset Name:** Online Cosmetics Dataset  
- **Source:** Kaggle  
- **Source link:** https://www.kaggle.com/datasets/mkechinov/ecommerce-events-history-in-cosmetics-shop  
- **Time Period:** October 2019 to February 2020 (5 months of data)  
- **Scale:** Over 20 million event records  
- **Key Features:** `event_time`, `event_type`, `product_id`, `brand`, `price`

### Data Preprocessing Summary

- **Feature Exclusion:** `user_id`, `category_id`, and `user_session` were excluded to focus on generalized event patterns.  
- **Missing Data Handling:** The `category_code` column was removed due to over 80% missing values (NaN).  
- **Temporal Engineering:** `event_time` was decomposed into granular features (`year`, `month`, `day`, `hour`) for deep time-series analysis.

---

## 🧠 Model Development

### Architecture: Hybrid CNN + BiGRU

The final model is a custom hybrid architecture combining two powerful sequential learning components:

- **CNN Layer:** Used first to extract local, high-level features and short-term patterns from the sequence of user actions (e.g., immediate viewing patterns).  
- **BiGRU Layer:** Processes the features extracted by the CNN, reading the sequence in both forward and backward directions to capture the full temporal context and long-range dependencies of the user session.

This combination yielded the best performance in forecasting the user's next action compared to standalone LSTM, GRU, and CNN models.

---

### Experiment Tracking

All model training runs, hyperparameters, and performance metrics were meticulously tracked using **MLflow** to ensure reproducibility and facilitate effective comparison between the benchmark architectures.

---

## 🚀 Deployment

The model is deployed via a user-friendly interface for immediate practical use.

- **Deployment Tool:** Gradio  
- **Functionality:** Allows users to input a short sequence of recent events.  
  The model processes it in real-time and outputs the predicted next event (e.g., purchase) along with a confidence score.

---

## 💰 Business Implications

The predictive capability of this model is directly linked to customer retention and revenue optimization.

- **Proactive Churn Mitigation:**  
  The model serves as an early-warning system by flagging users whose predicted next action falls below the 'purchase' probability threshold, indicating a high risk of churn.

- **Targeted Intervention:**  
  This real-time identification enables immediate personalized marketing actions (e.g., specialized discounts, personalized content recommendations based on favorite brands like *irisk* or *runail*) to re-engage the customer before they are lost.

- **Increased CLV:**  
  By improving customer retention rates, the model provides a quantifiable return on investment by maximizing Customer Lifetime Value (CLV) and reducing costly customer acquisition spend.

---

## 🛠️ Future Work

To further enhance the model's performance and prepare it for enterprise-level scale, the following improvements are planned:

- **Feature Enrichment:**  
  Integrate Embedding Layers for `user_id` and `user_session` to allow the model to learn and account for individual user and session biases.

- **External Context Integration:**  
  Incorporate external data such as promotional schedules and seasonal economic indicators to improve predictive accuracy, particularly during volatile shopping periods.

- **Scalable Deployment:**  
  Migrate the Gradio deployment to a robust microservice architecture (e.g., using Flask/FastAPI with Docker) to support high-volume, asynchronous, and concurrent real-time inference requests.
