The file is in the code format

Python code: 

import pandas as pd
import joblib

from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, classification_report


# ==========================================
# 1. Load Dataset
# ==========================================

print("Loading dataset...")

df = pd.read_csv("weatherAUS.csv")

print("Dataset loaded successfully!")
print("Dataset shape:", df.shape)


# ==========================================
# 2. Select Features
# ==========================================

features = [
    "MinTemp",
    "MaxTemp",
    "Rainfall",
    "WindGustSpeed",
    "WindSpeed9am",
    "WindSpeed3pm",
    "Humidity9am",
    "Humidity3pm",
    "Pressure9am",
    "Pressure3pm",
    "Cloud9am",
    "Cloud3pm",
    "Temp9am",
    "Temp3pm"
]

target = "RainTomorrow"


# ==========================================
# 3. Check Columns
# ==========================================

print("\nChecking required columns...")

missing_columns = []

for column in features + [target]:

    if column not in df.columns:
        missing_columns.append(column)


if len(missing_columns) > 0:

    print("\nThese columns are missing:")

    for column in missing_columns:
        print(column)

    print("\nPlease check your CSV file.")

    exit()


print("All required columns found!")


# ==========================================
# 4. Select Required Data
# ==========================================

data = df[features + [target]].copy()


# ==========================================
# 5. Convert Target
# ==========================================

data[target] = data[target].map({
    "Yes": 1,
    "No": 0
})


# ==========================================
# 6. Convert Features to Numbers
# ==========================================

for column in features:

    data[column] = pd.to_numeric(
        data[column],
        errors="coerce"
    )


# ==========================================
# 7. Remove Missing Values
# ==========================================

print("\nRemoving missing values...")

data = data.dropna()

print("Rows remaining:", len(data))


# ==========================================
# 8. Separate Input and Output
# ==========================================

X = data[features]

y = data[target]


# ==========================================
# 9. Split Dataset
# ==========================================

X_train, X_test, y_train, y_test = train_test_split(

    X,
    y,

    test_size=0.20,

    random_state=42,

    stratify=y
)


print("\nTraining samples:", len(X_train))
print("Testing samples:", len(X_test))


# ==========================================
# 10. Create Random Forest Model
# ==========================================

print("\nCreating Random Forest model...")

model = RandomForestClassifier(

    n_estimators=100,

    random_state=42,

    class_weight="balanced",

    n_jobs=-1
)


# ==========================================
# 11. Train Model
# ==========================================

print("Training model...")

model.fit(
    X_train,
    y_train
)

print("Model training completed!")


# ==========================================
# 12. Make Predictions
# ==========================================

print("\nTesting model...")

y_pred = model.predict(X_test)


# ==========================================
# 13. Calculate Accuracy
# ==========================================

accuracy = accuracy_score(
    y_test,
    y_pred
)


# ==========================================
# 14. Display Results
# ==========================================

print("\n========================================")
print("       RAINFALL PREDICTION RESULTS")
print("========================================")

print(
    "Accuracy:",
    round(accuracy * 100, 2),
    "%"
)

print("\nClassification Report:")

print(
    classification_report(
        y_test,
        y_pred
    )
)


# ==========================================
# 15. Save Trained Model
# ==========================================

print("\nSaving model...")

joblib.dump(
    model,
    "Rainfall.pkl"
)


# ==========================================
# 16. Save Feature Names
# ==========================================

joblib.dump(
    features,
    "features.pkl"
)


# ==========================================
# 17. Final Message
# ==========================================

print("\n========================================")
print("       MODEL SAVED SUCCESSFULLY")
print("========================================")

print("Created:")
print("1. Rainfall.pkl")
print("2. features.pkl")

print("\nYour rainfall prediction model is ready!")
