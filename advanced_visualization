import streamlit as st
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

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

def plot_contingency_table(data, y_combs, category):
    num_plots = len(y_combs)
    cols = 2
    rows = (num_plots + 1) // cols
    fig, axes = plt.subplots(rows, cols, figsize=(10 * cols, 6 * rows))
    axes = axes.flatten()
    for i, y_comb in enumerate(y_combs):
        filtered_data = data[data['Y'] == y_comb]
        contingency_table = pd.crosstab(filtered_data[category], filtered_data['Y'])
        sns.heatmap(contingency_table, annot=True, fmt="d", cmap='viridis', ax=axes[i])
        axes[i].set_title(f'Contingency Table of {category} and Y = {y_comb}')
    plt.tight_layout()
    st.pyplot(fig)

def main():
    st.title("Heart Disease Data Visualization")
    uploaded_file = st.file_uploader("Upload a dataset (.csv)", type=["csv"])

    if uploaded_file:
        data = load_dataset(uploaded_file)
        data = create_y_variable(data)

        if st.checkbox("Exclude (0, 0, 0) from Y?"):
            data = data[data['Y'] != 'None']

        categories = list(data.columns.difference(['Y', 'HeartDiseaseorAttack', 'Stroke', 'Diabetes']))
        y_combs = st.multiselect("Select Y Combinations:", sorted(data['Y'].unique()), default=data['Y'].unique())
        category = st.selectbox("Select a Category for Contingency Table:", categories)

        if st.button("Show Contingency Tables"):
            plot_contingency_table(data, y_combs, category)

if __name__ == "__main__":
    main()
