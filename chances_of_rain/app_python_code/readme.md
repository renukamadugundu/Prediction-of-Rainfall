The file in the code format

Python code: 

from flask import Flask, render_template, request
import pandas as pd
import joblib


# ==========================================
# Create Flask Application
# ==========================================

app = Flask(__name__)


# ==========================================
# Load Trained Model
# ==========================================

model = joblib.load("Rainfall.pkl")

features = joblib.load("features.pkl")


# ==========================================
# Home Page
# ==========================================

@app.route("/")
def home():
    return render_template("index.html")


# ==========================================
# Prediction
# ==========================================

@app.route("/predict", methods=["POST"])
def predict():

    try:

        # --------------------------------------
        # Get values from HTML form
        # --------------------------------------

        input_data = {

            "MinTemp": float(request.form["MinTemp"]),

            "MaxTemp": float(request.form["MaxTemp"]),

            "Rainfall": float(request.form["Rainfall"]),

            "WindGustSpeed": float(
                request.form["WindGustSpeed"]
            ),

            "WindSpeed9am": float(
                request.form["WindSpeed9am"]
            ),

            "WindSpeed3pm": float(
                request.form["WindSpeed3pm"]
            ),

            "Humidity9am": float(
                request.form["Humidity9am"]
            ),

            "Humidity3pm": float(
                request.form["Humidity3pm"]
            ),

            "Pressure9am": float(
                request.form["Pressure9am"]
            ),

            "Pressure3pm": float(
                request.form["Pressure3pm"]
            ),

            "Cloud9am": float(
                request.form["Cloud9am"]
            ),

            "Cloud3pm": float(
                request.form["Cloud3pm"]
            ),

            "Temp9am": float(
                request.form["Temp9am"]
            ),

            "Temp3pm": float(
                request.form["Temp3pm"]
            )
        }


        # --------------------------------------
        # Arrange input according to model
        # --------------------------------------

        input_values = []

        for feature in features:

            input_values.append(
                input_data[feature]
            )


        # --------------------------------------
        # Convert to DataFrame
        # --------------------------------------

        input_df = pd.DataFrame(
            [input_values],
            columns=features
        )


        # --------------------------------------
        # Make Prediction
        # --------------------------------------

        prediction = model.predict(input_df)[0]


        # --------------------------------------
        # Convert prediction to text
        # --------------------------------------

        if prediction == 1:

            return render_template(
                "chances_of_Rain.html"
            )

        else:

            return render_template(
                "no_chances_of_Rain.html"
            )


    except Exception as e:

        return f"""
        <h2>Prediction Error</h2>
        <p>{str(e)}</p>
        <br>
        <a href="/">Go Back</a>
        """


# ==========================================
# Run Application
# ==========================================

if __name__ == "__main__":

    app.run(
        debug=True
    )
