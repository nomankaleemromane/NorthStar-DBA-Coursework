# NorthStar DBA Coursework

This repository contains the NorthStar DBA coursework case study dataset and analysis notebooks. The project models a mobility and logistics operation with customers, orders, deliveries, drivers, vehicles, hubs, incidents, complaints, and digital app events.

The purpose of the repository is to demonstrate practical database administration and data management skills: understanding raw operational data, identifying data quality issues, preparing cleaned datasets, creating relational structures, running SQL operations, modelling selected data for MongoDB, and using indexes or query design to improve access patterns.

The repository is organised to support the full data workflow:

1. Review the original CSV datasets.
2. Clean and standardise the data.
3. Analyse the cleaned data using Python, R/SQL, and MongoDB.
4. Demonstrate relational and document database operations for a DBA coursework scenario.

## Repository Structure

| Path | Purpose |
| --- | --- |
| `dataset/` | Original raw CSV files used as the starting point for analysis. |
| `cleaned_dataset/` | Cleaned CSV files after standardisation and missing-value handling. |
| `notebooks/` | Jupyter notebooks for Python data processing, R/SQL analysis, and MongoDB operations. |
| `README.md` files | Documentation for the project and each major folder. |

## Coursework Scope

This repository supports the main areas expected in a DBA coursework assignment:

| Coursework Area | Repository Evidence |
| --- | --- |
| Data understanding | Raw datasets, data dictionary, schema summaries, and relationship mapping. |
| Data quality review | Missing-value checks, inconsistent category values, and raw-to-cleaned comparison. |
| Data preparation | Cleaned CSV files with standardised zones and handled missing values. |
| Relational database work | R notebook using SQLite tables, joins, CRUD operations, aggregation, and optimisation. |
| NoSQL database work | MongoDB notebook using collections, document insertion, CRUD, aggregation, and indexing. |
| Analytical reporting | Python and R analysis covering delivery performance, complaints, incidents, costs, ratings, and zone-level patterns. |

## Dataset Overview

The case study contains nine business datasets plus a data dictionary.

| Dataset | Records | Main Entity | Description |
| --- | ---: | --- | --- |
| `customers.csv` | 650 | Customer | Customer profile, zone, loyalty, engagement, preferred channel, and account status. |
| `orders.csv` | 1,250 | Order | Service orders with customer, zones, priority, booking channel, value, and special handling. |
| `deliveries.csv` | 950 | Delivery | Dispatch and delivery outcomes linked to orders, drivers, vehicles, and hubs. |
| `drivers.csv` | 170 | Driver | Driver workforce details, training score, rating, shift preference, and active status. |
| `vehicles.csv` | 120 | Vehicle | Fleet details, battery health, odometer, maintenance status, and telematics version. |
| `hubs.csv` | 8 | Hub | Operational hubs, zones, hub types, and capacity scores. |
| `incidents.csv` | 280 | Incident | Operational incident records linked to deliveries. |
| `complaints.csv` | 320 | Complaint | Customer complaints linked to customers and orders, including severity and compensation. |
| `app_events.csv` | 640 | Digital Event | App and platform activity suitable for document-style MongoDB analysis. |
| `data_dictionary.csv` | 9 | Metadata | File-level record counts and dataset descriptions. |

## Data Model

The datasets are designed around a transport and delivery operation:

| Relationship | Join Key |
| --- | --- |
| Customers to orders | `customers.customer_id = orders.customer_id` |
| Orders to deliveries | `orders.order_id = deliveries.order_id` |
| Drivers to deliveries | `drivers.driver_id = deliveries.driver_id` |
| Vehicles to deliveries | `vehicles.vehicle_id = deliveries.vehicle_id` |
| Hubs to deliveries | `hubs.hub_id = deliveries.hub_id` |
| Deliveries to incidents | `deliveries.delivery_id = incidents.delivery_id` |
| Customers/orders to complaints | `customer_id` and `order_id` |
| Customers/orders to app events | `customer_id` and optional `order_id` |

Some app events are not tied to a specific order, so `app_events.order_id` can be blank. This is expected for events such as route searches, chat interactions, or app usage before an order is created.

## DBA Relevance

The case study is useful for database administration because it contains both transactional and analytical requirements:

| DBA Task | How It Appears in the Project |
| --- | --- |
| Schema design | The CSV files can be converted into relational tables with primary and foreign key relationships. |
| Data integrity | Joins between customers, orders, deliveries, drivers, vehicles, hubs, complaints, and incidents can be validated. |
| Data cleaning | Missing values and inconsistent categories must be handled before reliable reporting. |
| Query design | SQL queries are used for CRUD operations, aggregation, and business analysis. |
| Query optimisation | Indexing is demonstrated in both SQL and MongoDB contexts. |
| Document modelling | App events and operational records can be represented as MongoDB collections for NoSQL analysis. |

## Analysis Workflow

The notebooks show three complementary approaches:

| Notebook | Focus |
| --- | --- |
| `North_Start_DBA_Case_study_Python.ipynb` | Data import, EDA, cleaning, integration, statistical analysis, and visualisation. |
| `North_Start_DBA_Case_study_R.ipynb` | SQLite database creation, SQL CRUD operations, data cleaning in R, aggregate queries, analytical SQL, and query optimisation. |
| `North_Start_DBA_Case_study_MongoDB.ipynb` | Loading cleaned data, connecting to MongoDB Atlas, inserting collections, CRUD operations, aggregation, and indexing. |

## Recommended Usage

Use the repository in this order:

1. Read `dataset/README.md` to understand the original raw data.
2. Review `cleaned_dataset/README.md` to understand what changed during cleaning.
3. Run or inspect `notebooks/North_Start_DBA_Case_study_Python.ipynb` first because it explains the data preparation and EDA.
4. Use the R notebook for relational database and SQL analysis.
5. Use the MongoDB notebook for document database modelling, CRUD, aggregation, and indexing.

## Notes

- The cleaned files preserve the same record counts as the raw files.
- Zone values in the raw data include inconsistent spellings and casing, such as `AIRPORT`, `CENTRAL`, `Ctr`, and `SOUTH`; these are standardised during cleaning.
- The project is suitable for DBA coursework topics including data quality, schema understanding, relational joins, CRUD operations, aggregation, indexing, and multi-database analysis.
