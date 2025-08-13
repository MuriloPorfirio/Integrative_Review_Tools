"""
Rayyan CSV Duplicate Remover
============================

Purpose:
--------
This script was designed to automatically remove duplicate articles from CSV datasets
exported from the Rayyan platform. It is intended for researchers conducting
Systematic Reviews or Integrative Reviews who want to clean large datasets efficiently.

Why use this script?
--------------------
- In the free version of Rayyan, removing duplicates is manual and limited to 50% similarity detection.
- This means you might have thousands of duplicates left, which would require tedious manual removal.
- This script applies a combination of exact and approximate matching strategies to detect and remove duplicates.

What it does:
-------------
1. Loads one or more CSV files exported from Rayyan.
2. Removes exact duplicates based on the article title.
3. Removes approximate duplicates by altering titles in specific ways (removing first, last, second, or middle words).
4. Optionally removes duplicates based on the abstract text.
5. Splits the cleaned dataset into parts of up to 90 MB for easy re-import into Rayyan.

When to use:
------------
Use this script right after exporting your complete dataset from Rayyan,
before screening, to ensure minimal duplication and avoid manual work.

Compatibility:
--------------
- Works in Python 3.
- Tested in VSCode, PyCharm, and command-line environments.
- Requires the following Python libraries:
    pandas, tqdm, tkinter (standard library for file dialogs).

Usage:
------
1. Install dependencies:
    pip install pandas tqdm
2. Run the script:
    python rayyan_duplicate_remover.py
3. Select the CSV file(s) exported from Rayyan.
4. Wait for the cleaning process to complete.
5. Find your cleaned CSV files in the same directory.

Authors: Murilo Porfírio, Julia Hailer, and Jéssica Ferreira.
Reviwed by 
-------
Adapted and translated for clarity and usability.
"""

import pandas as pd
import os
from tkinter import Tk
from tkinter.filedialog import askopenfilenames
from tqdm import tqdm  # Progress bar

# -----------------------------
# Duplicate Removal Functions
# -----------------------------

def remove_exact_duplicates(df, column_name):
    """
    Remove exact duplicates based on the given column.
    """
    return df.drop_duplicates(subset=[column_name])

def remove_word_and_compare(df, column_name, word_position):
    """
    Remove duplicates by ignoring a specific word position in the title.
    This helps capture duplicates with minor word variations.

    Parameters:
    - word_position:
        0  -> remove first word
        -1 -> remove last word
        1  -> remove second word
        2  -> remove middle word
    """
    seen_titles = set()
    unique_rows = []

    for _, row in tqdm(df.iterrows(), total=len(df), desc="Processing Word Removals"):
        title_words = str(row[column_name]).strip().split()

        if len(title_words) > abs(word_position):
            if word_position == 0:
                modified_title = " ".join(title_words[1:])
            elif word_position == -1:
                modified_title = " ".join(title_words[:-1])
            elif word_position == 1:
                modified_title = title_words[0] + " " + " ".join(title_words[2:])
            elif word_position == 2:
                middle_index = len(title_words) // 2
                modified_title = " ".join(title_words[:middle_index] + title_words[middle_index+1:])
            else:
                modified_title = " ".join(title_words)

            if modified_title not in seen_titles:
                seen_titles.add(modified_title)
                unique_rows.append(row)

    return pd.DataFrame(unique_rows)

def remove_abstract_duplicates(df, abstract_column):
    """
    Remove duplicates based on the abstract text.
    """
    return df.drop_duplicates(subset=[abstract_column])

# -----------------------------
# File Splitting Function
# -----------------------------

def split_csv_file(df, base_filename, max_size_mb=90):
    """
    Split the DataFrame into multiple CSV files of a specified max size (in MB).
    This is necessary because Rayyan's import limit is 100 MB per file.
    """
    max_size_bytes = max_size_mb * 1024 * 1024
    part_number = 1
    current_size = 0
    chunk = []

    for _, row in tqdm(df.iterrows(), total=len(df), desc="Splitting Files"):
        row_str = row.to_csv(index=False)
        row_size = len(row_str.encode('utf-8'))
        chunk.append(row)

        current_size += row_size
        if current_size > max_size_bytes:
            save_chunk(chunk, base_filename, part_number)
            part_number += 1
            chunk = []
            current_size = 0

    if chunk:
        save_chunk(chunk, base_filename, part_number)

def save_chunk(chunk, base_filename, part_number):
    """
    Save a chunk of the DataFrame to a CSV file.
    """
    chunk_df = pd.DataFrame(chunk)
    filename = f"{base_filename}_part_{part_number}.csv"
    chunk_df.to_csv(filename, index=False)
    print(f"Saved: {filename}")

# -----------------------------
# File Selection and Processing
# -----------------------------

def select_files():
    """
    Open a file dialog to select one or more CSV files.
    """
    root = Tk()
    root.withdraw()  # Hide main window
    file_paths = askopenfilenames(filetypes=[("CSV files", "*.csv")])
    return file_paths

def process_files(file_paths):
    """
    Process the selected CSV files:
    - Load
    - Remove duplicates
    - Save cleaned files
    """
    dfs = []
    for file in file_paths:
        print(f"Loading: {file}")
        chunks = pd.read_csv(file, low_memory=False, chunksize=5000)
        for chunk in chunks:
            dfs.append(chunk)

    df_combined = pd.concat(dfs, ignore_index=True)
    print("Columns detected:", df_combined.columns.tolist())

    # Remove exact duplicates by title
    df_no_exact_duplicates = remove_exact_duplicates(df_combined, column_name='title')

    # Remove word-based duplicates
    df_no_first_word = remove_word_and_compare(df_no_exact_duplicates, column_name='title', word_position=0)
    df_no_last_word = remove_word_and_compare(df_no_first_word, column_name='title', word_position=-1)
    df_no_second_word = remove_word_and_compare(df_no_last_word, column_name='title', word_position=1)
    df_no_middle_word = remove_word_and_compare(df_no_second_word, column_name='title', word_position=2)

    # Remove duplicates by abstract if present
    if 'abstract' in df_combined.columns:
        df_final = remove_abstract_duplicates(df_no_middle_word, abstract_column='abstract')
    else:
        df_final = df_no_middle_word

    # Save output files
    base_filename = "rayyan_cleaned_articles"
    split_csv_file(df_final, base_filename=base_filename, max_size_mb=90)

# -----------------------------
# Main Execution
# -----------------------------

if __name__ == "__main__":
    print("=== Rayyan Duplicate Remover ===")
    print("This tool removes duplicate articles from CSV files exported from Rayyan.\n")
    print("Steps:")
    print("1. Select one or more CSV files exported from Rayyan.")
    print("2. The script will remove duplicates using several matching strategies.")
    print("3. Cleaned CSV files will be saved in the current directory.\n")

    file_paths = select_files()
    if file_paths:
        process_files(file_paths)
    else:
        print("No files selected. Exiting.")
