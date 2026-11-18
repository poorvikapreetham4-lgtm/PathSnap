# PathSnap

PathSnap is a machine-learning-based GPS trajectory reconstruction system designed to identify likely road segments from noisy GPS observations and reconstruct vehicle journeys on a road network.

GPS signals can be inaccurate because of signal interference, urban infrastructure, irregular sampling and location noise. PathSnap addresses this challenge through candidate road generation, feature engineering, machine learning classification and connectivity-aware route reconstruction.

## 🎯 Problem Statement

Raw GPS trajectories do not always accurately represent the roads travelled by a vehicle.

The objective of PathSnap is to:

- Process noisy GPS trajectory data.
- Identify candidate road segments for each GPS observation.
- Predict the likelihood of candidate road matches.
- Reconstruct a connected road sequence.
- Visualize the original and reconstructed trajectories.

## 💡 Proposed Solution

PathSnap combines machine learning and road-network information through the following pipeline:

```text
GPS Trajectory Dataset
        |
        v
Data Loading & Preprocessing
        |
        v
Road Network Processing
        |
        v
Candidate Road Generation
        |
        v
Feature Engineering
        |
        v
Machine Learning Classification
        |
        v
Candidate Probability Prediction
        |
        v
Viterbi-Style Route Reconstruction
        |
        v
Interactive Route Visualization
```

## 🧠 Machine Learning Models

Six classification algorithms are trained and compared:

1. Logistic Regression
2. K-Nearest Neighbors (KNN)
3. Decision Tree
4. Random Forest
5. Gradient Boosting
6. HistGradientBoosting

### Preliminary Model Performance

| Model | Accuracy | F1-score |
|---|---:|---:|
| HistGradientBoosting | 89.84% | 0.6891 |
| Gradient Boosting | 89.74% | 0.6806 |
| Random Forest | 87.84% | 0.6907 |
| KNN | 87.38% | 0.6218 |
| Decision Tree | 83.86% | 0.6240 |
| Logistic Regression | 79.38% | 0.5973 |

**Best F1-score:** Random Forest — 0.6907.

**Highest accuracy:** HistGradientBoosting — 89.84%.

> Note: These are preliminary results obtained using automatically generated weak labels. They are not independently verified road-matching accuracy measurements.

## ⚙️ Feature Engineering

The candidate road feature dataset includes:

- Candidate rank
- Distance to road
- GPS bearing
- Road bearing
- Bearing difference
- GPS speed
- Road length
- Time gap

## 🛣️ Route Reconstruction

PathSnap implements a Viterbi-style dynamic programming approach to select likely road segments across consecutive GPS observations.

The reconstruction considers:

- Candidate match probabilities.
- Connectivity between consecutive road segments.
- Transition penalties for disconnected segments.

The current implementation is a prototype and requires further validation of road-network indexing and transition modelling.

## 🗺️ Interactive Visualization

Folium is used to generate interactive HTML maps.

The visualizations aim to display:

- Original GPS trajectories.
- Predicted road segments.
- Individual reconstructed trips.

## 🖥️ Technology Stack

| Category | Technologies |
|---|---|
| Programming | Python |
| Data Processing | Pandas, NumPy |
| Machine Learning | Scikit-learn |
| Model Persistence | Joblib |
| Visualization | Folium, Matplotlib |
| Frontend | Streamlit |
| API | FastAPI |
| Version Control | Git, GitHub |

## 📂 Project Structure

```text
PathSnap/
│
├── api/
│   └── main.py
│
├── frontend/
│   └── app.py
│
├── ml/
│   ├── train_all_models.py
│   └── predict_test.py
│
├── src/
│   ├── data_loader.py
│   ├── preprocessing.py
│   ├── feature_engineering.py
│   ├── generate_training_features.py
│   ├── generate_training_labels.py
│   ├── reconstruct_routes.py
│   ├── visualize_routes.py
│   └── final_evaluation.py
│
├── models/
├── data/
├── outputs/
├── requirements.txt
├── .gitignore
└── README.md
```

## 🛠️ Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/PathSnap.git
cd PathSnap
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

### 3. Activate the environment

Windows:

```powershell
.\venv\Scripts\Activate.ps1
```

### 4. Install dependencies

```bash
pip install -r requirements.txt
```

### 5. Add the dataset

Place the extracted dataset in the expected `data/` directory structure.

### 6. Run the frontend

```bash
streamlit run frontend/app.py
```

## 🔮 Future Improvements

- Improve GPS-to-road matching using point-to-segment geometric distance.
- Develop more reliable GPS-to-ground-truth sequence alignment.
- Incorporate travel distance and time into transition probabilities.
- Improve route decoding using a properly calibrated Hidden Markov Model.
- Evaluate against independently verified route labels.
- Develop a more comprehensive interactive route analytics dashboard.

## 🏁 Conclusion

PathSnap demonstrates an end-to-end prototype for GPS trajectory reconstruction by combining machine learning, road-network connectivity and interactive visualization.

The project provides a foundation for intelligent mobility applications, vehicle tracking, logistics and smart transportation systems.

---

**PathSnap — Turning Noisy GPS Data into Meaningful Road Journeys.**
