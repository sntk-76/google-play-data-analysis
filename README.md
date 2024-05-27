# Google Play Store Data Analysis

## Table of Contents
- [Introduction](#introduction)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Data Preprocessing](#data-preprocessing)
- [Analysis and Visualization](#analysis-and-visualization)
- [Results](#results)
- [Conclusion](#conclusion)
- [Acknowledgements](#acknowledgements)

## Introduction
This project involves analyzing a dataset from the Google Play Store. The objective is to extract insights from the data, such as the relationship between app categories and their ratings, installs, and prices. The analysis includes data preprocessing, cleaning, and visualization.

## Dataset
The dataset used in this project is the Google Play Store dataset, which contains information about various applications. The dataset includes the following columns:
- App Name
- App Id
- Category
- Rating
- Rating Count
- Installs
- Minimum Installs
- Maximum Installs
- Free
- Price
- Currency
- Size
- Minimum Android
- Developer Id
- Developer Website
- Developer Email
- Released
- Last Updated
- Content Rating
- Privacy Policy
- Ad Supported
- In App Purchases
- Editors Choice
- Scraped Time

## Project Structure
The project directory is structured as follows:
```
google-play-data-analysis/
├── data/
│   └── Google-Playstore.csv
├── src/
│   └── analysis.py
└── README.md
```

## Installation
To run this project, ensure you have Python installed on your system. You will also need to install the following Python libraries:
- pandas
- numpy
- matplotlib

You can install these libraries using pip:
```bash
pip install pandas numpy matplotlib
```

## Usage
1. Clone the repository:
```bash
git clone https://github.com/yourusername/google-play-data-analysis.git
```
2. Navigate to the project directory:
```bash
cd google-play-data-analysis
```
3. Run the analysis script:
```bash
python src/analysis.py
```

## Data Preprocessing
The data preprocessing steps include:
1. **Importing Libraries:**
    ```python
    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    ```
2. **Loading the Dataset:**
    ```python
    csv_file = pd.read_csv('data/Google-Playstore.csv')
    initial_data_frame = pd.DataFrame(csv_file)
    ```
3. **Inspecting the Dataset:**
    ```python
    print(initial_data_frame.columns)
    ```
4. **Separating Numerical and String Data:**
    ```python
    numerical_base_dataframe = pd.DataFrame(initial_data_frame, columns=['Category', 'Rating', 'Installs', 'Price'])
    string_base_dataframe = pd.DataFrame(initial_data_frame, columns=['Category', 'Free', 'Currency'])
    ```
5. **Handling Missing Values:**
    ```python
    NAN_cleared_initila_dataframe = initial_data_frame.dropna()
    NAN_cleared_numerical_base_dataframe = numerical_base_dataframe.dropna()
    NAN_cleared_string_base_dataframe = string_base_dataframe.dropna()
    ```
6. **Converting Data Types:**
    ```python
    NAN_cleared_numerical_base_dataframe['Installs'] = pd.to_numeric(NAN_cleared_numerical_base_dataframe['Installs'].str.rstrip('+'), errors='coerce')
    ```

## Analysis and Visualization
Various analyses and visualizations are performed to extract insights:
1. **Descriptive Statistics:**
    ```python
    print(NAN_cleared_numerical_base_dataframe.describe(include='all'))
    print(NAN_cleared_string_base_dataframe.describe(include='all'))
    ```
2. **Group By and Mean Calculation:**
    ```python
    final_initial_dataframe = NAN_cleared_numerical_base_dataframe.groupby('Category')[['Rating', 'Installs', 'Price']].mean()
    final_initial_dataframe = final_initial_dataframe.reset_index()
    ```
3. **Visualizations:**
    - **Rating vs Category:**
        ```python
        plt.figure(figsize=(15,8))
        plt.scatter(final_initial_dataframe['Category'], final_initial_dataframe['Rating'])
        plt.title('Rating vs Category')
        plt.xlabel('Category')
        plt.ylabel('Rating')
        plt.xticks(rotation=90)
        plt.grid()
        plt.show()
        ```
    - **Installs vs Category:**
        ```python
        plt.figure(figsize=(15,8))
        plt.scatter(final_initial_dataframe['Category'], final_initial_dataframe['Installs'])
        plt.xlabel('Category')
        plt.ylabel('Installs')
        plt.title('Installs vs Category')
        plt.grid()
        plt.xticks(rotation=90)
        plt.show()
        ```
    - **Price vs Category:**
        ```python
        plt.figure(figsize=(15,8))
        plt.scatter(final_initial_dataframe['Category'], final_initial_dataframe['Price'])
        plt.xlabel('Category')
        plt.ylabel('Price')
        plt.title('Price vs Category')
        plt.grid()
        plt.xticks(rotation=90)
        plt.show()
        ```
    - **Count of True and False Values:**
        ```python
        value_counts = NAN_cleared_string_base_dataframe['Free'].value_counts()
        value_counts.plot(kind='bar', rot=0)
        plt.title('Count of True and False Values')
        plt.xlabel('Value')
        plt.ylabel('Count')
        plt.show()
        ```
    - **Count of Different Currencies:**
        ```python
        currency_count = NAN_cleared_string_base_dataframe['Currency'].value_counts()
        currency_count.plot(kind='bar', rot=0)
        plt.title('Count of Different Currencies')
        plt.xlabel('Currency')
        plt.ylabel('Count')
        plt.show()
        ```
    - **Rating vs Price:**
        ```python
        plt.figure(figsize=(15,8))
        plt.scatter(final_initial_dataframe['Rating'], final_initial_dataframe['Price'])
        plt.xlabel('Rating')
        plt.ylabel('Price')
        plt.title('Rating vs Price')
        plt.grid()
        plt.xticks(rotation=90)
        plt.show()
        ```
    - **Installs vs Price:**
        ```python
        plt.figure(figsize=(15,8))
        plt.scatter(final_initial_dataframe['Installs'], final_initial_dataframe['Price'])
        plt.xlabel('Instals')
        plt.ylabel('Price')
        plt.title('Installs vs Price')
        plt.grid()
        plt.xticks(rotation=90)
        plt.show()
        ```

## Results
The analysis revealed several insights, such as:
- The average ratings, installs, and prices across different app categories.
- The distribution of free and paid apps.
- The usage of different currencies for app pricing.

## Conclusion
This project demonstrates how to preprocess, clean, and analyze a large dataset. The visualizations provide valuable insights into the app market on the Google Play Store. Further analysis can be conducted to explore other aspects of the dataset.

## Acknowledgements
This project was inspired by the need to understand the Google Play Store app market better. The dataset was sourced from [Google Play Store](https://www.kaggle.com/lava18/google-play-store-apps).
