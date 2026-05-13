# Raw Dataset Directory

This folder contains the original CSV files for the NorthStar Urban Mobility and Logistics case study in the **Databases and Analytics** module.

These files are the starting point for the Python and R notebooks. Both notebooks clone the repository from GitHub and read the CSV files from this folder.

## How the Notebooks Use This Folder

| Notebook | Actual Use of `dataset/` |
| --- | --- |
| `North_Start_DBA_Case_study_Python.ipynb` | Reads all 10 CSV files from `NorthStar-DBA-Coursework/dataset/` using `pd.read_csv()`. The notebook performs EDA, standardises zones, fills selected missing values, merges tables, creates derived fields, and exports cleaned CSV files during runtime. |
| `North_Start_DBA_Case_study_R.ipynb` | Reads all 10 CSV files from `NorthStar-DBA-Coursework/dataset/` using `read.csv()`. The notebook writes these data frames into an in-memory SQLite database, runs SQL operations, performs cleaning in R/SQL, and overwrites the SQLite tables with cleaned versions. |
| `North_Start_DBA_Case_study_MongoDB.ipynb` | Does not load this folder directly. It loads prepared files from `cleaned_dataset/`. |

## Files

| File | Records | Columns | Description |
| --- | ---: | ---: | --- |
| `app_events.csv` | 640 | 10 | Customer platform events such as route searches, tracking, ETA refreshes, chat events, and payment retries. |
| `complaints.csv` | 320 | 10 | Complaint records with customer, order, type, channel, severity, status, resolution days, and compensation. |
| `customers.csv` | 650 | 9 | Customer profile data including age, zone, segment, loyalty, app engagement, preferred channel, and account status. |
| `data_dictionary.csv` | 9 | 3 | File-level metadata with record counts and short descriptions. |
| `deliveries.csv` | 950 | 13 | Dispatch and delivery data including status, route distance, proof issues, rating, and fuel or charge cost. |
| `drivers.csv` | 170 | 8 | Driver workforce data including zone, employment type, experience, training, rating, shift, and active status. |
| `hubs.csv` | 8 | 5 | Hub reference data for dispatch, warehouse, charging, and control locations. |
| `incidents.csv` | 280 | 7 | Exception and incident records linked to deliveries. |
| `orders.csv` | 1,250 | 11 | Service orders across passenger, parcel, retail, medical, and business operations. |
| `vehicles.csv` | 120 | 8 | Fleet data including vehicle type, zone, battery health, odometer, maintenance status, and telematics version. |

## Key Relationships

| Relationship | Key |
| --- | --- |
| Customers to orders | `customer_id` |
| Orders to deliveries | `order_id` |
| Drivers to deliveries | `driver_id` |
| Vehicles to deliveries | `vehicle_id` |
| Hubs to deliveries | `hub_id` |
| Deliveries to incidents | `delivery_id` |
| Customers/orders to complaints | `customer_id`, `order_id` |
| Customers/orders to app events | `customer_id`, optional `order_id` |

## Data Quality Issues Used in Notebook Cleaning

| File | Issue Observed |
| --- | --- |
| `app_events.csv` | `order_id` is blank for 144 rows because some platform events are not linked to a specific order. |
| `complaints.csv` | `compensation_amount` has missing values. |
| `customers.csv` | `loyalty_score` and `preferred_channel` have missing values; zone values use inconsistent spellings and casing. |
| `deliveries.csv` | `delivery_completed_at` and `customer_rating_post_delivery` have missing values. |
| `drivers.csv` | `training_score` has missing values. |
| `incidents.csv` | `resolved_hours` is missing for some unresolved or open incidents. |
| `orders.csv` | `booking_channel` has missing values; pickup and drop-off zones contain inconsistent casing. |
| `vehicles.csv` | `battery_health_pct` has missing values. |

## Notebook Cleaning and Validation Steps

| Step in Notebook Workflow | Columns or Tables Involved |
| --- | --- |
| Zone standardisation in Python | `customers.home_zone`, `orders.pickup_zone`, `orders.dropoff_zone`, `drivers.base_zone`, `vehicles.assigned_zone`, `app_events.zone_context` |
| Missing-value handling in Python | `customers.loyalty_score`, `customers.preferred_channel`, `orders.booking_channel`, `deliveries.customer_rating_post_delivery`, `drivers.training_score`, `vehicles.battery_health_pct`, `complaints.compensation_amount` |
| Consolidated Python merge | `orders`, `deliveries`, `customers`, `complaints`, `drivers`, `vehicles`, `hubs` |
| Duplicate prevention during Python merge | `complaints` is deduplicated by `order_id` before joining so each order remains one row in the consolidated dataframe. |
| Integrity verification in Python | Row count is checked against 1,250 original orders; duplicate `order_id` values and delivery/complaint/driver/vehicle/hub coverage are reviewed. |
| SQLite loading in R | All 10 raw CSV files are written into SQLite tables using `dbWriteTable()`. |
| Empty-string cleanup in R | Blank values are converted to `NULL` in the SQLite workflow. |
| Datetime conversion in R | `signup_date`, `order_created_at`, `dispatch_time`, `delivery_completed_at`, `created_at`, `reported_at`, `event_timestamp` |

The prepared versions used by the MongoDB notebook are stored in `cleaned_dataset/`.
