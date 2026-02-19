# Student Performance Prediction

This project predicts students' final grades (G3) using Linear Regression based on various features like student information, family background, and study habits.

---

## Dataset

- CSV file: `data/student_data.csv`  
- Contains 33 columns with features such as age, gender, family size, parental education, study time, and more.  
- Target variable: `G3` (final grade).

---

## Data Cleaning and Preprocessing

1. Converted categorical text to numeric values:

```python
df["sex"] = df["sex"].map({"F":0,"M":1})
df["address"] = df["address"].map({"U":0,"R":1})
df["famsize"] = df["famsize"].map({"LE3":0,"GT3":1})
df["Pstatus"] = df["Pstatus"].map({"T":0,"A":1})
Converted yes/no columns to 0/1:

for col in ["schoolsup","famsup","paid","activities","nursery","higher","internet","romantic"]:
    df[col] = df[col].map({"yes":1,"no":0})
Mapped parents’ jobs to numeric codes:

job_mapping = {"teacher":0,"health":1,"services":2,"at_home":3,"other":4}
df["Mjob"] = df["Mjob"].map(job_mapping).fillna(4).astype(int)
df["Fjob"] = df["Fjob"].map(job_mapping).fillna(4).astype(int)
Encoded school:

df["school"] = df["school"].map({"GP":0,"MS":1})
One-hot encoded reason and guardian:

df = pd.get_dummies(df, columns=["reason","guardian"], drop_first=True)
Features and Target
y = df["G3"]
X = df.drop("G3", axis=1)
X contains input features

y contains the target (final grade)

Train/Test Split
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
80% training, 20% testing

Random state ensures reproducibility

Model Training
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)
Linear Regression model learns the relationship between features and final grades.

Predictions
predictions = model.predict(X_test)
print(predictions[:10])
Predicts G3 for the test set.

Model Evaluation
from sklearn.metrics import mean_absolute_error, mean_squared_error

mae = mean_absolute_error(y_test, predictions)
mse = mean_squared_error(y_test, predictions)

print("MAE:", mae)
print("MSE:", mse)
MAE ≈ 1.85 → average error in predicted grades

MSE ≈ 6.62 → penalizes larger errors

Summary
Dataset cleaned and numeric

Features and target defined

Linear Regression trained and predictions made

Model performance evaluated using MAE and MSE

Project is ready for analysis and further improvement
