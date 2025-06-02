# future-health-prediction
The inspiration to create this code is that ,where humans technically able to analyze their upcoming health conditions based on their past health data and past health conditions where care and precautions can be taken before head as they always says  "PREVENTION IS BETTER THAN CURE!"
Here i have used random forest classifier algorithm
Random Forest Classifier: This is the core machine learning algorithm employed for prediction.
It belongs to the ensemble learning family, specifically a bagging method.
It works by constructing multiple decision trees during training and outputting the class that is the mode of the classes (classification) or mean/average prediction (regression) of the individual trees.
Known for its good accuracy, robustness to overfitting, and ability to handle high-dimensional data.
*********************************************************************************************************************************************************
# Import necessary libraries
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

# -----------------------------------
# Step 1: Prepare training data
# -----------------------------------
# This is a mock dataset we’re using to train our simple model.
# In real life, you'd want to load this from a real medical database.
data = {
    'age': [25, 45, 35, 50, 30, 60, 40, 70],
    'bmi': [22.0, 30.5, 25.3, 32.1, 24.2, 28.6, 27.0, 29.8],
    'blood_pressure': [120, 140, 130, 150, 125, 160, 135, 155],
    'smoking': [0, 1, 0, 1, 0, 1, 1, 1],      # 1 = Yes, 0 = No
    'exercise': [1, 0, 1, 0, 1, 0, 0, 0],     # 1 = Yes, 0 = No
    'future_health': [1, 0, 1, 0, 1, 0, 0, 0] # 1 = Good, 0 = Poor
}

# Load data into a DataFrame
df = pd.DataFrame(data)

# -----------------------------------
# Step 2: Split into features and labels
# -----------------------------------
X = df[['age', 'bmi', 'blood_pressure', 'smoking', 'exercise']]
y = df['future_health']

# Train-test split (80% training, 20% testing)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=1)

# Train the model using Random Forest
model = RandomForestClassifier()
model.fit(X_train, y_train)

# -----------------------------------
# Step 3: Take user input and make prediction
# -----------------------------------
def predict_user_health():
    print("\n🧠 Let's predict your future health based on your current lifestyle.\n")
    try:
        # Get user details
        age = int(input("👉 Enter your age: "))
        height_cm = float(input("👉 Enter your height (in cm): "))
        weight_kg = float(input("👉 Enter your weight (in kg): "))
        bp = int(input("👉 Enter your blood pressure: "))
        exercise = input("👉 Do you exercise regularly? (yes/no): ").strip().lower()
        smoking = input("👉 Do you smoke? (yes/no): ").strip().lower()
        height_m = height_cm / 100
        bmi = weight_kg / (height_m ** 2)
        # Convert text inputs to binary values
        exercise_binary = 1 if exercise == 'yes' else 0
        smoking_binary = 1 if smoking == 'yes' else 0
         # Prepare input for prediction
        user_input = [[age, bmi, bp, smoking_binary, exercise_binary]]
        prediction = model.predict(user_input)
        if prediction[0] == 1:
            print("\n✅ You are likely to enjoy GOOD health in the future! Keep it up 💪")
        else:
            print("\n⚠️ Warning: You might face health issues in the future. Time to adopt a healthier lifestyle 🏃‍♂️🥗")
             except Exception as e:
        print("🚫 Error:", e)

# Run the health predictor
predict_user_health()

    

      

        
