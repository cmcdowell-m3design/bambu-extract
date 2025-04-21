
## 📌 Feature: Total Price Calculation

### ✨ Overview
Add dynamic pricing calculations to the summary table and export formats. The total price per print job will be calculated as:

Total Price = (Total Grams × Per-Gram Rate) + Flat Rate

### 🛠 Implementation Details
- **Input Controls:**
  - Add two input text boxes to the UI:
    - **Per-Gram Cost** (default: `$0.40`)
    - **Flat Rate** (default: `$23.20`)
  - Inputs should accept decimal currency values (e.g. `0.35`, `25.00`)
  - Add an **“Update Prices”** button to trigger recalculation and table refresh.

- **Behavior:**
  - When the page loads, the default values are auto-filled in the fields.
  - On pressing “Update Prices”, the table recalculates the total cost for each row using:
    - Sum of all filament weights (grams)
    - Formula: `(sum of filament weights × per-gram cost) + flat rate`
  - Add a **new column to the table and exports**: `Total Price (USD)`, formatted to two decimal places with `$`. 
  - XLSX export should include this actual formula, not the hard coded results. CSV export will need to include hard coded results. 

- **Exports:**
  - Include the calculated total price in both the **CSV** and **Excel** outputs.
  - The column should appear at the end of each row.

### 🔄 Affects
- Table rendering (`renderTable()`)
- Export logic for CSV and XLSX
- HTML interface (new inputs and update button)

### ✅ Goals
- Enable billing visibility for shared-use 3D printing scenarios.
- Keep calculations transparent and editable for various cost models.

