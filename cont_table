import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt
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

def entropy(prob):
    return -sum(p * log2(p) if p > 0 else 0 for p in prob)

def calculate_joint_prob(data, columns, values):
    filtered_data = data
    for col, val in zip(columns, values):
        filtered_data = filtered_data[filtered_data[col] == val]
    return len(filtered_data) / len(data) if len(data) > 0 else 0

def calculate_conditional_entropy(data, y_comb, all_categories, selected_categories, values_dict):
    data = data[data['Y'] == y_comb]
    if data.empty:
        st.write("Filtered data is empty after applying Y combination.")
        return {}

    entropy_values = {}
    total_entropy = 0
    for category in all_categories:
        if category not in ['HeartDiseaseorAttack', 'Stroke', 'Diabetes'] or category in selected_categories:
            values = values_dict.get(category, data[category].unique())
            cat_probs = [calculate_joint_prob(data, [category], [value]) for value in values]
            cat_entropy = entropy(cat_probs)
            entropy_values[category] = cat_entropy
            total_entropy += cat_entropy

    if total_entropy > 0:
        entropy_values = {k: v / total_entropy for k, v in entropy_values.items()}

    return entropy_values

def main():
    st.title("Heart Disease Data Visualization")
    uploaded_file = st.file_uploader("Upload a dataset (.csv)", type=["csv"])

    if uploaded_file:
        data = load_dataset(uploaded_file)
        data = create_y_variable(data)

        if st.checkbox("Exclude (0, 0, 0) from Y?"):
            data = data[data['Y'] != 'None']

        all_categories = list(data.columns.difference(['Y']))
        selected_categories = st.multiselect("Select categorical variables:", all_categories)
        values_dict = {}
        for category in selected_categories:
            values_dict[category] = st.multiselect(f"Select specific values for {category}:", sorted(data[category].unique()), key=f"values{category}")

        y_combinations = sorted(set(data['Y']))
        y_comb = st.selectbox("Select a Y Combination:", y_combinations)

        if st.button("Calculate Conditional Entropy for Factors"):
            cond_entropy_values = calculate_conditional_entropy(data, y_comb, all_categories, selected_categories, values_dict)
            if cond_entropy_values:
                sorted_categories = sorted(cond_entropy_values.items(), key=lambda x: x[1], reverse=True)
                categories, entropies = zip(*sorted_categories)
                cmap = plt.get_cmap('RdYlGn_r')
                plt.figure(figsize=(10, 6))
                plt.barh(categories, entropies, color=cmap(np.linspace(0, 1, len(categories))))
                plt.xlabel('Normalized Conditional Entropy')
                plt.title('Conditional Entropy of Risk-Factors')
                plt.gca().invert_yaxis()
                st.pyplot(plt)

if __name__ == "__main__":
    main()
