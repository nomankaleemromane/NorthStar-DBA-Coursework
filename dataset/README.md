# Raw Dataset Directory

This folder contains the original CSV files for the NorthStar Urban Mobility and Logistics case study in the **Databases and Analytics** module.

These files are the starting point for understanding the organisation's fragmented operational data. They support data overview, data quality assessment, relationship discovery, and comparison against the cleaned data.

## Role in the Coursework

| Coursework Need | How This Folder Supports It |
| --- | --- |
| Data overview | Provides the original files used to describe the case study data. |
| Problem identification | Contains delays, failures, complaints, incidents, route data, hub data, and app events needed to investigate NorthStar's challenges. |
| Data quality analysis | Includes missing values and inconsistent categories that are handled during preparation. |
| Integration planning | Provides keys for linking customers, orders, deliveries, drivers, vehicles, hubs, complaints, incidents, and app events. |
| Baseline for cleaning | Allows clear comparison with the prepared files in `cleaned_dataset/`. |

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

## Data Quality Issues to Discuss

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

## Suggested Analysis Checks

| Check | Example Columns |
| --- | --- |
| Unique identifiers | `customer_id`, `order_id`, `delivery_id`, `driver_id`, `vehicle_id`, `hub_id` |
| Join consistency | `orders.customer_id`, `deliveries.order_id`, `deliveries.driver_id`, `deliveries.vehicle_id`, `deliveries.hub_id` |
| Missing values | `booking_channel`, `loyalty_score`, `training_score`, `battery_health_pct`, `customer_rating_post_delivery` |
| Category consistency | `home_zone`, `pickup_zone`, `dropoff_zone`, `zone_context`, `assigned_zone` |
| Time fields | `signup_date`, `order_created_at`, `dispatch_time`, `delivery_completed_at`, `reported_at`, `created_at`, `event_timestamp` |

Use `cleaned_dataset/` for the prepared version of this data after cleaning and standardisation.
