# 📰 Project: Fake News Detection

![App Interface](app-interface.jpeg)
![Training Results](training-results.jpeg)
![Terminal Output](terminal-output.jpeg)

---

## 🛠️ Codebase Overview

### 1. `app.py`
Builds the reactive frontend UI utilizing **Streamlit**. It loads the model, caches resources to prevent redundant training, displays status messages, accepts raw user input via a text area, and outputs the prediction with clear, color-coded styling based on the classification.
* **Core UI Components:** Custom titles, descriptions, spinner states, toasts for user feedback, metrics panels, and semantic status banners (`st.error` for Fake, `st.success` for Authentic).

### 2. `model_pipeline.py`
Handles the backend data science workflow:
* **`get_real_dataset()`:** Downloads the `emniyetm/fake-news-detection-datasets` dataset from Kaggle via `kagglehub`, extracts the subfolder files, aligns them into a single pandas DataFrame, and pre-cleans the text feature sets.
* **`train_fake_news_model()`:** Sets up an 80/20 train-test split, extracts numerical features using a TF-IDF vectorizer, trains a **Passive-Aggressive Classifier** (max iterations = 50), and reports model performance metrics.
* **`predict_news_veracity()`:** Preprocesses single input strings through the sanitization pipeline, vectorizes them, and runs model predictions to return the final classification verdict.

### 3. `text_cleaner.py`
A modular text sanitization script. It pre-compiles regex patterns (HTML cleaner, URL cleaner, non-alphabetic character cleaner, and duplicate whitespace cleaner) to run highly optimized string operations across large Pandas DataFrames without compiling regex on every iteration.

---

## ⚙️ Installation & Setup

### Prerequisites
* Python 3.10+
* A Kaggle API token (if using `kagglehub` for dataset downloading, ensure your credentials are set up locally).

### 1. Clone the Repository
```bash
git clone https://github.com/Diyaasrivastava43/Fake-News-Detector.git
cd Fake-News-Detector
```

### 2. Install Dependencies
Ensure you have the required libraries installed:
```bash
pip install streamlit pandas scikit-learn kagglehub
```

### 3. Run the Streamlit Application
Start the development server:
```bash
python -m streamlit run app.py
```

After starting, the console will print your access URLs:
```plaintext
Local URL: http://localhost:8501
Network URL: http://10.140.173.206:8501
```

---

## 🔍 How It Works

1. **Bootstrapping the Pipeline:** When you launch the web application, the backend automatically verifies and downloads the Kaggle dataset if it isn't already present locally.
2. **Training Phase:** The pipeline parses the CSV files, merges and shuffles ~45,000 articles, cleanses the raw text, vectorizes it using TF-IDF, and trains the Passive-Aggressive Classifier model.
3. **Interactive Testing:** Paste any news headline or full article body inside the text box. The model processes the input text through the sanitization pipeline, transforms it using the pre-fitted TF-IDF matrix, and instantly outputs a classification verdict.
