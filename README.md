# MindGuard AI: Behavioral Analysis System

**MindGuard AI** is an AI-powered system designed to detect digital distraction and smartphone addiction risk through behavioral telemetry analysis. This project was developed as a final year project to map raw Android usage patterns to clinical risk categories using the **Smartphone Addiction Scale (SAS)**.

## 🚀 Project Overview
The system aggregates low-level device logs (app launches, screen events, session durations) and uses supervised machine learning to categorize user behavior into three risk levels:
- **Normal**: Healthy digital habits.
- **Risk**: Emerging patterns of distraction or overuse.
- **High Risk**: Compulsive usage patterns aligning with SAS addiction markers.

## 🛠️ Tech Stack
- **Language**: Python 3.x
- **AI Framework**: Scikit-Learn (Random Forest & Isolation Forest)
- **Data Engineering**: Pandas, NumPy
- **Visualizations**: Matplotlib, Seaborn
- **Development Environment**: Android Studio / PyCharm

## 📋 Project Pipeline
To run the full AI lifecycle, execute the scripts in the following order:

1. **`synthetic_data_generator.py`**: Generates 200 days of simulated behavioral logs across diverse user profiles (Healthy, Risk, Addictive).
2. **`dataset_generation.py`**: Performs feature engineering on raw logs and applies the SAS weighted scoring engine to generate ground-truth labels.
3. **`model_training.py`**: 
    - Trains a Supervised **Random Forest Classifier** for risk prediction.
    - Trains an Unsupervised **Isolation Forest** for sudden distraction (anomaly) detection.
    - Generates academic plots (`confusion_matrix.png`, `feature_importance.png`).
4. **`inference_engine.py`**: The live analysis engine that processes behavioral data and provides clinical recommendations.

## ⚠️ Environment Setup (NumPy Fix)
This project requires a stable environment. Due to breaking changes in NumPy 2.0, please ensure you use a compatible version:

```bash
pip uninstall -y numpy pandas scikit-learn
pip install "numpy<2.0" pandas scikit-learn matplotlib seaborn
```

## 📊 Research Metrics
The model evaluation produces two key artifacts for research documentation:
- **Confusion Matrix**: Visualizes the model's accuracy across all three SAS categories.
- **Feature Importance**: Ranks the behavioral markers (e.g., night usage vs. pickup frequency) that most contribute to addiction risk.

## 📁 Folder Structure
- `/data`: Raw CSV logs from device.
- `/models`: Serialized AI assets (`.pkl`).
- `/plots`: Academic validation plots.
- `MindGuard_Feature_Dataset.csv`: The final engineered training set.
