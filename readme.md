# 🧬 CLD Clone Selection Simulation Dashboard

A modular, Streamlit-powered dashboard to simulate clone screening workflows for Cell Line Development (CLD). This tool estimates the probability that the final selected clones are within the top X% of performers using Monte Carlo simulations, customizable workflow parameters, and flexible distribution modeling (LogNormal or KDE).

## What is CLD?

Cell Line Development (CLD) is a foundational process in the production of biopharmaceuticals, especially for biologics like monoclonal antibodies, recombinant proteins, and cell-based therapies. It refers to the generation, screening, and optimization of cell lines capable of consistently producing a desired therapeutic product at high yields and with quality suitable for regulatory approval.
## 💡 Why Simulate Clone Selection?

Simulations using tools like Monte Carlo can:

-🧠 Model the effects of assay noise and clone variability
-📊 Help design better workflows and thresholds
-🔍 Estimate the probability of successful clone capture (i.e., retaining top X% of performers)
-🚀 Reduce experimental overhead by guiding better decision-making upstream saving money

## 📊 Features

- 📈 Visualize assay distributions for all criteria  
- ⚙️ Choose between LogNormal (parametric) and KDE (non-parametric) modeling  
- 🔁 Run Monte Carlo simulations across correlation values  
- 📉 Compare real vs synthetic data distributions  
- 📊 Plot clone success histograms and probability curves  

## 📁 Input Format

The uploaded Excel file should contain:

- A `Results` column with assay values (**required**)  
- Optional `CriteriaX` columns (e.g., `Criteria1`, `Criteria2`…) used for filtering  

## 🛠 How to Run

### Clone the repo:
```
git clone https://github.com/your-username/cld-clone-simulation.git
cd cld-clone-simulation
```

### (Optional) Set up a virtual environment:
```
python -m venv venv
source venv/bin/activate  # Windows: venv\Scriptsctivate
```

### Install dependencies:
```
pip install -r requirements.txt
```

### Launch the app:
```
streamlit run app.py
```

## 🧠 Why KDE over GMM?

- ✅ **Avoids Overfitting** – KDE is smoother and generalizes better  
- 🎯 **No Component Guesswork** – No need to select number of clusters  
- 📐 **Captures Complex Distributions** – Better fit for skewed or multimodal data  
- 🚀 **Faster & Simpler** – Non-iterative and robust for small samples  
- 🔁 **Better Simulation Behavior** – KDE yields more realistic Monte Carlo results  

## 🧬 Full Project Explanation

### 🔍 Objective

This dashboard models the cell line development workflow where multiple rounds of screening assays are conducted, and the goal is to retain the best-performing clones. It estimates how likely it is that the clones selected at the final step are in the top X% of the original population.

### ⚙️ Workflow Logic

- **Step 1 (Assay F):** All clones are sampled  
- **Step 2 (Assay G):** Clones from step 1 are re-evaluated with correlated synthetic noise  
- **Step 3 (Assay H):** Optional final round (if 3-step workflow is selected)  

At each step:
- You retain a fraction of clones  
- Synthetic assay values are generated using a correlation coefficient  
- Optional filtering criteria are applied at any step  

## 🧪 Simulation Engine

- Monte Carlo simulation runs thousands of times to estimate success probability  
- LogNormal or KDE used to generate synthetic assay distributions  
- Correlation between steps is applied mathematically  
- Filtering criteria can be enforced before or after selection  

## 📈 Dashboard Functionality

- Sidebar controls for simulation parameters  
- Histogram plots for all criteria columns  
- Synthetic vs real distribution overlay  
- Success probability vs correlation plot  
- Final clone success histograms  
- State caching using `st.session_state` for performance  

## 🗂️ File Structure

```
.
├── app.py               # Main Streamlit entry point
├── loader.py            # Handles file upload & sheet parsing
├── sidebar.py           # Configures sidebar widget logic
├── simulation.py        # Monte Carlo simulation engine
├── plots.py             # Handles all matplotlib-based plots
├── requirements.txt     # Python dependencies
└── README.md            # This file
```

## 📦 Dependencies

- streamlit >= 1.30  
- pandas >= 1.5.0  
- numpy >= 1.23.0  
- scipy >= 1.10.0  
- matplotlib >= 3.7.0

Install them with:
```
pip install -r requirements.txt
```

## 📌 Use Cases

- Clone screening strategy evaluation  
- Sensitivity analysis for experimental workflows  
- Optimizing thresholds in cell line development pipelines  
- Educational tool for bioinformatics or biotech teams  
