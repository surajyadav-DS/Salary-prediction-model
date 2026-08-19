# 💰 Salary Prediction App

A machine learning web application that predicts an individual's salary
based on demographic, educational, professional, and experience-related
information.

The project uses **XGBoost Regression**, **Label Encoding**, and
**Streamlit** to provide an interactive salary prediction interface.

------------------------------------------------------------------------

## 📌 Project Overview

The **Salary Prediction App** takes the following user information as
input:

-   Age
-   Gender
-   Education Level
-   Job Title
-   Years of Experience

The trained machine learning model processes these features and returns
an estimated salary.

The application is designed as a simple end-to-end machine learning
deployment project:

**User Input → Data Preprocessing → Trained XGBoost Model → Salary
Prediction → Streamlit UI**

------------------------------------------------------------------------

## 🎯 Objectives

The main objectives of this project are to:

1.  Build a regression-based machine learning model for salary
    prediction.
2.  Handle categorical variables using label encoding.
3.  Save the trained model for later use.
4.  Develop an interactive web interface using Streamlit.
5.  Deploy a machine learning model without retraining it every time the
    application runs.
6.  Demonstrate a practical machine learning deployment workflow.

------------------------------------------------------------------------

## 🧠 Machine Learning Approach

### Problem Type

This is a **Supervised Machine Learning Regression** problem because the
target variable is a continuous numerical value: **salary**.

### Model

The project uses:

**XGBoost Regressor**

The saved model is an `XGBRegressor` with a regression objective
(`reg:squarederror`) and 200 estimators.

### Why XGBoost?

XGBoost is well suited for structured/tabular datasets and can model
nonlinear relationships between input features and salary.

------------------------------------------------------------------------

## 🧾 Input Features

  Feature                 Type          Description
  ----------------------- ------------- --------------------------------
  `Age`                   Numerical     Age of the individual
  `Gender`                Categorical   Gender of the individual
  `Education Level`       Categorical   Highest education level
  `Job Title`             Categorical   Current/professional job title
  `Years of Experience`   Numerical     Total professional experience

### Categorical Features

The project uses saved label encoders for:

-   `Gender`
-   `Education Level`
-   `Job Title`

The encoder file contains:

-   **2** gender categories
-   **3** education-level categories
-   **176** job-title categories

This is important because the Streamlit application should use the same
encoding scheme that was used when the model was trained.

------------------------------------------------------------------------

## 🏗️ Project Architecture

``` text
                   ┌─────────────────────┐
                   │    User Input       │
                   │ Age / Gender /      │
                   │ Education / Job /   │
                   │ Experience          │
                   └──────────┬──────────┘
                              │
                              ▼
                   ┌─────────────────────┐
                   │   Streamlit UI      │
                   └──────────┬──────────┘
                              │
                              ▼
                   ┌─────────────────────┐
                   │ Label Encoding      │
                   │ Categorical Data    │
                   └──────────┬──────────┘
                              │
                              ▼
                   ┌─────────────────────┐
                   │ XGBoost Regressor   │
                   │ Trained Model       │
                   └──────────┬──────────┘
                              │
                              ▼
                   ┌─────────────────────┐
                   │ Predicted Salary    │
                   └─────────────────────┘
```

------------------------------------------------------------------------

## 📁 Project Structure

``` text
Salary-Prediction/
│
├── salary_prediction_deployment.py
├── salary_prediction_model.pkl
├── lable_encoder.pkl
├── requirements.txt
└── README.md
```

### File Description

  -----------------------------------------------------------------------
  File                                Purpose
  ----------------------------------- -----------------------------------
  `salary_prediction_deployment.py`   Streamlit application and
                                      prediction logic

  `salary_prediction_model.pkl`       Saved trained XGBoost regression
                                      model

  `lable_encoder.pkl`                 Saved encoders for categorical
                                      features

  `requirements.txt`                  Python dependencies

  `README.md`                         Project documentation
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 🛠️ Technologies Used

### Programming Language

