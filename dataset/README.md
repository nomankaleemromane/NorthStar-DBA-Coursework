# Cleaned Dataset Directory

This folder contains cleaned versions of the NorthStar DBA coursework CSV files. The cleaned files keep the same business entities and record counts as the raw files, but values have been standardised and most missing fields have been handled.

Use these files for modelling, SQL analysis, MongoDB import, reporting, and visualisation.

For the coursework assignment, this directory represents the prepared dataset after data quality work has been completed. It should be used when demonstrating database loading, joins, CRUD operations, aggregation, indexing, and final analysis.

## Coursework Role

| Requirement | How This Folder Supports It |
| --- | --- |
| Clean data submission | Provides standardised files ready for analysis and database loading. |
| Data preparation evidence | Shows that raw data issues were reviewed and corrected where appropriate. |
| Relational database design | Supplies clean tables for SQLite creation, joins, CRUD, and aggregate SQL. |
| MongoDB modelling | Supplies prepared records for collection insertion and document queries. |
| Analytical reporting | Provides reliable inputs for delivery, customer, driver, vehicle, incident, complaint, and app-event analysis. |

## Files

| Raw File | Cleaned File | Records | Purpose |
| --- | --- | ---: | --- |
| `dataset/app_events.csv` | `app_events_cleaned.csv` | 640 | Cleaned digital event data for app behaviour and MongoDB-style analysis. |
| `dataset/complaints.csv` | `complaints_cleaned.csv` | 320 | Cleaned customer complaint and compensation records. |
| `dataset/customers.csv` | `customers_cleaned.csv` | 650 | Cleaned customer master data. |
| `dataset/data_dictionary.csv` | `data_dictionary_cleaned.csv` | 9 | Cleaned metadata file. |
| `dataset/deliveries.csv` | `deliveries_cleaned.csv` | 950 | Cleaned delivery outcome and cost records. |
| `dataset/drivers.csv` | `drivers_cleaned.csv` | 170 | Cleaned driver workforce data. |
| `dataset/hubs.csv` | `hubs_cleaned.csv` | 8 | Cleaned hub reference data. |
| `dataset/incidents.csv` | `incidents_cleaned.csv` | 280 | Cleaned incident management data. |
| `dataset/orders.csv` | `orders_cleaned.csv` | 1,250 | Cleaned order records. |
| `dataset/vehicles.csv` | `vehicles_cleaned.csv` | 120 | Cleaned fleet asset records. |

## Cleaning Summary

The cleaning process focuses on making the data more reliable for analysis while preserving the original row counts.

| Cleaning Area | What Was Addressed |
| --- | --- |
| Zone standardisation | Inconsistent zone values such as `AIRPORT`, `CENTRAL`, `Ctr`, and `SOUTH` were standardised for easier grouping and joining. |
| Missing categorical values | Missing fields such as booking channel and preferred channel were handled. |
| Missing numeric values | Fields such as loyalty score, training score, battery health, customer rating, and compensation amount were cleaned or imputed where appropriate. |
| Date and timestamp readiness | Date/time fields are prepared for analysis in Python, R, SQL, and MongoDB workflows. |
| Record preservation | No source table loses records during cleaning; raw and cleaned record counts match. |

## Remaining Blank Values

Some blank values remain because they represent valid business situations rather than simple data errors.

| Cleaned File | Remaining Blank Field | Count | Reason |
| --- | --- | ---: | --- |
| `app_events_cleaned.csv` | `order_id` | 144 | Some app events occur before or outside a specific order. |
| `deliveries_cleaned.csv` | `delivery_completed_at` | 19 | Failed or incomplete deliveries may not have a completion timestamp. |
| `incidents_cleaned.csv` | `resolved_hours` | 17 | Open, escalated, or unresolved incidents may not have resolution duration yet. |

## Recommended Use

Use this folder when:

- building the SQLite database in the R notebook;
- loading collections into MongoDB;
- running EDA and visualisation after cleaning;
- joining operational tables across customers, orders, deliveries, drivers, vehicles, hubs, complaints, incidents, and app events;
- preparing DBA coursework outputs where clean and consistent data is required.

## Assignment Evidence

The cleaned files help demonstrate these DBA skills:

| Skill | Evidence in This Folder |
| --- | --- |
| Data quality management | Missing values are reduced and inconsistent categorical values are standardised. |
| Data integrity preparation | Identifier columns remain available for joins and relationship validation. |
| Auditability | Cleaned filenames preserve the original table names with a `_cleaned` suffix. |
| Reproducibility | Row counts match the raw files, making it clear that cleaning did not remove records. |
| Database readiness | Tables are suitable for importing into SQLite and MongoDB workflows. |

## Key Relationships

| From | To | Key |
| --- | --- | --- |
| `customers_cleaned.csv` | `orders_cleaned.csv` | `customer_id` |
| `orders_cleaned.csv` | `deliveries_cleaned.csv` | `order_id` |
| `drivers_cleaned.csv` | `deliveries_cleaned.csv` | `driver_id` |
| `vehicles_cleaned.csv` | `deliveries_cleaned.csv` | `vehicle_id` |
| `hubs_cleaned.csv` | `deliveries_cleaned.csv` | `hub_id` |
| `deliveries_cleaned.csv` | `incidents_cleaned.csv` | `delivery_id` |
| `customers_cleaned.csv` and `orders_cleaned.csv` | `complaints_cleaned.csv` | `customer_id`, `order_id` |
| `customers_cleaned.csv` and `orders_cleaned.csv` | `app_events_cleaned.csv` | `customer_id`, optional `order_id` |

## File Naming Convention

Each cleaned file follows the pattern:

```text
<original_table_name>_cleaned.csv
```

For example, `orders.csv` becomes `orders_cleaned.csv`.
