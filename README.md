# Bangalore House Price Prediction Model

## Table of Contents
- [Introduction](#introduction)
- [Dataset](#dataset)
- [Model Description](#model-description)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Results](#results)
- [Contributing](#contributing)
- [License](#license)

## Introduction

This project involves developing a machine learning model to predict house prices in Bangalore. By analyzing various features such as location, size, and amenities, the model aims to provide accurate price estimates for residential properties. This tool is useful for real estate agents, potential buyers, and data enthusiasts interested in property price trends in Bangalore.

## Dataset

The dataset used for this model includes several features relevant to house prices in Bangalore, such as:
- Location
- Number of bedrooms (BHK)
- Square footage (total area)
- Number of bathrooms
- Availability (immediate, upcoming, etc.)
- Price

The dataset is preprocessed to handle missing values, outliers, and categorical variables.
Example input CSV format:

| location      | size  | total_sqft | bath | price |
|---------------|-------|------------|------|-------|
| Whitefield    | 3 BHK | 1500       | 2    | ?     |
| Indiranagar   | 2 BHK | 1200       | 2    | ?     |
| ...           | ...   | ...        | ...  | ...   |

## Model Description

The prediction model is built using several machine learning algorithms. The final model is selected based on performance metrics such as RMSE (Root Mean Squared Error), MAE (Mean Absolute Error), and R² score. The main algorithms considered include:
- Linear Regression
- Decision Trees

After extensive testing and validation, the best-performing model is chosen and fine-tuned for optimal performance.

## Installation

To use this project, follow these steps:

1. Clone the repository:
   \`\`\`bash
   git clone https://github.com/yourusername/bangalore-house-price-prediction.git
   \`\`\`
2. Navigate to the project directory:
   \`\`\`bash
   cd bangalore-house-price-prediction
   \`\`\`
3. Install the required dependencies:
   \`\`\`bash
   pip install -r requirements.txt
   \`\`\`

## Usage
```bash
import pickle
import numpy as np
import pandas as pd

# Load the trained model
model_file = 'banglore_home_prices_model.pickle'  # Replace with the path to your trained model file
with open(model_file, 'rb') as file:
    model = pickle.load(file)

# Load the columns data (assuming you have the columns saved in a file)
columns_file = 'columns.pickle'  # Replace with the path to your columns file
with open(columns_file, 'rb') as file:
    data_columns = pickle.load(file)

# Create a DataFrame with the columns
X = pd.DataFrame(columns=data_columns)

# Define the prediction function
def predict_price(location, sqft, bath, bhk):    
    loc_index = np.where(X.columns == location)[0][0]

    x = np.zeros(len(X.columns))
    x[0] = sqft
    x[1] = bath
    x[2] = bhk
    if loc_index >= 0:
        x[loc_index] = 1

    return model.predict([x])[0]

# Example usage
predicted_price = predict_price('1st Phase JP Nagar', 1000, 2, 2)
print(f"Estimated House Price: ${predicted_price:.2f}")
```


## Configuration

You can adjust various settings and hyperparameters in the \`config.yaml\` file. This includes parameters such as:
- Model hyperparameters (e.g., number of trees in Random Forest)
- Data preprocessing options
- Paths for input and output data

## Results

The model's performance metrics are provided in the results directory, which includes:
- RMSE
- MAE
- R² score

These metrics are calculated on the test dataset and can be used to evaluate the model's accuracy and reliability.

## Contributing

Contributions to this project are welcome. If you have suggestions for improvements or new features, please submit an issue or a pull request. For major changes, please discuss them with the project maintainers first.

To contribute:

1. Fork the repository.
2. Create a new branch (\`git checkout -b feature-branch\`).
3. Make your changes.
4. Commit your changes (\`git commit -m 'Add some feature'\`).
5. Push to the branch (\`git push origin feature-branch\`).
6. Open a pull request.

## License

This project is licensed under the MIT License. See the LICENSE file for details.

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)


