# MLflow Documentation

## 1. Introduction
MLflow is an **open-source platform for managing the complete lifecycle of machine learning (ML) projects**. It allows tracking experiments, reproducing results, versioning models, and deploying them easily.

> Its purpose is to facilitate collaboration among teams, improve experiment reproducibility, and optimize ML workflows.

---

## 2. Objectives
The main objectives of using MLflow are:  
- Track and organize ML experiments.  
- Facilitate model reproducibility.  
- Manage versions of models and artifacts.  
- Simplify model deployment to production.

---

## 3. MLflow Components

### 3.1 MLflow Tracking
- Allows **experiment tracking**, storing:  
  - **Metrics:** accuracy, loss, etc.  
  - **Parameters:** hyperparameters used.  
  - **Artifacts:** graphs, models, output files.  
- Example: Saving a model’s accuracy along with its parameters.

### 3.2 MLflow Projects
- Enables **packaging ML projects** with all dependencies and scripts.  
- Makes it easy to run the project in different environments without compatibility issues.

### 3.3 MLflow Models
- Handles **model saving and deployment** in multiple formats.  
- Compatible with frameworks like **scikit-learn, TensorFlow, PyTorch, XGBoost**, etc.  
- Example: Save a trained model and load it later for predictions.

### 3.4 MLflow Registry
- Centralized model registry.  
- Features include:  
  - Model versioning.  
  - Approval of models for production.  
  - Full change history tracking.

---

## 4. Installation and Setup
1. Install MLflow via pip:
```bash
pip install mlflow
```
2. Start the tracking server:
```bash
mlflow ui
```

3. Folder structure:
```text
mlruns/
    └── <experiment_id>/
        └── <run_id>/
            ├── metrics/
            ├── params/
            └── artifacts/
```
4. Basic Usage Example

Track an experiment and save a scikit-learn model:
```
```python
# Load data
X, y = load_iris(return_X_y=True)
X_train, X_test, y_train, y_test = train_test_split(X, y)

# Experiment
with mlflow.start_run():
    model = RandomForestClassifier()
    model.fit(X_train, y_train)
    accuracy = model.score(X_test, y_test)
    mlflow.log_metric("accuracy", accuracy)
    mlflow.sklearn.log_model(model, "model")
```

5. Advantages and Disadvantages

Advantages:

Experiment reproducibility.

Model and artifact versioning.

Facilitates team collaboration.

Disadvantages:

Initial learning curve.

Complex setup in large environments.

6. Simplified MLflow Diagram
```text
             +-----------------+
             |   Experiment    |
             +-----------------+
                     |
          +----------+----------+
          |                     |   
 +----------------+      +----------------+
 | MLflow Tracking|      | MLflow Projects|
 +----------------+      +----------------+
          |
 +----------------+
 | MLflow Models  |
 +----------------+
          |
 +----------------+
 | MLflow Registry|
 +----------------+
```