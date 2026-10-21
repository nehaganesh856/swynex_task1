# Titanic Data Cleaning Project

A comprehensive data-cleaning and preprocessing pipeline for the classic Titanic passenger dataset using Python, **pandas**, **NumPy**, and **Jupyter Notebook**.

---

## 📌 Project Objective

The goal of this project is to clean, standardize, and prepare raw Titanic passenger records for exploratory data analysis (EDA) and predictive machine learning models. Real-world datasets often suffer from missing entries, inconsistent string casing, trailing whitespaces, and suboptimal data types. This pipeline addresses each data quality issue systematically with reproducible, documented transformations.

---

## 📊 Dataset Used

- **Filename**: `data/Titanic-Dataset.csv`
- **Observations**: 891 rows × 12 columns
- **Features**:
  - `PassengerId`: Unique identifier for each passenger
  - `Survived`: Survival status (0 = No, 1 = Yes)
  - `Pclass`: Ticket class (1 = 1st, 2 = 2nd, 3 = 3rd)
  - `Name`: Full passenger name
  - `Sex`: Gender of the passenger
  - `Age`: Age in years
  - `SibSp`: Number of siblings / spouses aboard the Titanic
  - `Parch`: Number of parents / children aboard the Titanic
  - `Ticket`: Ticket number
  - `Fare`: Passenger fare
  - `Cabin`: Cabin number
  - `Embarked`: Port of embarkation (C = Cherbourg, Q = Queenstown, S = Southampton)

> [!NOTE]
> ### Dataset Download Instruction (If File is Missing)
> If `data/Titanic-Dataset.csv` is not present in your local clone, please download `Titanic-Dataset.csv` from [Kaggle Titanic Dataset](https://www.kaggle.com/datasets/yasserh/titanic-dataset) (or the official Kaggle Titanic Competition dataset) and save it directly into the `data/` directory:
> ```bash
> # Path to place the file:
> data/Titanic-Dataset.csv
> ```

---

## 📁 Folder Structure

```text
titanic-data-cleaning/
│
├── data/
│   ├── Titanic-Dataset.csv       # Raw Titanic passenger dataset
│   └── titanic_cleaned.csv       # Cleaned, standardized, ready-for-analysis dataset
│
├── notebooks/
│   └── titanic_data_cleaning.ipynb  # Step-by-step interactive Jupyter notebook
│
├── .gitignore                    # Git ignore file for Python/Jupyter artifacts
├── README.md                     # Project documentation
└── requirements.txt              # Project dependencies
```

---

## 🔍 Data-Quality Issues Found

| Issue | Columns Affected | Description / Metrics |
|---|---|---|
| **Missing Values** | `Age` | 177 missing entries (~19.87%) |
| **Missing Values** | `Cabin` | 687 missing entries (~77.10%) |
| **Missing Values** | `Embarked` | 2 missing entries (~0.22%) |
| **Duplicate Records** | All | 0 duplicate rows detected |
| **Inconsistent Text** | `Sex`, `Cabin`, `Name`, `Ticket` | Potential leading/trailing whitespace |
| **Casing Variations** | `Sex`, `Cabin` | String values not standardized in casing |
| **Data Types** | `Sex`, `Embarked`, `Pclass`, etc. | Categorical variables stored as generic objects |

---

## 🧹 Cleaning Steps Performed

1. **Dataset Inspection & Summary**:
   - Inspected first 5 records (`df.head()`).
   - Analyzed dimensions (`df.shape` = 891 rows, 12 columns).
   - Reviewed column headers, data types, and five-number statistical summaries (`df.describe(include='all')`).

2. **Missing Value Auditing**:
   - Calculated null counts (`df.isnull().sum()`) and exact percentages for each column.

3. **Deduplication Check**:
   - Scanned for duplicates using `df.duplicated().sum()`. Confirmed zero duplicate rows.

4. **Missing Value Imputation**:
   - **`Age`**: Imputed missing values with the median age (**`28.0` years**), which is robust to outliers and right-skewness.
   - **`Embarked`**: Imputed missing values with the statistical mode (**`'S'`** for Southampton, representing >72% of passengers).
   - **`Cabin`**: Because >77% of entries were missing, nulls were replaced with the explicit category placeholder **`"Unknown"`**.

5. **Text Formatting & Standardization**:
   - Stripped leading and trailing whitespace across all string/object columns.
   - Standardized `Sex` values to strictly lowercase (`male`, `female`).
   - Standardized `Cabin` values to uppercase (`UNKNOWN`, `C85`, etc.).

6. **Data Type Casting**:
   - **Integers**: `PassengerId`, `Survived`, `Pclass`, `SibSp`, `Parch` converted to `int`.
   - **Floats**: `Age`, `Fare` converted to `float`.
   - **Categories**: `Sex` and `Embarked` converted to `category` dtype for optimized memory usage and logical representation.

7. **Unique Value Verification**:
   - Checked unique values:
     - `Sex`: `['male', 'female']`
     - `Embarked`: `['S', 'C', 'Q']`
     - `Pclass`: `[3, 1, 2]`

8. **Integrity Validation**:
   - Asserted that zero missing values remain in `Age` and `Embarked`.

9. **Data Export**:
   - Saved final dataframe to `data/titanic_cleaned.csv` using `index=False`.

---

## 🛠️ Tools & Libraries Used

- **Python 3.x**
- **pandas**: Data loading, transformation, string manipulation, and CSV export
- **NumPy**: Numerical operations and missing value handling
- **Jupyter Notebook**: Interactive notebook environment

---

## 🚀 How to Run the Project

### 1. Prerequisites
Ensure Python 3.9+ is installed on your system.

### 2. Set Up Virtual Environment (Recommended)
```bash
# Navigate into the project folder
cd titanic-data-cleaning

# Create a virtual environment
python -m venv .venv

# Activate the virtual environment
# Windows (PowerShell):
.venv\Scripts\Activate.ps1
# Windows (Command Prompt):
.venv\Scripts\activate.bat
# macOS / Linux:
source .venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Launch Jupyter Notebook
```bash
jupyter notebook notebooks/titanic_data_cleaning.ipynb
```
Once Jupyter opens in your browser, select **Cell > Run All** to execute the pipeline.

---

## 📄 Output Files Generated

- **`data/titanic_cleaned.csv`**:
  - Contains all 891 records with zero missing values in `Age` and `Embarked`.
  - All text standardized and trimmed.
  - Proper integer, float, and categorical data types applied.
  - Ready for machine learning models and visualizations.
