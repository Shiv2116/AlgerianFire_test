Here’s a `README.md` template for your Flask-based machine learning project:

---

# Flask ML Prediction API

This repository contains a Flask application for serving a machine learning model. The API accepts input data via HTTP requests, processes it, and returns predictions.

## Features
- **Scalable API:** Built with Flask for serving ML models.
- **Input Validation:** Ensures data integrity before making predictions.
- **Error Handling:** Handles and reports errors gracefully.
- **Extensibility:** Easy to update with new models or endpoints.

---

## Installation

### Prerequisites
- Python 3.12 or higher
- pip (Python package manager)

### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/Shiv2116/AlgerianFire_test.git
   cd AlgerianFire_test
   ```
2. Create a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows, use venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

---

## Usage

1. Run the Flask app:
   ```bash
   flask run
   ```
   By default, the app runs on `http://127.0.0.1:5000`.

2. Test the endpoint using a tool like Postman or cURL.

### Example cURL Command
```bash
curl -X POST http://127.0.0.1:5000/predict \
     -H "Content-Type: application/json" \
     -d '{"Temperature": 25, "RH": 60, "Ws": 12, "Rain": 0, "FFMC": 85, "DMC": 26, "ISI": 5, "Classes": 1, "Region": 2}'
```

---

## API Endpoints

### `/predict` (POST)
- **Description:** Accepts input data, processes it, and returns predictions.
- **Request Body:** JSON object with the following fields:
  | Field       | Type     | Description                     |
  |-------------|----------|---------------------------------|
  | `Temperature` | `float` | Temperature in Celsius          |
  | `RH`          | `int`   | Relative humidity percentage    |
  | `Ws`          | `float` | Wind speed                     |
  | `Rain`        | `float` | Rainfall amount                |
  | `FFMC`        | `float` | Fine Fuel Moisture Code         |
  | `DMC`         | `float` | Duff Moisture Code              |
  | `ISI`         | `float` | Initial Spread Index            |
  | `Classes`     | `int`   | Fire class                     |
  | `Region`      | `int`   | Region code                    |

- **Response:**
  - **Success (200):** 
    ```json
    {
      "prediction": "value"
    }
    ```
  - **Error (400/500):** 
    ```json
    {
      "error": "Error message"
    }
    ```

---

## Error Handling

- **Input Validation:** Ensures all required fields are provided and valid.
- **500 Internal Server Error:** Unhandled exceptions are caught and returned as JSON with a descriptive error message.

---

## Deployment

1. **Production Server:**
   Use `gunicorn` or similar WSGI servers:
   ```bash
   gunicorn -w 4 -b 0.0.0.0:5000 app:app
   ```
2. **Containerization:** Add a `Dockerfile` for containerized deployment.

---

## Model Training and Saving

1. Train your machine learning model using your preferred framework (e.g., scikit-learn, TensorFlow).
2. Save the model and scaler using `joblib`:
   ```python
   from joblib import dump

   dump(model, 'model.joblib')
   dump(scaler, 'scaler.joblib')
   ```
3. Place the saved files in the project directory and load them during app initialization:
   ```python
   from joblib import load

   model = load('model.joblib')
   scaler = load('scaler.joblib')
   ```

---
