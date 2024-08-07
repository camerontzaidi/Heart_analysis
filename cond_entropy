import streamlit as st
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from math import log2

def load_dataset(filepath):
    return pd.read_csv(filepath)

def create_y_variable(data):
    conditions = {
        (0, 0, 0): 'None',
        (1, 0, 0): 'Heart Disease',
        (0, 1, 0): 'Stroke',
        (0, 0, 1): 'Diabetes',
        (1, 1, 0): 'Heart Disease + Stroke',
        (1, 0, 1): 'Heart Disease + Diabetes',
        (0, 1, 1): 'Stroke + Diabetes',
        (1, 1, 1): 'All Conditions'
    }
    data['Y'] = data.apply(lambda row: (
        int(row['HeartDiseaseorAttack']),
        int(row['Stroke']),
        1 if row['Diabetes'] in [1, 2] else 0
    ), axis=1)
    data['Y'] = data['Y'].map(conditions)
    return data

def covariance_matrix(data, y_comb):
    filtered_data = data[data['Y'] == y_comb]
    numeric_data = filtered_data.select_dtypes(include=[np.number])
    return numeric_data.cov()

def plot_histogram(data, factor):
    plt.figure(figsize=(10, 6))
    sns.histplot(data[factor], kde=True, color='skyblue')
    plt.title(f'Histogram of {factor}')
    plt.xlabel(factor)
    plt.ylabel('Frequency')
    st.pyplot(plt)

def plot_covariance_matrix(cov_matrix):
    plt.figure(figsize=(10, 6))
    sns.heatmap(cov_matrix, annot=True, cmap='coolwarm', fmt=".2f")
    plt.title('Covariance Matrix')
    st.pyplot(plt)

def main():
    st.title("Heart Disease Data Visualization")
    uploaded_file = st.file_uploader("Upload a dataset (.csv)", type=["csv"])

    if uploaded_file:
        data = load_dataset(uploaded_file)
        data = create_y_variable(data)

        if st.checkbox("Exclude (0, 0, 0) from Y?"):
            data = data[data['Y'] != 'None']

        categories = list(data.columns.difference(['Y']))
        y_comb = st.selectbox("Select a Y Combination:", sorted
