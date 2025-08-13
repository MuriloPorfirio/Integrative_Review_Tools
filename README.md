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
| **`rayyan-keyword-filter.html`** | HTML (Browser) | Filters articles based on a list of desired keywords found in title, abstract, or keywords columns. | Use when you want to pre-filter articles by topic before screening. |
| **`rayyan-mandatory-keywords-filter.html`** | HTML (Browser) | Keeps only articles containing all mandatory keywords you specify. | Use when refining your dataset to a very specific research question. |
| **`rayyan-duplicate-remover.py`** | Python | Removes duplicates from Rayyan CSV files with advanced strategies (title variations and optional abstract checks). Splits large outputs into up to 90 MB parts for re-upload. | Use early in the process to batch‑remove duplicates beyond simple exact matches. |

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
- Any modern web browser (Chrome, Firefox, Edge, etc.).
- No installation or dependencies required.
- CSV files exported from Rayyan with the columns `title`, `abstract`, and `keywords` (lowercase, as exported by Rayyan).

### For Python Script
- Python 3.8+
- Required Python packages:
  ```bash
  pip install pandas tqdm
  ```
- Optional (for GUI file picker):
  - `tkinter` (usually included with Python)
- CSV files exported from Rayyan. At minimum, the script expects `title`; if `abstract` exists it will also be used.

## How to Use

### 1. HTML Scripts
1. Download the `.html` file you want to use.
2. Open it in your browser (double-click or right-click → Open with Browser).
3. Follow the on-screen instructions.
4. The processed CSV(s) will download automatically.

- `rayyan-keyword-filter.html`: keeps records containing any of the provided keywords in title, abstract, or keywords.  
- `rayyan-mandatory-keywords-filter.html`: keeps records only if all provided keywords are present in at least one of the three fields.

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
   - Remove exact duplicates by title.
   - Remove near-duplicates by comparing title variants (removing first, last, second, and middle words).
   - Optionally remove duplicates by abstract if an `abstract` column exists.
   - Split the output into files of up to 90 MB for re-upload to Rayyan.

## Possible Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| Column not found | Your CSV does not have the required `title`, `abstract`, or `keywords` column. | Re-export from Rayyan ensuring these fields are included. |
| Output file not downloading (HTML) | Browser blocked automatic download. | Use the manual download button shown at the end. |
| Encoding errors (Python) | Special characters in CSV (e.g., accents, symbols). | Re-export CSV with UTF-8 encoding. |
| Tkinter error (Python) | `tkinter` not installed or missing GUI backend. | Install via OS package manager or reinstall Python with Tcl/Tk support. |
| Very large datasets slow to process | Browser or Python memory limits. | Run the Python deduplicator first to reduce the dataset, then apply HTML filters. |

## Recommended Workflow for an Integrative Review

1. Export the full dataset from Rayyan (all articles, with duplicates).
2. Run `rayyan-duplicate-remover.py` to clean duplicates and split into manageable files.
3. Run `rayyan-keyword-filter.html` to pre-filter by topic (optional).
4. Run `rayyan-mandatory-keywords-filter.html` to narrow to highly relevant papers.
5. Re-import cleaned dataset into Rayyan for title/abstract screening and full-text review.

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
- These tools do not use similarity percentages; they rely on exact or rule-based detection and keyword matching.
- HTML scripts run entirely locally in your browser; data is not uploaded anywhere.
- Large datasets are automatically split to respect Rayyan's approximate 100 MB upload limit.
