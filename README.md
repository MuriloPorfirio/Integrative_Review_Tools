# Rayyan Tools for Integrative Review

A collection of tools designed to make integrative review workflows easier, specifically for researchers using [Rayyan](https://www.rayyan.ai/) to manage bibliographic references.

These scripts were created to remove duplicates, filter articles by keywords, and split CSV files into sizes compatible with Rayyan's upload limits.  
They are tailored for scenarios where Rayyan's premium features are unavailable, forcing tedious manual work.

Important:  
Before using any script, read the `LICENSE.txt` file.  
These scripts are released under a NonCommercial-Attribution license — you may use and adapt them only for non-commercial purposes, and you must credit the original authors.

## Repository Contents

| File Name | Type | Description | When to Use in an Integrative Review |
|-----------|------|-------------|--------------------------------------|
| **`rayyan-duplicate-remover.html`** | HTML (Browser) | Removes exact duplicates from CSVs exported from Rayyan. Works entirely in the browser, no installation needed. | Use before screening to clean obvious duplicate records quickly. |
| **`rayyan-keyword-filter.html`** | HTML (Browser) | Filters articles based on a list of desired keywords found in title, abstract, or keywords columns. | Use when you want to pre-filter articles by topic before screening. |
| **`rayyan-mandatory-keywords-filter.html`** | HTML (Browser) | Keeps only articles containing all mandatory keywords you specify. | Use when refining your dataset to a very specific research question. |
| **`rayyan-duplicate-remover.py`** | Python | Removes duplicates from Rayyan CSV files with advanced strategies (title variations, abstract checks). Splits large outputs into ≤90MB files for re-upload. | Use when you need batch duplicate removal beyond simple exact matches. |

## License

These scripts are licensed under the Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0) license.

- You can share and adapt the scripts for research or personal use.
- You cannot use them for commercial purposes.
- You must credit the original authors:
  ```
  Murilo Porfírio, Julia Hailer, and Jéssica Ferreira
  ```

Read the full license in [`LICENSE.txt`](LICENSE.txt).

## Requirements

### For HTML Scripts
- Any modern web browser (Chrome, Firefox, Edge, etc.)
- No installation or dependencies required.
- CSV files exported from Rayyan with `title`, `abstract`, and `keywords` columns.

### For Python Scripts
- Python 3.8+
- Required Python packages:
  ```bash
  pip install pandas tqdm
  ```
- Optional (for GUI file picker):
  - `tkinter` (usually included with Python)

## How to Use

### 1. HTML Scripts
1. Download the `.html` file you want to use.
2. Open it in your browser (double-click or right-click → "Open with Browser").
3. Follow the on-screen instructions.
4. The processed CSV(s) will download automatically.

Example: Using `rayyan-duplicate-remover.html`
- Step 1: Select your exported Rayyan CSV file.
- Step 2: The script removes exact duplicates.
- Step 3: Download the cleaned CSV file.

### 2. Python Script
1. Install Python and required libraries:
   ```bash
   pip install pandas tqdm
   ```
2. Run the script:
   ```bash
   python rayyan-duplicate-remover.py
   ```
3. Use the file picker to select one or more Rayyan CSVs.
4. The script will:
   - Merge all files.
   - Apply multiple duplicate-removal strategies.
   - Split the output into ≤90MB files.

## Possible Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| Script says column not found | Your CSV does not have the required `title`, `abstract`, or `keywords` column. | Re-export from Rayyan ensuring these fields are included. |
| Output file not downloading (HTML) | Browser blocked automatic download. | Use the manual download button shown at the end. |
| Encoding errors in Python script | Special characters in CSV (e.g., accents, symbols). | Try re-exporting CSV with UTF-8 encoding. |
| Tkinter error in Python | `tkinter` not installed. | Install it via your OS package manager (Linux) or reinstall Python with Tcl/Tk support. |

## Recommended Workflow for an Integrative Review

1. Export dataset from Rayyan (all articles, including duplicates).
2. Run `rayyan-duplicate-remover.html` to clean exact duplicates.
3. Run `rayyan-keyword-filter.html` to pre-filter by topic (optional).
4. Run `rayyan-mandatory-keywords-filter.html` to narrow to highly relevant papers.
5. Re-import cleaned dataset into Rayyan for final screening.

## Authors
- Murilo Porfírio
- Julia Hailer
- Jéssica Ferreira

## Citation
If you use these scripts in a published work, please cite the authors and the repository:

```
Porfírio, M., Hailer, J., & Ferreira, J. (2025). Rayyan Tools for Integrative Review. GitHub repository.
```

## Notes
- These scripts do not use similarity percentages — they focus on exact or rule-based duplicate detection.
- HTML scripts run entirely locally in your browser — your data never leaves your computer.
- Large datasets are automatically split to respect Rayyan's 100MB upload limit.
