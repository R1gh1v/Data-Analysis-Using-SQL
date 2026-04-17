# World Layoffs Data Cleaning Project

## Project Overview
This project demonstrates a thorough data cleaning process using MySQL. The primary objective was to take a raw dataset of global company layoffs and transform it into a structured, clean format ready for analysis. 

[cite_start]The cleaning process involved several stages, including deduplication, data standardization, and handling missing information[cite: 1, 12].

## Dataset
The project utilizes a `layoffs.csv` file containing detailed records of company layoffs, including:
* **Company**: Name of the organization.
* **Location**: City/Headquarters.
* **Industry**: Sector of the company (e.g., Crypto, Aerospace, Finance).
* **Total Laid Off**: Number of employees affected.
* **Percentage Laid Off**: The fraction of the company's workforce let go.
* **Date**: When the layoffs occurred.
* **Stage**: Funding stage (e.g., Series B, Post-IPO).
* **Country**: National location of the company.
* [cite_start]**Funds Raised**: Total capital raised in millions[cite: 13].

## SQL Techniques Applied
The following data cleaning steps were implemented in the `data cleaning project.sql` script:

### 1. Staging the Data
[cite_start]Created a `layoffs_staging` table to keep the raw data intact while performing transformations on a working copy[cite: 12].

### 2. Removing Duplicates
* Utilized `ROW_NUMBER()` partitioned by all columns to identify identical rows.
* [cite_start]Created a secondary staging table (`layoffs_staging2`) with an added `row_num` column to safely delete duplicate entries[cite: 12].

### 3. Data Standardization
* [cite_start]**Trimming**: Removed unnecessary white space from company names[cite: 12].
* [cite_start]**Industry Alignment**: Standardized inconsistent labels (e.g., updating all variations of 'Crypto' to a single standard)[cite: 12].
* [cite_start]**Country Cleanup**: Fixed trailing punctuation in country names (e.g., 'United States.')[cite: 12].
* [cite_start]**Date Formatting**: Converted the `date` column from text to a proper `DATE` format using `STR_TO_DATE()` for time-series compatibility[cite: 12].

### 4. Handling Null and Blank Values
* [cite_start]Populated missing `industry` values by joining the table with itself where records for the same company had industry data available elsewhere[cite: 12].
* [cite_start]Removed records where both `total_laid_off` and `percentage_laid_off` were null, as they provided no actionable data for analysis[cite: 12].

### 5. Schema Optimization
* [cite_start]Dropped unnecessary columns used during the cleaning process (like `row_num`) to finalize the table for the analysis phase[cite: 12].

## How to Use
1. **Import the Data**: Load the provided `layoffs.csv` into your MySQL environment.
2. **Run the Script**: Execute the `data cleaning project.sql` script step-by-step to see the transformation from raw data to a cleaned dataset.

## Tools Used
* **MySQL**: Primary tool for data transformation and cleaning.
* **SQL Concepts**: Joins, CTEs, Window Functions, DDL, and DML.
