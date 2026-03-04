# Amazon Bestselling Books 2023 vs. Goodreads Choice Awards 2023 — Exploratory Data Analysis

**Dataset Source:** Kaggle
**Tools Used:** Python, pandas, matplotlib, seaborn, Jupyter Notebook

## Project Overview

This project is a two-part Exploratory Data Analysis (EDA) that examines what makes a book successful in 2023 — combining data from **Amazon's bestseller list** and **Goodreads Book Awards** to uncover patterns across pricing, ratings, reviews, genre, and critical recognition.

**Part 1** focused on Amazon's bestselling books dataset, exploring price distributions, customer ratings, review counts, and genre breakdowns.

**Part 2** extended the analysis by integrating a Goodreads Book Awards dataset, enabling a comparative look at whether critically acclaimed books (award winners) overlap with commercial bestsellers — and what distinguishes the two.

### Datasets Used
1. Amazon Top Selling Books 2023 (Primary Dataset)
   - Source: Kaggle
   - Contains: approx. 4000 bestselling books with ratings, reviews and pricing data from 2023
2. Goodreads Book Awards 2023
   - Source: Kaggle
   - Contains: award-winning books from 2023 with author information, titles, and ratings 

### Part 1 - Amazon Bestsellers
#### Data Preparation
- Inspected data types, shape, and column names
- Checked for and handled missing values
- Identified and noted outliers in pricing and review counts
- Ensured consistent formatting across categories

#### Area of Analysis
1. **Pricing** - How are bestselling books priced? Are there significant outliers?
2. **Ratings** — What does the ratings distribution look like across bestsellers?
3. **Genre** — Which genres dominate the list, and does genre affect pricing?

### Part 2 - Goodreads Awards Integration
#### Data Preparation
- Standardized author names across both datasets (lowercase, whitespace normalization)
- Created `Author_cleaned` column as the merge key
- Preserved original author names for reference
- **Merge Strategy:** Left Join on `author_cleaned`, preserving all Amazon bestselling books while provding awards data when matched

#### Area of Analysis
1. **Overlap** — How much do commercial bestsellers and award-winning books overlap?
2. **Author Presence** — Which authors appear in both datasets?

## Key Findings
- The price of Amazon bestsellers are positively skewed, with a majority of books in the $5-15 range
- rating analysis focused on the top 25% most reviewed books to eliminate the the case of books with perfect score from very few reviews
- Fantasy accounts for 3.63% of all books, making it the most popular genre
- Over 900 unique genres were found
- Only 7.39% of Amazon Bestsellers appeared in the Goodreads Book Awards data, indicating that commercial success and recognition may be largely seperate

## AI Usage
AI tools were used throughout this project to assist with writing and debugging Python code, understanding pandas and matplotlib functions, and brainstorming workflows. All analytical decisions, interpretations, anc conclusions are my own. 
