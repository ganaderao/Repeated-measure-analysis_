---

# Repeated Measures Analysis Using Mixed Effects Model

This script is designed to perform repeated measures analysis using a mixed-effects model. It includes functionalities for uploading a dataset, cleaning it, and fitting a statistical model with `statsmodels`. The script is especially useful for analyzing data with hierarchical or nested structures, such as animal studies.

## **Features**
1. Handles data upload directly in Google Colab.
2. Prepares and cleans the dataset, including renaming columns, removing duplicates, and handling missing values.
3. Implements a mixed-effects model to analyze repeated measures data, accounting for fixed and random effects.
4. Provides a detailed summary of the model fit.

---

## **Prerequisites**
1. **Python Libraries Required**:
   - `pandas`
   - `statsmodels`
   - `google.colab` (for Colab file upload functionality)

2. **Environment**:
   - Google Colab or any Jupyter Notebook environment that supports file uploads.

---

## **How to Use**
### Step 1: Clone the Repository
First, clone the repository from GitHub:
```bash
git clone https://github.com/<your-username>/<repository-name>.git
cd <repository-name>
```

### Step 2: Open the Script
Open the script in Google Colab or any Python IDE of your choice.

### Step 3: Upload Dataset
The script expects a CSV file with the following structure:
- **Columns**:
  - `Animal ID`: A unique identifier for each subject (e.g., an animal in an experiment).
  - `Treat`: Treatment group for each subject.
  - `Week`: Timepoint for repeated measurements.
  - `DMI`: Dependent variable (e.g., Dry Matter Intake).
  - Other columns will be ignored or removed automatically.

Use the file upload functionality to provide your dataset. Example:
```plaintext
Treat,Week,Animal ID,DMI
CON,1,1,1.30
CON,1,2,1.64
CON,1,3,2.27
...
```

### Step 4: Run the Script
Run the cells in the script sequentially. The script will:
1. Upload and read your dataset.
2. Clean and prepare the data.
3. Fit a mixed-effects model.
4. Output a detailed summary of the results.

### Step 5: Review Results
The results include:
- Coefficients for fixed effects (e.g., treatment, week).
- Interactions between variables (e.g., `Treat:Week`).
- Variance estimates for random effects.

---

## **Script Explanation**
### **Step 1: File Upload**
The script uses `google.colab.files.upload()` to allow users to upload a CSV file directly into Colab.

### **Step 2: Data Reading**
The uploaded CSV file is read into a Pandas DataFrame:
```python
file_name = list(uploaded.keys())[0]
data = pd.read_csv(file_name)
```

### **Step 3: Data Cleaning**
1. Unnecessary columns (e.g., unnamed columns) are removed.
2. The `Animal ID` column is renamed to `AnimalID` for consistency.
3. Missing values in the dependent variable (`DMI`) are dropped.

### **Step 4: Model Fitting**
The script fits a mixed-effects model using the formula:
```python
model = mixedlm("DMI ~ Treat * Week", data, groups=data["AnimalID"])
result = model.fit()
```
- **Fixed Effects**:
  - `Treat`: Treatment groups.
  - `Week`: Timepoints for repeated measurements.
  - `Treat * Week`: Interaction between treatment and time.
- **Random Effects**:
  - Individual subjects (`AnimalID`) are modeled as random effects.

### **Step 5: Output Results**
The script outputs a detailed summary of the model fit, including coefficients, standard errors, p-values, and variance estimates.

---

## **Error Handling**
The script includes error handling to:
- Check for missing or malformed columns (e.g., `AnimalID`).
- Handle missing values in the dependent variable (`DMI`).
- Raise appropriate error messages during model fitting.

---

## **Example Output**
Example of model summary:
```plaintext
           Mixed Linear Model Regression Results
===============================================================
Model:               MixedLM    Dependent Variable:    DMI    
No. Observations:    216        Method:                REML   
No. Groups:          24         Scale:                 0.039  
Min. group size:     9          Log-Likelihood:        -71.56
Max. group size:     9          Converged:             Yes    
Mean group size:     9.0                                      
---------------------------------------------------------------
                     Coef.  Std.Err.   z    P>|z| [0.025 0.975]
---------------------------------------------------------------
Intercept            1.456    0.820  1.776 0.076 -0.150  3.062
Treat[T.CON_HS]     -0.867    0.989 -0.877 0.381 -2.806  1.071
Treat[T.T1_HS]       0.971    0.989  0.982 0.326 -0.968  2.910
Treat[T.T2_HS]       1.275    0.989  1.289 0.197 -0.664  3.215
Week                 0.082    0.010  8.200 0.000  0.062  0.103
Treat[T.CON_HS]:Week 0.042    0.015  2.800 0.005  0.013  0.071
---------------------------------------------------------------
```

---

## **Customization**
You can modify the formula in `mixedlm()` to suit your dataset. For example, if you have additional covariates or interactions, include them in the formula string.

---

## **Contributing**
Contributions are welcome! Please fork the repository, make your changes, and submit a pull request.

---

## **License**
This project is licensed under the MIT License.

---

