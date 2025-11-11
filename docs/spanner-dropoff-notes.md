# Spanner Drop-Off Source of Truth

## Project Overview

Spannr Drop-Off is a prototype of system for independent garages to manage day-based bookings, website content, and daily schedules. It includes an admin portal (for configuration, website editing, and diary management) and a public website with a customer booking flow.

## Entities and Data Model

1. **booking_settings** — Defines how bookings work and when the business is open.

   - Fields:  

     `id`, `opening_days`, `advance_booking_notice_hours`, `daily_booking_limit`, `notification_name`, `notification_email`.

   - **opening_days** structure:** one entry per day of the week, each with:  

     `day_of_week` (e.g. "monday"), `is_open`, `business_open_time`, `business_close_time`, `dropoff_from_time`, `dropoff_to_time`.

   - Purpose: controls per-day opening hours, drop-off windows, booking availability rules, and where alerts are sent.

2. **bookings** — Stores all customer booking records.

   - Fields:  

     `id`, `date`, `appointment_type`, `issue_description`, `customer_name`, `customer_mobile`, `vehicle_reg`, `created_at`.

   - Purpose: tracks each appointment request and stores customer details for the diary and notifications.

3. **garage_site_content** — Holds the editable content for the public-facing garage website.

   - Fields:  

     `id`, `business_name`, `tagline`, `about_text`, `address_line1`, `address_line2`, `city`, `postcode`, `phone`, `email`, `services[]` (each with `service_name`, `description`), `reviews[]` (each with `customer_name`, `review_text`, `stars`), `google_reviews_link`.

   - Purpose: defines what appears on the garage's public site, including contact info, services, and testimonials.

This file serves as your **single source of truth** — everything in Cursor (queries, types, schema) should use these names and fields exactly.
