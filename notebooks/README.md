# Notebooks Directory

This folder contains the analysis notebooks for the NorthStar DBA coursework case study. The notebooks demonstrate the same case study from three database and analytics perspectives: Python data processing, relational SQL in R, and MongoDB document database operations.

For the assignment, these notebooks are the executable evidence of the methodology. They show how the data was inspected, cleaned, loaded into database systems, queried, analysed, and optimised.

## Coursework Role

| Requirement | Notebook Evidence |
| --- | --- |
| Data profiling and cleaning | Python notebook performs EDA, missing-value review, standardisation, integration, and derived columns. |
| Relational database implementation | R notebook creates SQLite tables and demonstrates SQL operations. |
| SQL CRUD and analytics | R notebook includes `SELECT`, `INSERT`, `UPDATE`, `DELETE`, aggregate queries, and business interpretation. |
| NoSQL implementation | MongoDB notebook loads cleaned data into MongoDB collections. |
| Query optimisation | R and MongoDB notebooks include optimisation/indexing concepts. |
| Reporting and insight | Python and R notebooks produce statistical summaries and operational analysis. |

## Notebook Overview

| Notebook | Main Purpose | Cells |
| --- | --- | ---: |
| `North_Start_DBA_Case_study_Python.ipynb` | Data import, EDA, cleaning, integration, statistical analysis, and visualisation. | 50 |
| `North_Start_DBA_Case_study_R.ipynb` | SQLite database creation, SQL CRUD operations, SQL analytics, R transformations, and query optimisation. | 96 |
| `North_Start_DBA_Case_study_MongoDB.ipynb` | MongoDB Atlas connection, collection loading, CRUD operations, aggregation, and indexing. | 52 |

## Recommended Execution Order

1. `North_Start_DBA_Case_study_Python.ipynb`
2. `North_Start_DBA_Case_study_R.ipynb`
3. `North_Start_DBA_Case_study_MongoDB.ipynb`

The Python notebook is the best starting point because it documents the raw data import, exploratory data analysis, cleaning, integration, and summary workflow. The R and MongoDB notebooks then use the cleaned data for database-oriented coursework tasks.

## Python Notebook

File: `North_Start_DBA_Case_study_Python.ipynb`

This notebook focuses on data understanding and preparation.

| Section | Description |
| --- | --- |
| Setup and data import | Loads the NorthStar CSV files for analysis. |
| Exploratory data analysis | Reviews table structure, unique categorical values, missing values, numeric distributions, and summary statistics. |
| Data cleaning and integration | Standardises zone names, handles missing values, merges datasets, verifies data integrity, and creates derived columns. |
| Statistical analysis | Uses Pandas and NumPy for delivery cost summaries, delivery failure rates by zone, and correlation analysis. |
| Visualisation | Produces charts such as correlation heatmaps, pair plots, delivery outcome distributions, and complaint type distributions. |
| Summary | Documents key analytical takeaways from the Python workflow. |

## R and SQL Notebook

File: `North_Start_DBA_Case_study_R.ipynb`

This notebook focuses on relational database operations and analytical SQL.

| Section | Description |
| --- | --- |
| Data import | Loads the coursework CSV files from the repository. |
| SQLite database creation | Creates a relational SQLite database and writes the CSV files as database tables. |
| CRUD operations | Demonstrates `SELECT`, `INSERT`, `UPDATE`, and `DELETE` operations. |
| Data cleaning in R | Standardises zone names, counts missing values, and converts date columns. |
| Aggregate analysis | Summarises order value, driver ratings, complaint severity, and fleet information. |
| Analytical queries | Performs business-focused SQL analysis using the connected tables. |
| R transformations | Applies statistical analysis to driver performance, zone variation, and delivery cost distribution. |
| Query optimisation | Demonstrates indexing or optimisation concepts for DBA coursework. |

## MongoDB Notebook

File: `North_Start_DBA_Case_study_MongoDB.ipynb`

This notebook focuses on document database loading and querying.

| Section | Description |
| --- | --- |
| Library setup | Installs and imports `pymongo` and supporting libraries. |
| Cleaned data loading | Loads cleaned CSV data for MongoDB insertion. |
| MongoDB Atlas connection | Connects to a MongoDB Atlas database. |
| Collection insertion | Inserts customers, drivers, vehicles, deliveries, and other case study data into MongoDB collections. |
| CRUD operations | Demonstrates document retrieval, insertion, update, and deletion. |
| Aggregation | Runs more complex queries for analytical insight. |
| Indexing | Shows query optimisation through MongoDB indexes. |

## Data Used

The notebooks use files from:

| Folder | Usage |
| --- | --- |
| `../dataset/` | Raw source data for initial exploration and cleaning. |
| `../cleaned_dataset/` | Cleaned data for SQL, MongoDB, and final analysis workflows. |

## Notes for Running

- Open the notebooks in Jupyter Notebook, JupyterLab, VS Code, or another compatible notebook environment.
- Run cells from top to bottom because later cells depend on imported data and variables created earlier.
- The MongoDB notebook requires valid MongoDB Atlas connection credentials before database operations can run successfully.
- If a notebook reads from GitHub URLs, confirm that the repository path and branch are still correct.

## Submission Notes

- Use the Python notebook to explain the data cleaning and preparation stage.
- Use the R notebook to evidence relational database design, SQL operations, joins, aggregations, and optimisation.
- Use the MongoDB notebook to evidence document database loading, CRUD operations, aggregation pipelines, and indexing.
- Reference `../dataset/README.md` and `../cleaned_dataset/README.md` when explaining why raw and cleaned data folders are both included.
