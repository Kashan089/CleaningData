# IMDB Data Cleaning - Python Portfolio Project

## Project Overview
Data cleaning and preprocessing of a messy IMDB dataset containing movie information (titles, release years, genres, directors, ratings, box office income, votes, and scores). Handled encoding issues, inconsistent formats, special characters, and missing values.

## Dataset Issues Fixed

### Column Headers
- Removed special characters and non-ASCII text
- Renamed misspelled columns (`Genr` → `Genre`, `Original titl` → `Original Title`)
- Standardized column name formatting

### Text Data & Encoding
- **Original Titles**: Fixed latin1/utf-8 encoding issues
- **Director Names**: Cleaned encoding problems and filled nulls
- **Countries**: 
  - Standardized `US` → `USA`
  - Removed trailing numbers/dots
  - Fuzzy-matched "New Zealand" variations
  - Replaced 'nan' strings with empty values

### Numeric Data Cleaning

| Column | Issues Found | Fix Applied |
|--------|--------------|-------------|
| **Release Year** | Invalid formats | Converted to datetime with coercion |
| **Duration** | Non-numeric characters (letters, symbols) | Extracted only digits, filled nulls with 0 |
| **Income** | 'o' instead of '0', special characters | Replaced 'o' with '0', removed non-digits, divided by 10 |
| **Votes** | Dots as thousand separators, null values | Removed dots, filled nulls with 0 |
| **Score** | Commas, colons, multiple dots, leading zeros | Multiple cleaning passes to extract valid decimal |

### Categorical Data
- **Content Rating**: Filled null values with 'Not Rated'
- **Genre**: Column renamed and cleaned

## Key Cleaning Techniques Demonstrated

### Encoding Handling
```python
# Fixed latin1/utf-8 encoding issues
df['Original Title'] = (df['Original Title']
    .str.encode('latin1', errors='ignore')
    .str.decode('utf-8', errors='ignore')
)
