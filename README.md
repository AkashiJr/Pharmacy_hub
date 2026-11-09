# Pharmacy Inventory Control Hub (CSC2854 Final Project)

Laravel 11 web application implementing the approved SRS/SDD: role-based access, medicine/category/supplier
master data, batch-level expiry tracking with FEFO, stock receiving/issuing (atomic, row-locked), low-stock /
near-expiry / expired alerts, dashboard, filtered reports (print + CSV) and an audit trail.

## Requirements
PHP 8.2+ (with pdo_mysql, mbstring, intl, xml), Composer, MySQL 8 / MariaDB (XAMPP is fine).

## Setup
```bash
composer install
cp .env.example .env            # edit DB_* if needed (default: MySQL db "pharmacy_hub", user root, no password)
php artisan key:generate
# create an empty database called pharmacy_hub in phpMyAdmin / mysql first
php artisan migrate --seed      # creates tables + synthetic demo data
php artisan serve               # http://127.0.0.1:8000
```
Demo logins (password for all: `Password@123`): `admin`, `manager`, `pharmacist`, `staff`.

## Tests
```bash
php artisan test                # TC01-TC13 (uses in-memory SQLite, no MySQL needed; enable pdo_sqlite)
```

## Role permissions
| Area | admin | manager | pharmacist | staff |
|---|---|---|---|---|
| Dashboard | yes | yes | yes | yes |
| Medicines (view), batches, receive, issue, reports | - | yes | yes | yes |
| Add / (de)activate medicines, categories, suppliers | - | yes | yes | - |
| Users, audit log | yes | - | - | - |

## Known limitations (stated in the report)
No medicine edit form (deactivate only), no ADJUSTMENT transaction screen, near-expiry window fixed at 30 days
(`config/pharmacy.php`), no database backup UI (use `mysqldump`).

All data is synthetic. This is an academic prototype, not clinical software.
