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
  - Add an **"Update Prices"** button to trigger recalculation and table refresh.

- **Behavior:**
  - When the page loads, the default values are auto-filled in the fields.
  - On pressing "Update Prices", the table recalculates the total cost for each row using:
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

### 🚀 Implementation Plan
1. **UI Addition**
   - Add input fields for Per-Gram Cost and Flat Rate above the table
   - Add validation to ensure only valid decimal currency values are accepted
   - Add the "Update Prices" button

2. **Calculate Total Filament Weight**
   - Create a helper function to sum all filament weights for each print job
   - Handle the case where filament weights may be missing or invalid

3. **Modify Table Rendering**
   - Update the `prepareGroupedData()` function to include price calculation
   - Modify the `renderTable()` function to display the new price column
   - Format prices as currency with dollar sign and two decimal places

4. **Update Export Functions**
   - Modify CSV export to include the calculated prices
   - For Excel export, implement proper formulas that reference cell values
   - Ensure consistent column ordering across UI and exports

### 📝 Implementation Notes
- Input validation should allow numbers with up to two decimal places
- Default to treating empty/invalid filament weights as 0 grams
- For the Excel export, use SheetJS cell references in formulas
- The calculation should run automatically on initial load and when "Update Prices" is clicked