-   Python

### Libraries & Frameworks

-   **Streamlit** --- interactive web application
-   **Pandas** --- data manipulation
-   **NumPy** --- numerical operations
-   **XGBoost** --- machine learning regression model
-   **Scikit-learn** --- preprocessing/label encoding
-   **Joblib** --- saving and loading trained model artifacts

The supplied `requirements.txt` lists these project dependencies.
fileciteturn0file0L1-L6

------------------------------------------------------------------------

## ⚙️ Installation

### 1. Clone the Repository

``` bash
git clone https://github.com/<your-username>/Salary-Prediction.git
cd Salary-Prediction
```

Replace `<your-username>` with your GitHub username.

### 2. Create a Virtual Environment

Windows:

``` bash
python -m venv venv
venv\Scripts\activate
```

macOS/Linux:

``` bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

``` bash
pip install -r requirements.txt
```

The project requires Streamlit, Pandas, NumPy, XGBoost, scikit-learn,
and Joblib. fileciteturn0file0L1-L6

------------------------------------------------------------------------

## ▶️ Run the Application

Start the Streamlit application with:

``` bash
streamlit run salary_prediction_deployment.py
```

After starting the application, Streamlit will provide a local URL in
the terminal. Open that URL in your browser.

------------------------------------------------------------------------

## 🖥️ How to Use

### Step 1 --- Enter Age

Enter the individual's age using the **Age** input.

### Step 2 --- Select Gender

Choose the appropriate gender from the available options.

### Step 3 --- Select Education Level

Choose the education level:

-   Bachelor's
-   Master's
-   PhD

The exact options are loaded from the saved encoder.

### Step 4 --- Select Job Title

Select the relevant job title from the available encoded job-title
categories.

### Step 5 --- Enter Experience

Enter the individual's years of professional experience.

### Step 6 --- Predict Salary

Click:

``` text
Predict Salary
```

The application sends the processed input to the trained XGBoost model
and displays the predicted salary.

------------------------------------------------------------------------

## 🔄 Prediction Workflow

The deployment script follows this workflow:

``` text
1. Load trained model
        ↓
2. Load label encoders
        ↓
3. Collect user input
        ↓
4. Create a Pandas DataFrame
        ↓
5. Encode categorical columns
        ↓
6. Pass processed data to XGBoost
        ↓
7. Generate salary prediction
        ↓
8. Display prediction in Streamlit
```

The supplied deployment script loads both saved artifacts with Joblib
and creates Streamlit controls for the five input features.
fileciteturn0file1L10-L24

------------------------------------------------------------------------

## 💾 Model Loading

The application loads the saved model and encoders instead of training
the model again:

``` python
model = joblib.load("salary_prediction_model.pkl")
encoder = joblib.load("lable_encoder.pkl")
```

This makes the application faster at startup and separates the
**model-training stage** from the **model-deployment stage**.
fileciteturn0file1L14-L17

------------------------------------------------------------------------

## 📊 Model Configuration

The saved model is an:

``` text
XGBRegressor
```

with:

``` text
Objective: reg:squarederror
Number of estimators: 200
```

The model is intended for continuous salary prediction.

------------------------------------------------------------------------

## 🔐 Important Model Compatibility Note

The `.pkl` files are serialized Python objects. For reliable deployment,
use package versions compatible with the environment in which the model
was trained.

In particular, serialized scikit-learn/XGBoost objects can produce
compatibility warnings or unexpected behavior when loaded with
substantially different library versions.

For production deployment, it is recommended to:

1.  Record the exact training environment.
2.  Pin dependency versions.
3.  Retrain/export the model when upgrading major library versions.
4.  Test predictions after changing package versions.

------------------------------------------------------------------------

## ⚠️ Important Code Check Before Running

The supplied deployment file contains the intended encoding loop:

``` python
for col in encoder:
    df(col) = encoder[col].transform(df[col])
```

However, `df(col)` is not valid Pandas DataFrame column-assignment
syntax.

It should be:

``` python
for col in encoder:
    df[col] = encoder[col].transform(df[col])
