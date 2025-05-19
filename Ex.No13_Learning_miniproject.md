# Ex.No: 13 Learning – Use Supervised Learning  
### DATE: 13/05/2025                                                                           
### REGISTER NUMBER : 212222040170
### AIM: 
To write a program to train the classifier for Differentiated Thyroid Cancer Recurrence.
###  Algorithm:

1.Data Collection and Preprocessing
2.Identify Target Column
3.Data Splitting
4.Model Training
5.Prediction and Evaluation
6.Visualization

### Program:

"""Thyroid Cancer Recurrence Graphs"""

import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix
import zipfile
import os

# 1. Load and Prepare Data
# Upload ZIP
from google.colab import files
uploaded = files.upload()

# Extract ZIP
zip_filename = list(uploaded.keys())[0]
extract_dir = "thyroid_data"

with zipfile.ZipFile(zip_filename, 'r') as zip_ref:
    zip_ref.extractall(extract_dir)

# Construct the CSV path dynamically after extracting the ZIP
csv_path = os.path.join(extract_dir, "Thyroid_Diff.csv")
df = pd.read_csv(csv_path)

# Data preprocessing
df = df.dropna()
df_encoded = pd.get_dummies(df, drop_first=True)

# Identify Target Column
target_column = None
for col in df_encoded.columns:
    if 'Recur' in col:
        target_column = col
        break

if target_column:
    X = df_encoded.drop(target_column, axis=1)
    y = df_encoded[target_column]

    # Train/Test Split
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

    # 2. Train Model
    model = RandomForestClassifier(random_state=42)
    model.fit(X_train, y_train)
    y_pred = model.predict(X_test)

    # 3. Visualization

    # a. Bar Chart of Predicted Probabilities
    y_pred_proba = model.predict_proba(X_test)[:, 1]  # Probability of class 1 (recurrence)
    df_plot = pd.DataFrame({'Sample': range(len(y_test)), 'Probability': y_pred_proba, 'Actual': y_test})

    plt.figure(figsize=(10, 6))
    sns.barplot(x='Sample', y='Probability', data=df_plot)
    plt.xlabel('Test Sample')
    plt.ylabel('Probability of Recurrence')
    plt.title('Predicted Probability of Thyroid Cancer Recurrence')
    plt.xticks(rotation=90)
    plt.show()

    # b. Confusion Matrix
    cm = confusion_matrix(y_test, y_pred)
    plt.figure(figsize=(8, 6))
    sns.heatmap(cm, annot=True, fmt='d', cmap='Blues')
    plt.xlabel('Predicted Label')
    plt.ylabel('True Label')
    plt.title('Confusion Matrix')
    plt.show()

    # c. Feature Importance
    if hasattr(model, 'feature_importances_'):
        importances = model.feature_importances_
        feature_names = X_train.columns
        df_importance = pd.DataFrame({'Feature': feature_names, 'Importance': importances})
        df_importance = df_importance.sort_values(by='Importance', ascending=False)

        plt.figure(figsize=(10, 6))
        sns.barplot(x='Importance', y='Feature', data=df_importance)
        plt.xlabel('Importance')
        plt.ylabel('Feature')
        plt.title('Feature Importance')
        plt.show()

    # Print Evaluation Metrics
    print("Classification Report:\n", classification_report(y_test, y_pred))
else:
    print("Error: Target column not found! Please check your data.")


### Output:

![Screenshot 2025-05-14 105026](https://github.com/user-attachments/assets/a138580f-4268-45d2-a405-ee77a8ef3e2f)

![Screenshot 2025-05-14 105237](https://github.com/user-attachments/assets/75f4a464-1f2e-4e21-bb11-34a8d168f639)

![Screenshot 2025-05-14 105253](https://github.com/user-attachments/assets/7dc7aa35-300d-47e5-bd7d-22d9ac5123e0)


### Result:
Thus the system was trained successfully and the prediction was carried out.
