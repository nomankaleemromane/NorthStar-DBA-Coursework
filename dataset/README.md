# Raw Dataset Directory

This folder contains the original CSV files for the NorthStar DBA coursework case study. These files should be treated as the raw source data before cleaning, standardisation, or transformation.

The raw data includes operational records for customers, orders, deliveries, drivers, vehicles, hubs, incidents, complaints, and mobile app events.

For the coursework, this directory provides the evidence base for data profiling, schema discovery, data quality assessment, and relationship identification before the data is loaded into relational or NoSQL systems.

## Coursework Role

| Requirement | How This Folder Supports It |
| --- | --- |
| Source data review | Provides the original unmodified files used at the start of the assignment. |
| Schema analysis | Shows the fields, keys, and business entities available for database design. |
| Data quality assessment | Contains missing values and inconsistent categories that must be identified and cleaned. |
| Relationship mapping | Provides IDs needed to connect customers, orders, deliveries, drivers, vehicles, hubs, incidents, complaints, and app events. |
| Baseline comparison | Allows comparison against `cleaned_dataset/` to show what was changed during preparation. |

## Files

| File | Records | Columns | Description |
| --- | ---: | --- | --- |
| `app_events.csv` | 640 | 10 | Digital application events such as route searches, order tracking, ETA refreshes, chat events, and payment retries. |
| `complaints.csv` | 320 | 10 | Customer complaint records with channel, severity, status, resolution time, and compensation amount. |
| `customers.csv` | 650 | 9 | Customer profile data including age, zone, customer type, loyalty score, app engagement, and account status. |
| `data_dictionary.csv` | 9 | 3 | File-level metadata containing record counts and short descriptions. |
| `deliveries.csv` | 950 | 13 | Delivery operations data including driver, vehicle, hub, timing, status, distance, route overrides, ratings, and cost. |
| `drivers.csv` | 170 | 8 | Driver workforce data including zone, employment type, experience, training, rating, shift preference, and active status. |
| `hubs.csv` | 8 | 5 | Operational hub reference data with hub names, zones, hub types, and capacity scores. |
| `incidents.csv` | 280 | 7 | Incident records linked to deliveries, including incident type, severity, status, and resolution hours. |
| `orders.csv` | 1,250 | 11 | Order data including service type, creation time, zones, priority, value, booking channel, and special handling flag. |
| `vehicles.csv` | 120 | 8 | Fleet asset data including vehicle type, assigned zone, battery health, odometer, maintenance status, and telematics version. |

## Schema Summary

### `customers.csv`

| Column | Meaning |
| --- | --- |
| `customer_id` | Unique customer identifier. |
| `age` | Customer age. |
| `home_zone` | Customer's home operating zone. |
| `customer_type` | Customer segment: `Consumer`, `Enterprise`, or `SME`. |
| `signup_date` | Date the customer joined. |
| `loyalty_score` | Customer loyalty metric. |
| `app_engagement_score` | Digital engagement metric. |
| `preferred_channel` | Preferred contact or booking channel. |
| `account_status` | Account state: `Active`, `Dormant`, or `Suspended`. |

### `orders.csv`

| Column | Meaning |
| --- | --- |
| `order_id` | Unique order identifier. |
| `customer_id` | Customer who placed the order. |
| `service_type` | Service category: `Business`, `Medical`, `Parcel`, `Passenger`, or `Retail`. |
| `order_created_at` | Timestamp when the order was created. |
| `promised_window_hours` | Promised service window in hours. |
| `pickup_zone` | Pickup operating zone. |
| `dropoff_zone` | Drop-off operating zone. |
| `priority_level` | Order priority: `Critical`, `High`, `Medium`, or `Low`. |
| `order_value` | Monetary value of the order. |
| `booking_channel` | Booking source: `API`, `App`, `Phone`, or `Web`. |
| `special_handling_flag` | Indicates whether special handling is required. |