```

This correction is required before running the application successfully.

The rest of the supplied deployment structure creates the input
DataFrame and calls the model prediction step after the button is
pressed. fileciteturn0file1L27-L40

------------------------------------------------------------------------

## 🧪 Example Prediction Flow

Example input:

``` text
Age: 25
Gender: male
Education Level: master's
Job Title: Data Scientist
Years of Experience: 2
```

The application:

``` text
Raw Input
   ↓
Categorical Encoding
   ↓
Numerical Feature DataFrame
   ↓
XGBoost Model
   ↓
Predicted Salary
```

The actual predicted salary depends on the trained model and its
training dataset.

------------------------------------------------------------------------

## 🚀 Deployment

This project can be deployed on a Streamlit-compatible hosting platform.

Before deployment, make sure the repository contains:

``` text
salary_prediction_deployment.py
salary_prediction_model.pkl
lable_encoder.pkl
requirements.txt
README.md
```

Then configure the deployment platform to run:

``` bash
streamlit run salary_prediction_deployment.py
```

------------------------------------------------------------------------

## 🔮 Future Improvements

The current project can be improved significantly in future versions.

### 1. Better Data Preprocessing

Create a complete preprocessing pipeline so that encoding and model
prediction are handled consistently.

### 2. Model Evaluation

Add regression metrics such as:

-   MAE
-   MSE
-   RMSE
-   R² Score

### 3. Improved User Interface

Add:

-   Better page layout
-   Sidebar controls
-   Input validation
-   Salary range visualization
-   Professional dashboard design

### 4. Prediction History

Use Streamlit session state or a database to store previous predictions.

### 5. Model Explainability

Add feature importance or SHAP-based explanations to show which features
influence salary predictions.

### 6. Better Encoding Strategy

For production systems, consider a complete preprocessing pipeline
instead of manually applying separate encoders.

### 7. API Deployment

The prediction model can also be exposed through an API using frameworks
such as FastAPI.

### 8. Continuous Model Improvement

Retrain the model periodically with new salary-market data.

------------------------------------------------------------------------

## 📌 Limitations

This application provides an **estimated salary**, not a guaranteed
salary.

Salary can depend on many additional factors, including:

-   Location
-   Company
-   Industry
-   Skills
-   Job responsibilities
-   Market conditions
-   Negotiation
-   Performance
-   Additional certifications

If these variables were not included in the training data, the model
cannot account for them.

------------------------------------------------------------------------

## 🔒 Data & Privacy

Do not enter sensitive personal information into the application.

The application is intended for educational and demonstration purposes
unless additional security, privacy, validation, and production controls
are implemented.

------------------------------------------------------------------------

## 🎓 Learning Outcomes

This project demonstrates practical understanding of:

-   Supervised machine learning
-   Regression
-   XGBoost
-   Categorical encoding
-   Pandas DataFrames
-   Model serialization with Joblib
-   Streamlit UI development
-   Machine learning model deployment
-   Python dependency management
-   Basic production-readiness considerations

------------------------------------------------------------------------

## 👨‍💻 Author

**Suraj Yadav**

B.Sc. Data Science & AI Student

### Areas of Interest

-   Data Science
-   Artificial Intelligence
-   Machine Learning
-   Data Analysis
-   Python
-   Machine Learning Deployment

------------------------------------------------------------------------

## 📜 License

This project is intended for educational and learning purposes.

If you plan to distribute or use the project commercially, add an
appropriate open-source or proprietary license.

------------------------------------------------------------------------

## ⭐ Support

If you find this project useful, consider giving the repository a ⭐ on
GitHub.

For suggestions, improvements, or collaboration, feel free to open an
issue or submit a pull request.

------------------------------------------------------------------------

## 📈 Project Status

**Status:** Machine Learning Deployment Project

**Model:** XGBoost Regressor

**Interface:** Streamlit

**Purpose:** Salary Prediction
