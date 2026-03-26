# End-to-End Machine Learning Project: Student Performance Prediction

## Overview

This project implements an end-to-end machine learning pipeline to predict student math scores based on demographic and academic factors. The system predicts student performance using features like gender, race/ethnicity, parental education level, lunch type, and test preparation course.

**Author**: Amrish (IIIT Lucknow)  
**Version**: 0.0.1  
**Dataset**: Student Performance Dataset (Kaggle) - 1000 rows, 8 columns

## Problem Statement

The project aims to understand how various factors influence student academic performance, specifically predicting math scores from:
- Demographic information (gender, race/ethnicity)
- Socioeconomic factors (parental education, lunch type)
- Academic preparation (test preparation course, reading/writing scores)

## Features

- **Target Variable**: math_score (numerical prediction)
- **Input Features**:
  - Numerical: reading_score, writing_score
  - Categorical: gender, race_ethnicity, parental_level_of_education, lunch, test_preparation_course

## Project Workflow

### 1. Data Ingestion
- Load raw data from CSV file (`notebook/data/raw.csv`)
- Perform 80/20 train-test split with random state 42
- Save processed data to `artifacts/` directory

### 2. Data Transformation
- **Numerical Features**: Median imputation + Standard scaling
- **Categorical Features**: Mode imputation + One-hot encoding + Standard scaling
- Save preprocessor pipeline as `artifacts/preprocessor.pkl`

### 3. Model Training
- Test 7 different regression algorithms:
  - Random Forest Regressor
  - Decision Tree Regressor
  - Gradient Boosting Regressor
  - Linear Regression
  - XGBRegressor
  - CatBoost Regressor
  - AdaBoost Regressor
- Hyperparameter tuning using GridSearchCV
- Model evaluation using RMSE, MAE, and R² metrics
- Save best performing model as `artifacts/model.pkl`

### 4. Experiment Tracking
- MLflow integration for experiment logging
- DagsHub remote tracking (repository: amrish407/mlproject)
- Automatic model versioning and comparison

## Installation & Setup

### Prerequisites
- Python 3.11+
- MySQL database (optional, for future extensions)
- Git

### Environment Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd "Data Science"
   ```

2. **Create virtual environment**
   ```bash
   # Using conda (recommended)
   conda create -p dsenv python=3.11 -y
   conda activate dsenv/

   # Or using venv
   python -m venv dsenv
   source dsenv/bin/activate  # On Windows: dsenv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Environment Configuration**
   Create a `.env` file in the root directory:
   ```env
   host=localhost
   user=root
   password=your_mysql_password
   db=college
   ```

5. **Data Setup**
   - Place your dataset as `notebook/data/raw.csv`
   - Initialize DVC for data versioning: `dvc init`

## Usage

### Training the Model
Run the complete training pipeline:
```bash
python app.py
```

This will:
- Load and preprocess the data
- Train multiple models with hyperparameter tuning
- Select and save the best performing model
- Log experiments to MLflow

### Exploring with Notebooks
```bash
jupyter notebook
```
Open these notebooks for detailed analysis:
- `notebook/1 . EDA STUDENT PERFORMANCE.ipynb` - Exploratory Data Analysis
- `notebook/2. MODEL TRAINING.ipynb` - Model development and comparison

### MLflow UI
View experiment tracking:
```bash
mlflow ui
```
Access at: http://localhost:5000

## Project Structure

```
├── src/ml_project/                    # Main package
│   ├── components/                    # ML pipeline components
│   │   ├── data_ingestion.py         # Data loading & splitting
│   │   ├── data_transformation.py    # Feature preprocessing
│   │   ├── model_trainer.py          # Model training & selection
│   │   └── model_monitoring.py       # Model monitoring (empty)
│   ├── pipelines/                     # Pipeline orchestrators
│   │   ├── training_pipeline.py      # Training workflow
│   │   └── prediction_pipeline.py    # Prediction workflow (empty)
│   ├── logger.py                      # Custom logging
│   ├── exception.py                   # Custom exceptions
│   └── utils.py                       # Helper functions
├── notebook/                          # Jupyter notebooks
│   ├── 1 . EDA STUDENT PERFORMANCE.ipynb
│   ├── 2. MODEL TRAINING.ipynb
│   └── data/raw.csv                   # Source dataset
├── artifacts/                         # Generated outputs
│   ├── train.csv, test.csv           # Split datasets
│   ├── raw.csv                        # Raw data copy
│   ├── preprocessor.pkl              # Saved preprocessor
│   └── model.pkl                      # Trained model
├── logs/                             # Application logs
├── catboost_info/                    # CatBoost training artifacts
├── app.py                            # Main training script
├── requirements.txt                  # Python dependencies
├── setup.py                          # Package configuration
├── Dockerfile                        # Containerization (empty)
└── .env                              # Environment variables
```

## Dependencies

Key libraries used:
- **Data Processing**: pandas, numpy
- **Machine Learning**: scikit-learn, catboost, xgboost
- **Experiment Tracking**: mlflow, dagshub
- **Web Framework**: Flask (for future API)
- **Database**: pymysql, mysql-connector-python
- **Visualization**: seaborn, matplotlib

## Model Performance

The system evaluates models using:
- **RMSE** (Root Mean Squared Error)
- **MAE** (Mean Absolute Error)
- **R² Score** (Coefficient of Determination)

Best performing model is automatically selected and saved.

## Configuration

### Environment Variables
- `host`: MySQL database host
- `user`: MySQL username
- `password`: MySQL password
- `db`: MySQL database name

### MLflow Setup
- Local tracking: `mlruns/` directory
- Remote tracking: DagsHub repository (amrish407/mlproject)

## Future Enhancements

- [ ] Complete Flask API for real-time predictions
- [ ] Implement prediction pipeline
- [ ] Add Docker containerization
- [ ] Create web interface for model deployment
- [ ] Add model monitoring and retraining capabilities
- [ ] API documentation with Swagger/OpenAPI

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes and test thoroughly
4. Commit changes: `git commit -am 'Add feature'`
5. Push to branch: `git push origin feature-name`
6. Submit a pull request

## License

This project is for educational purposes.

## Contact

**Amrish**  
Email: mcs24020@iiitl.ac.in  
Institution: IIIT Lucknow

---

*Built with Python 3.11, scikit-learn, and MLflow*
