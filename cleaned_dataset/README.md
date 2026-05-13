# Cleaned Dataset Directory

This folder contains the prepared CSV files for the NorthStar Urban Mobility and Logistics **Databases and Analytics** coursework.

The cleaned files keep the same business entities and record counts as the raw files, but values have been standardised and most missing fields have been handled.

## How the Notebooks Use This Folder

| Notebook | Actual Use of `cleaned_dataset/` |
| --- | --- |
| `North_Start_DBA_Case_study_MongoDB.ipynb` | Reads all 10 cleaned CSV files from `NorthStar-DBA-Coursework/cleaned_dataset/` using `pd.read_csv()`. These data frames are converted into MongoDB documents and inserted into MongoDB Atlas collections. |
| `North_Start_DBA_Case_study_Python.ipynb` | Does not read this folder directly in the current notebook code. It reads from `dataset/`, performs cleaning, and exports cleaned CSV files during notebook execution. |
| `North_Start_DBA_Case_study_R.ipynb` | Does not read this folder directly in the current notebook code. It reads from `dataset/`, creates SQLite tables, then performs cleaning and table overwrites inside the notebook. |

## Files

| Raw File | Cleaned File | Records | Purpose |
| --- | --- | ---: | --- |
| `dataset/app_events.csv` | `app_events_cleaned.csv` | 640 | Prepared platform event data for app interaction and NoSQL analysis. |
| `dataset/complaints.csv` | `complaints_cleaned.csv` | 320 | Prepared complaint data for severity, resolution, and compensation analysis. |
| `dataset/customers.csv` | `customers_cleaned.csv` | 650 | Prepared customer master data. |
| `dataset/data_dictionary.csv` | `data_dictionary_cleaned.csv` | 9 | Prepared file-level metadata. |
| `dataset/deliveries.csv` | `deliveries_cleaned.csv` | 950 | Prepared delivery outcome, route, rating, and cost data. |
| `dataset/drivers.csv` | `drivers_cleaned.csv` | 170 | Prepared driver workforce data. |
| `dataset/hubs.csv` | `hubs_cleaned.csv` | 8 | Prepared hub reference data. |
| `dataset/incidents.csv` | `incidents_cleaned.csv` | 280 | Prepared incident and exception data. |
| `dataset/orders.csv` | `orders_cleaned.csv` | 1,250 | Prepared order data. |
| `dataset/vehicles.csv` | `vehicles_cleaned.csv` | 120 | Prepared vehicle and fleet data. |

## Cleaning Summary

| Cleaning Area | What Was Addressed |
| --- | --- |
| Zone standardisation | Inconsistent zone values such as `AIRPORT`, `CENTRAL`, `Ctr`, and `SOUTH` were standardised for grouping and joins. |
| Missing categorical values | Missing fields such as booking channel and preferred channel were handled. |
| Missing numeric values | Fields such as loyalty score, training score, battery health, customer rating, and compensation amount were cleaned or imputed where appropriate. |
| Date and timestamp readiness | Date/time fields were prepared for Python, R, SQL, and MongoDB workflows. |
| Record preservation | No source table loses records during cleaning; raw and cleaned record counts match. |

## Remaining Valid Blanks

Some blanks remain because they represent real business conditions rather than simple data errors.

| Cleaned File | Remaining Blank Field | Count | Interpretation |
| --- | --- | ---: | --- |
| `app_events_cleaned.csv` | `order_id` | 144 | Some app events occur before or outside a specific order. |
| `deliveries_cleaned.csv` | `delivery_completed_at` | 19 | Failed or incomplete deliveries may not have a completion timestamp. |
| `incidents_cleaned.csv` | `resolved_hours` | 17 | Open or unresolved incidents may not have a resolution duration yet. |

## MongoDB Document Inputs

The MongoDB notebook uses these cleaned files to build collections:

| Cleaned Source File | MongoDB Use in the Notebook |
| --- | --- |
| `customers_cleaned.csv` | Builds `customers` documents with customer profile fields plus embedded matching orders, complaints, and app events. |
| `drivers_cleaned.csv` | Builds `drivers` documents with driver profile fields plus matching deliveries and related incidents. |
| `vehicles_cleaned.csv` | Builds `vehicles` documents with fleet fields plus related incidents from deliveries. |
| `deliveries_cleaned.csv` | Builds `deliveries` documents with route, cost, proof-of-completion, status, and embedded delivery incidents. |
| `app_events_cleaned.csv` | Inserts app event records into the `app_events` collection. |
| `orders_cleaned.csv` | Embedded inside matching customer documents. |
| `complaints_cleaned.csv` | Embedded inside matching customer documents. |
| `incidents_cleaned.csv` | Embedded into related driver, vehicle, and delivery documents. |
| `hubs_cleaned.csv` | Loaded into a data frame for reference with delivery and hub identifiers. |
| `data_dictionary_cleaned.csv` | Loaded as metadata for the cleaned dataset. |

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
