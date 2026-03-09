*Simple project using TensorFlow, FastAPI for the backend, and Streamlit for the frontend*

* The project will train a simple classification model with TensorFlow and expose an API via FastAPI to make predictions. The frontend with Streamlit will allow users to enter data and display predictions.

# 1 - Project Structure

```text
.
├── backend.py
├── frontend.py
├── model.py
├── README.md
└── requirements.txt
```

# 2 - `model.py` File

```python
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
import numpy as np

# Generate dummy training data
def generate_data():
    X = np.random.rand(1000, 8)  # 1000 samples, 8 features
    y = (X.sum(axis=1) > 4).astype(int)  # 1 if the sum of the features > 4, otherwise 0
    return X, y

# Create and train a simple model
def train_model():
    X, y = generate_data()
    model = Sequential([
        Dense(16, activation='relu', input_shape=(8,)),
        Dense(8, activation='relu'),
        Dense(1, activation='sigmoid')
    ])
    model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
    model.fit(X, y, epochs=10)
    model.save('model.h5')

if __name__ == "__main__":
    train_model()
```

# 3 - `backend.py` File

```python
from fastapi import FastAPI
from pydantic import BaseModel
import tensorflow as tf
import numpy as np

# Load the trained model
model = tf.keras.models.load_model('model.h5')

# Define the structure of the input data
class PredictionInput(BaseModel):
    features: list

app = FastAPI()

@app.post("/predict")
def predict(input: PredictionInput):
    features = np.array(input.features).reshape(1, -1)
    prediction = model.predict(features)
    return {"prediction": float(prediction[0, 0])}
```

# 4 - `frontend.py` File

```python
import streamlit as st
import requests

# FastAPI API URL
API_URL = "http://127.0.0.1:8000"

st.title("Prediction with TensorFlow, FastAPI and Streamlit")

features = [st.number_input(f"Feature {i+1}", format="%f") for i in range(8)]

if st.button("Predict"):
    response = requests.post(f"{API_URL}/predict", json={"features": features})
    if response.status_code == 200:
        prediction = response.json().get("prediction")
        st.success(f"The prediction is: {prediction}")
    else:
        st.error("Prediction error")
```

# 5 - `requirements.txt` File

```text
tensorflow
fastapi
uvicorn
pydantic
streamlit
requests
```

# 6 - Steps

6.1. Clone this repository to your local machine:

```bash
git clone https://github.com/hrhouma/fastapi-calculator-tensorflow-1.git
cd fastapi-calculator-tensorflow-1
```

6.2. Create a virtual environment and activate it:

```bash
python -m venv myenv
# On Windows
myenv\Scripts\activate
# On macOS and Linux
source myenv/bin/activate
```

6.3. Install the required dependencies:

```bash
pip install -r requirements.txt
```

6.4. Model Training

1. Run the `model.py` script to train and save the model:

```bash
python model.py
```

6.5. Starting the Backend

1. Start the FastAPI server:

```bash
uvicorn backend:app --reload
```

6.6. Starting the Frontend

1. Run the Streamlit application:

```bash
streamlit run frontend.py
```

6.7. Usage

1. Access the Streamlit web interface by opening a browser and going to the address indicated by Streamlit after launching the application (default: `http://localhost:8501`).
2. Enter the feature values and click on "Predict" to see the prediction.

## Project Structure

```text
.
├── backend.py
├── frontend.py
├── model.py
├── README.md
└── requirements.txt
```

---

### Commands

```bash
# Clone the repository
git clone https://github.com/hrhouma/fastapi-calculator-tensorflow-1.git
cd fastapi-calculator-tensorflow-1

# Create and activate a virtual environment
python -m venv myenv
# On Windows
myenv\Scripts\activate
# On macOS and Linux
source myenv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Train and save the model
python model.py

# Start the FastAPI server
uvicorn backend:app --reload

# Run the Streamlit application
streamlit run frontend.py
```
