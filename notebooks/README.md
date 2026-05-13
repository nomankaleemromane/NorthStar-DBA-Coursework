# Notebooks Directory

This folder contains the executable analysis work for the NorthStar Urban Mobility and Logistics **Databases and Analytics** coursework.

The notebooks provide the actual workflows for SQL within R, R analytics and visualisation, Python data processing, MongoDB Atlas NoSQL design and querying, and query optimisation.

## Assignment Coverage

| Requirement | Notebook Evidence |
| --- | --- |
| SQL within R | R notebook creates SQLite tables and uses SQL to filter, join, aggregate, and manipulate structured data. |
| R analytics and visualisation | R notebook performs statistical analysis, comparisons, and business-focused interpretation. |
| Python data processing | Python notebook cleans, transforms, integrates, analyses, and visualises NorthStar data. |
| MongoDB Atlas | MongoDB notebook loads cleaned records into collections and demonstrates NoSQL querying. |
| Query optimisation | R and MongoDB notebooks include indexing and optimisation concepts. |
| Business interpretation | Notebooks connect outputs to delays, failures, complaints, costs, hubs, services, and operational performance. |

## Notebook Overview

| Notebook | Main Purpose | Cells |
| --- | --- | ---: |
| `North_Start_DBA_Case_study_Python.ipynb` | Data import, EDA, cleaning, integration, statistical analysis, and visualisation. | 50 |
| `North_Start_DBA_Case_study_R.ipynb` | SQLite database creation, SQL CRUD operations, analytical SQL, R transformations, and query optimisation. | 96 |
| `North_Start_DBA_Case_study_MongoDB.ipynb` | MongoDB Atlas connection, collection loading, CRUD operations, aggregation, and indexing. | 52 |

## Recommended Execution Order

1. `North_Start_DBA_Case_study_Python.ipynb`
2. `North_Start_DBA_Case_study_R.ipynb`
3. `North_Start_DBA_Case_study_MongoDB.ipynb`

The Python notebook is the best starting point because it documents the raw data import, exploratory data analysis, cleaning, integration, and summary workflow. The R notebook also starts from the raw CSV files and performs relational work in SQLite. The MongoDB notebook starts from the cleaned CSV files.

## Actual Data Sources Used

| Notebook | Data Folder Used in Code | Loading Pattern |
| --- | --- | --- |
| `North_Start_DBA_Case_study_Python.ipynb` | `dataset/` | Clones the GitHub repository, then reads all raw CSV files with `pd.read_csv("NorthStar-DBA-Coursework/dataset/<file>.csv")`. |
| `North_Start_DBA_Case_study_R.ipynb` | `dataset/` | Clones the GitHub repository, then reads all raw CSV files with `read.csv("NorthStar-DBA-Coursework/dataset/<file>.csv")`. |
| `North_Start_DBA_Case_study_MongoDB.ipynb` | `cleaned_dataset/` | Clones the GitHub repository, then reads all cleaned CSV files with `pd.read_csv("NorthStar-DBA-Coursework/cleaned_dataset/<file>_cleaned.csv")`. |

## Python Notebook

File: `North_Start_DBA_Case_study_Python.ipynb`

| Section | Coursework Purpose |
| --- | --- |
| Setup and data import | Loads the NorthStar CSV files. |
| Exploratory data analysis | Reviews structure, unique values, missing values, numeric distributions, and summary statistics. |
| Data cleaning and integration | Standardises zones, handles missing values, merges datasets, verifies integrity, and creates derived columns. |
| Statistical analysis | Uses Pandas and NumPy to analyse delivery cost, failure rates, and correlations. |
| Visualisation | Produces charts that support the analytical argument. |
| Summary | Presents the main findings from the Python workflow. |
| Cleaned CSV export | Writes `*_cleaned.csv` files during runtime after cleaning. |

## R and SQL Notebook

File: `North_Start_DBA_Case_study_R.ipynb`

| Section | Coursework Purpose |
| --- | --- |
| Data import | Loads the coursework CSV files. |
| SQLite database creation | Creates database tables from the case study data. |
| SQL CRUD operations | Demonstrates `SELECT`, `INSERT`, `UPDATE`, and `DELETE`. |
| SQL analysis | Uses filtering, joins, grouping, and aggregation to investigate operational questions. |
| R analytics | Performs statistical analysis and comparisons across drivers, zones, costs, and services. |
| Visualisation | Supports interpretation through graphs and summaries. |
| Query optimisation | Demonstrates indexing or optimisation ideas and explains why they matter. |
| SQLite table overwrite | Writes cleaned in-memory data frames back into SQLite tables after cleaning steps. |

## MongoDB Notebook

File: `North_Start_DBA_Case_study_MongoDB.ipynb`

| Section | Coursework Purpose |
| --- | --- |
| Library setup | Installs and imports `pymongo` and supporting libraries. |
| Cleaned data loading | Loads prepared CSV data for MongoDB insertion. |
| MongoDB Atlas connection | Connects to a MongoDB Atlas database. |
| Collection insertion | Creates collections for NorthStar operational data. |
| CRUD operations | Demonstrates document retrieval, insertion, update, and deletion. |
| Aggregation | Runs analytical queries over collections. |
| Indexing | Shows query optimisation through MongoDB indexes. |

## MongoDB Collections Built from Cleaned Data

| Collection | Built From |
| --- | --- |
| `customers` | `customers_cleaned.csv`, with matching orders, complaints, and app events embedded. |
| `drivers` | `drivers_cleaned.csv`, with matching deliveries and incidents embedded. |
| `vehicles` | `vehicles_cleaned.csv`, with related incidents embedded. |
| `deliveries` | `deliveries_cleaned.csv`, with route, cost, proof-of-completion, and exception fields. |
| `app_events` | `app_events_cleaned.csv` inserted as event documents. |

## Data Used

| Folder | Usage |
| --- | --- |
| `../dataset/` | Raw source data loaded by the Python and R notebooks. |
| `../cleaned_dataset/` | Prepared CSV files loaded by the MongoDB notebook. |

## Notes for Running

- Open the notebooks in Jupyter Notebook, JupyterLab, VS Code, Google Colab, or another compatible notebook environment.
- Run cells from top to bottom because later cells depend on variables and data loaded earlier.
- The MongoDB notebook requires valid MongoDB Atlas credentials before database operations can run successfully.
- If a notebook reads from GitHub URLs, confirm that the repository path and branch are still correct.
