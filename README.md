[![Shipping files](https://github.com/neuefische/ds-ml-project-template/actions/workflows/workflow-02.yml/badge.svg?branch=main&event=workflow_dispatch)](https://github.com/neuefische/ds-ml-project-template/actions/workflows/workflow-02.yml)

# STEG Fraud Detection Project

## Project Background

This project was developed as part of a private hackathon for participants in InstaDeep’s Data Science Program, held in collaboration with Google.

The Tunisian Company of Electricity and Gas (STEG) is a public, non-administrative entity responsible for the distribution of electricity and gas throughout Tunisia. In recent years, STEG has faced severe financial challenges, recording losses of approximately 200 million Tunisian Dinars. These losses are largely attributed to fraudulent meter manipulations and sophisticated theft patterns by consumers.

## The Objective

The goal of this Machine Learning project is to analyze historical billing data to detect and recognize clients involved in fraudulent activities. By automating the detection process, the solution helps STEG:
- Recover lost revenue.
- Minimize the need for inefficient manual inspections.
- Secure the integrity of the national energy grid.

## Data Overview
The analysis is based on two primary datasets provided by STEG, covering the period from 2005 to 2019.

1. Client Dataset
This file provides the demographic and categorical profile of each customer.
- Client_id: Unique identifier for the client.
- District/Region: Geographical location codes.
- Client_catg: The category of the client (e.g., residential, industrial).
- Creation_date: The date the client’s contract began.
- Target: The label to predict (1 for Fraud, 0 for Clean).

2. Invoice Dataset
This file contains the billing history and meter reading details.
- Invoice_date: When the bill was issued.
- Tarif_type: The specific tax/tariff bracket.
- Counter_number: The unique ID of the physical meter.
- Counter_statue: The state of the meter (e.g., Working, Broken, or On Hold).
- Reading_remarque: Qualitative notes from STEG agents during site visits (often contains clues about tampering).
- Consommation_level_1 to 4: Consumption data split into four different tiers/levels.
- Old/New_index: The previous and current meter readings used to calculate usage.
- Months_number: The duration of the billing cycle.
- Counter_type: Indicates whether the service is Electricity or Gas.

## Methodology
To address the problem, the following steps were taken:

1. Data Integration: Merging invoice history with client profiles to create a comprehensive view of each user.
2. Feature Engineering: Creating new metrics, such as the average consumption per month and the frequency of "bad" reading remarks.
3. Handling Imbalance: Since fraud is much rarer than normal usage, estimation techniques like Recall have been considered
4. Modeling: Utilizing gradient-boosted decision trees (like XGBoost) to handle the mixed categorical and numerical data.


---
## Set up your Environment

### **`macOS`** type the following commands : 

- For installing the virtual environment you can either use the [Makefile](Makefile) and run `make setup` or install it manually with the following commands:

     ```BASH
    make setup
    ```
    After that active your environment by following commands:
    ```BASH
    source .venv/bin/activate
    ```
Or ....
- Install the virtual environment and the required packages by following commands:

    ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/bin/activate
    pip install --upgrade pip
    pip install -r requirements.txt
    ```
    
### **`WindowsOS`** type the following commands :

- Install the virtual environment and the required packages by following commands.

   For `PowerShell` CLI :

    ```PowerShell
    pyenv local 3.11.3
    python -m venv .venv
    .venv\Scripts\Activate.ps1
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```

    For `Git-bash` CLI :
  
    ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/Scripts/activate
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```

    **`Note:`**
    If you encounter an error when trying to run `pip install --upgrade pip`, try using the following command:
    ```Bash
    python.exe -m pip install --upgrade pip
    ```


   
## Usage

In order to train the model and store test data in the data folder and the model in models run:

**`Note`**: Make sure your environment is activated.

```bash
python example_files/train.py  
```

In order to test that predict works on a test set you created run:

```bash
python example_files/predict.py models/linear_regression_model.sav data/X_test.csv data/y_test.csv
```

## Limitations

Development libraries are part of the production environment, normally these would be separate as the production code should be as slim as possible.


---

## Handling Merge Conflicts in Jupyter Notebooks

When working in teams, `.ipynb` files can cause messy merge conflicts because they’re JSON-based.  
We use **nbdime** to make this easy.

### Setup (run once)
```bash
nbdime config-git --enable
```

### When a conflict happens
```bash
nbdime mergetool
```

A web interface will open showing both notebook versions side by side.
Choose what to keep, save and close tool, then:
```bash
git add your_notebook.ipynb
git commit -m "Resolved notebook conflict"
```
That’s it — clean merges for notebooks!