### `deliveries.csv`

| Column | Meaning |
| --- | --- |
| `delivery_id` | Unique delivery identifier. |
| `order_id` | Order linked to the delivery. |
| `driver_id` | Driver assigned to the delivery. |
| `vehicle_id` | Vehicle assigned to the delivery. |
| `hub_id` | Hub responsible for dispatch or handling. |
| `dispatch_time` | Dispatch timestamp. |
| `delivery_completed_at` | Completion timestamp when available. |
| `delivery_status` | Delivery outcome: `OnTime`, `Delayed`, or `Failed`. |
| `route_distance_km` | Route distance in kilometres. |
| `manual_route_override_count` | Number of manual route changes. |
| `proof_of_completion_missing` | Indicates whether proof of completion is missing. |
| `customer_rating_post_delivery` | Customer rating after delivery. |
| `fuel_or_charge_cost` | Fuel or charging cost for the delivery. |

### Other Tables

| File | Key Columns |
| --- | --- |
| `drivers.csv` | `driver_id`, `base_zone`, `employment_type`, `years_experience`, `training_score`, `driver_rating`, `shift_preference`, `active_flag` |
| `vehicles.csv` | `vehicle_id`, `vehicle_type`, `assigned_zone`, `commission_date`, `battery_health_pct`, `odometer_km`, `maintenance_status`, `telematics_version` |
| `hubs.csv` | `hub_id`, `hub_name`, `zone`, `hub_type`, `capacity_score` |
| `incidents.csv` | `incident_id`, `delivery_id`, `incident_type`, `reported_at`, `severity`, `resolution_status`, `resolved_hours` |
| `complaints.csv` | `complaint_id`, `customer_id`, `order_id`, `complaint_type`, `channel`, `severity`, `created_at`, `status`, `resolution_days`, `compensation_amount` |
| `app_events.csv` | `event_id`, `customer_id`, `order_id`, `event_timestamp`, `event_type`, `session_id`, `device_type`, `zone_context`, `api_latency_ms`, `success_flag` |

## Raw Data Quality Notes

These files intentionally contain data quality issues for coursework analysis:

| File | Missing or inconsistent fields observed |
| --- | --- |
| `app_events.csv` | `order_id` is blank for 144 rows where the event is not linked to an order. |
| `complaints.csv` | `compensation_amount` has missing values. |
| `customers.csv` | `loyalty_score` and `preferred_channel` have missing values. Zone names use inconsistent casing and spelling. |
| `deliveries.csv` | `delivery_completed_at` and `customer_rating_post_delivery` have missing values. |
| `drivers.csv` | `training_score` has missing values. |
| `incidents.csv` | `resolved_hours` is missing for some unresolved or open incidents. |
| `orders.csv` | `booking_channel` has missing values. Pickup and drop-off zones contain inconsistent casing. |
| `vehicles.csv` | `battery_health_pct` has missing values. |

Use `cleaned_dataset/` for analysis that requires standardised values and cleaner missing-value handling.

## Suggested DBA Checks

When using this folder in the assignment, the following checks are useful:

| Check | Example Fields |
| --- | --- |
| Primary key uniqueness | `customer_id`, `order_id`, `delivery_id`, `driver_id`, `vehicle_id`, `hub_id` |
| Foreign key consistency | `orders.customer_id`, `deliveries.order_id`, `deliveries.driver_id`, `deliveries.vehicle_id`, `deliveries.hub_id` |
| Missing-value review | `booking_channel`, `loyalty_score`, `training_score`, `battery_health_pct`, `customer_rating_post_delivery` |
| Categorical standardisation | `home_zone`, `pickup_zone`, `dropoff_zone`, `zone_context`, `assigned_zone` |
| Date/time validity | `signup_date`, `order_created_at`, `dispatch_time`, `delivery_completed_at`, `reported_at`, `created_at`, `event_timestamp` |
