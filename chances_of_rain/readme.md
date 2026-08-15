The file is in the code format.

<!DOCTYPE html>
<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">

    <title>Rainfall Prediction Result</title>

    <style>

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {

            min-height: 100vh;

            display: flex;

            justify-content: center;

            align-items: center;

            font-family: Arial, sans-serif;

            background:
                linear-gradient(
                    135deg,
                    #dbeafe,
                    #e0f2fe
                );

            padding: 30px;
        }


        .result-card {

            width: 100%;

            max-width: 700px;

            background: white;

            padding: 35px;

            border-radius: 20px;

            text-align: center;

            box-shadow:
                0 10px 30px
                rgba(0, 0, 0, 0.15);
        }


        .icon {

            font-size: 60px;

            margin-bottom: 10px;
        }


        h1 {

            color: #0369a1;

            margin-bottom: 10px;

            font-size: 32px;
        }


        .message {

            color: #475569;

            font-size: 18px;

            margin-bottom: 25px;
        }


        img {

            width: 100%;

            max-width: 600px;

            height: 330px;

            object-fit: cover;

            border-radius: 15px;

            box-shadow:
                0 6px 18px
                rgba(0, 0, 0, 0.15);
        }


        .prediction {

            margin-top: 25px;

            padding: 15px;

            background: #eff6ff;

            border-radius: 10px;

            color: #0369a1;

            font-weight: bold;

            font-size: 18px;
        }


        .btn {

            display: inline-block;

            margin-top: 25px;

            padding: 12px 25px;

            background: #0284c7;

            color: white;

            text-decoration: none;

            border-radius: 8px;

            font-size: 16px;

            transition: 0.3s;
        }


        .btn:hover {

            background: #0369a1;

            transform: translateY(-2px);
        }


        @media(max-width:600px) {

            .result-card {

                padding: 20px;
            }

            h1 {

                font-size: 26px;
            }

            img {

                height: 250px;
            }
        }

    </style>

</head>


<body>

    <div class="result-card">

        <div class="icon">
            🌧️
        </div>


        <h1>
            Rainfall is Likely!
        </h1>


        <p class="message">

            The machine learning model predicts
            that there are chances of rainfall.

        </p>


        <img
            src="{{ url_for('static', filename='images/rainy.jpg') }}"
            alt="Rainy Weather">


        <div class="prediction">

            🌧️ Prediction:
            Chances of Rain Tomorrow

        </div>


        <a href="/" class="btn">

            ← Check Again

        </a>

    </div>

</body>

</html>
