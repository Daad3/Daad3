{
      "cell_type": "code",
      "source": "import pandas as pd\nfrom sklearn.preprocessing import LabelEncoder\n\n# Read the dataset\ndf = pd.read_csv('StressLevelcleaned_dataset.csv')\n\n# Because there is no categorical columns in the dataset, we assuming 'mental_health_history' is a categorical column with textual data like 'yes' and 'no'\n\nle = LabelEncoder()\ndf['mental_health_history'] = le.fit_transform(df['mental_health_history'])\nprint(df)",
      "metadata": {
        "trusted": true
      },
      "outputs": [],
      "execution_count": null
    },
    {
      "cell_type": "markdown",
      "source": "## selected features\nThe selected features: blood pressure, sleep quality, future career concerns, bullying, and stress level.",
      "metadata": {}
    },
    {
      "cell_type": "code",
      "source": "import pandas as pd\nimport numpy as np\nfrom sklearn.feature_selection import SelectKBest\nfrom sklearn.feature_selection import f_classif  # You can also use other statistical tests like chi2 for classification\n\n\n# Read the dataset\ndf = pd.read_csv('StressLevelcleaned_dataset.csv')\n\n# Separate features and target variable\nX = df.drop(columns=['anxiety_level'])\ny = df['anxiety_level']\n\n# Apply SelectKBest algorithm with f_classif (for classification) or f_regression (for regression)\nnum_features_to_select = 5  # Number of features to select\nselector = SelectKBest(score_func=f_classif, k=num_features_to_select)\nX_selected = selector.fit_transform(X, y)\n\n# Get the selected feature indices\nselected_indices = selector.get_support(indices=True)\n\n# Get the names of the selected features\nselected_features = X.columns[selected_indices]\n\nprint(\"Selected Features:\", selected_features)",
      "metadata": {
        "trusted": true
      },
      "outputs": [
        {
          "name": "stdout",
          "text": "Selected Features: Index(['blood_pressure', 'sleep_quality', 'future_career_concerns', 'bullying',\n       'stress_level'],\n      dtype='object')\n",
          "output_type": "stream"
        }
      ],
      "execution_count": 3
