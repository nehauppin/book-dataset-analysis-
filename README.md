# book-dataset-analysis-
Part 2: Data Integration

## Project Overview
This project extends the original Amazon bestselling books analysis by integrating additional data from a Goodreads dataset to perform a comparative analysis.

### Datasets Used
1. Amazon Top Selling Books 2023
   - Source: Kaggle
   - Contains: approx. 4000 bestselling books with ratings, reviews and pricing data from 2023
2. Goodreads Book Awards 2023
   - Source: Kaggle
   - Contains: award-winning books from 2023 with author information, titles, and ratings 

### Data Cleaning
- Standardized author names across both datasets (lowercase, whitespace normalization)
- Created `Author_cleaned` column as the merge key
- Preserved original author names for reference

### Merge Strategy
- Join Type: Left Join
- Rationale: Preserves all Amazon bestselling books while provding awards data when matched
- Match Rate: 7.39% of Amazon bestsellers appear in the Goodreads award data
