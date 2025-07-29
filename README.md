# 🧠 ML Regression Model with CI/CD Pipeline & AWS S3 Deployment

## 📌 Project Overview

This project demonstrates a complete Machine Learning workflow for training, fine-tuning, and deploying a **regression model**. The final trained model is automatically uploaded to an **AWS S3 bucket** using a robust **CI/CD pipeline**.

---

## 🚀 Features

- 📊 Trains a regression model on input data  
- 🧪 Performs hyperparameter tuning to boost performance  
- ✅ Saves and serializes the best model  
- 🔁 CI/CD integration for automation  
- ☁️ Automatically uploads model to AWS S3  
- 🔐 Secure AWS credential handling

---

## 🧰 Tech Stack

- **Language**: Python  
- **ML Library**: scikit-learn / XGBoost  
- **CI/CD**: GitHub Actions  
- **Cloud**: AWS S3 for model storage  
- **Environment Management**: `venv` 

---


---

## 🧪 Training & Fine-Tuning

1. **Load Dataset** from CSV or external sources.  
2. **Preprocess Data** – handle nulls, encoding, scaling, etc.  
3. **Train Model** using regression algorithms like LinearRegression, XGBoostRegressor.  
4. **Fine-Tune** using GridSearchCV or RandomizedSearchCV.  
5. **Save the Best Model** using `joblib` or `pickle`.

```bash
python scripts/train.py

⚙️ CI/CD Pipeline
🔄 Automated Workflow
Triggered on every git push or pull request to the main branch

Runs training, testing, and packaging

Uploads best_model.pkl to a specified S3 bucket

✅ GitHub Actions Workflow (.github/workflows/model_deploy.yml)
yaml
Copy
Edit
name: ML Model Training & Deployment

on:
  push:
    branches: [main]

jobs:
  train-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'

      - name: Install Dependencies
        run: pip install -r requirements.txt

      - name: Train Model
        run: python scripts/train.py

      - name: Upload to S3
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_DEFAULT_REGION: "ap-south-1"
        run: |
          aws s3 cp models/best_model.pkl s3://your-bucket-name/model/
