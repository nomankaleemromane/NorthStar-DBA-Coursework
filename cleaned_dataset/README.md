# Cleaned Dataset Directory

This folder contains the prepared CSV files for the NorthStar Urban Mobility and Logistics **Databases and Analytics** coursework.

The cleaned files keep the same business entities and record counts as the raw files, but values have been standardised and most missing fields have been handled. These files are intended for SQL analysis, R analytics, Python reporting, and MongoDB Atlas loading.

## Role in the Coursework

| Coursework Need | How This Folder Supports It |
| --- | --- |
| Data preparation evidence | Shows the output of cleaning and standardisation work. |
| SQL within R | Provides clean tables for SQLite loading, joins, CRUD operations, aggregation, and optimisation. |
| R analytics | Provides consistent inputs for statistical summaries, comparisons, and visualisation. |
| Python analytics | Provides prepared data for deeper analysis of delays, failures, costs, ratings, and complaints. |
| MongoDB Atlas | Provides clean records for collection insertion, document queries, aggregation, and indexing. |
| Reproducibility | Keeps cleaned data separate from the raw source files. |

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

## Analysis Use

Use this folder when:

- loading data into SQLite for SQL within R;
- producing R analytics and visualisations;
- running Python analysis on prepared data;
- loading MongoDB Atlas collections;
- analysing delays, failures, complaints, incident patterns, service performance, route costs, and hub-level variation;
- preparing final coursework outputs and business interpretation.

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
