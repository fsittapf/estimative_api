
# Monte Carlo Simulation API

This project provides a Flask-based API for running Monte Carlo simulations to estimate project durations. It includes endpoints for running simulations, retrieving results, and visualizing the distributions of total project durations.

---

## Features

1. **Monte Carlo Simulation**:
   - Supports PERT (triangular) and normal distributions for task duration modeling.
   - Simulates total project durations by sampling task durations iteratively.

2. **Statistical Analysis**:
   - Calculates mean, median, standard deviation, and custom percentiles of the simulation results.

3. **Visualization**:
   - Generates histograms of simulation results with mean and median visualized.
   - Uploads histograms to Imgur for easy sharing.

4. **API Endpoints**:
   - Retrieve all estimations.
   - Retrieve a specific estimation by ID.
   - Run a Monte Carlo simulation with custom parameters.

---

## Installation

### Prerequisites
- Python 3.8+
- Install required dependencies:
```bash
pip install flask numpy matplotlib pyimgur
```

### Configuration
Set the `CLIENT_ID` variable in the simulation script with your Imgur client ID.

---

## Usage

### Running the API
Run the application using:
```bash
python app.py
```

The API will be accessible at `http://127.0.0.1:5000/`.

---

## Endpoints

### `/` (GET)
Returns a welcome message.

### `/estimative` (GET)
Returns all estimations stored in the database.

### `/estimative/<calc_uuid>` (GET)
Retrieves a specific estimation by ID.

### `/estimative` (POST)
Runs a Monte Carlo simulation. Expects a JSON body with the following structure:
```json
{
    "tasks": [
        {"min": 2, "likely": 4, "max": 8},
        {"min": 3, "likely": 5, "max": 7}
    ],
    "iterations": 1000,
    "type": "triangular",
    "percentiles": [50, 70, 90],
    "image": {"plot": true}
}
```
- **tasks**: List of tasks with `min`, `likely`, and `max` durations.
- **iterations**: Number of iterations (default: 1000).
- **type**: Distribution type (`triangular` or `normal`).
- **percentiles**: List of percentiles to calculate (default: [50, 70, 90, 100]).
- **image**: Configuration for plot generation.

### Example Response:
```json
{
    "id": "CALC_UUID",
    "tasks": [{"min": 2, "likely": 4, "max": 8, "mean": 4.67, "std_dev": 1.0}],
    "mean": 15.6,
    "median": 14.9,
    "std_dev": 3.2,
    "type": "triangular",
    "iterations": 1000,
    "percentiles": {"P50": 14.5, "P90": 19.3},
    "image_url": "https://i.imgur.com/example.png",
    "created_at": "2025-01-17_15:30:00"
}
```

---

## Contribution

Feel free to fork and enhance this project. Contributions are welcome!

---

## License

This project is licensed under the MIT License.
