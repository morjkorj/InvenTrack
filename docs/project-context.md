# Inventory Management System

## Project Overview

This project is a portfolio-grade Inventory Management System designed to simulate real-world inventory operations for businesses such as coffee shops, distributors, warehouses, and retail stores.

The system focuses on:

* Inventory accuracy
* Stock movement tracking
* Warehouse management
* Procurement workflows
* Auditability
* Scalability
* Maintainability

This is **not a POS system** and **not a full ERP**. The primary goal is to demonstrate enterprise-level inventory management concepts and software architecture.

---

# Technology Stack

## Backend

* Laravel 12
* PHP 8.4+
* Laravel Sanctum
* Laravel Queues
* Laravel Scheduler
* Spatie Permission

## Frontend

* React 19
* TypeScript
* React Router
* TanStack Query
* React Hook Form
* Zod
* Shadcn/UI
* Tailwind CSS
* Recharts

## Database

### Development Environment

* XAMPP

### Database Engine

* MySQL / MariaDB

### Database Name

```text
inventory_management
```

---

# Architecture Principles

## API First

All business functionality must be exposed through REST APIs.

Controllers should:

* Validate requests
* Call services
* Return API responses

Controllers must not contain business logic.

---

## Service Layer Pattern

Business operations should be handled through dedicated service classes.

Examples:

```text
InventoryService
StockMovementService
ProcurementService
WarehouseTransferService
ProductService
```

Benefits:

* Maintainability
* Testability
* Separation of concerns

---

## Database Transactions

Critical inventory operations must always use transactions.

Examples:

* Stock receiving
* Inventory adjustments
* Warehouse transfers
* Procurement approvals
* Stock reservations

Inventory consistency is the highest priority.

---

## Auditability

Every inventory change must generate a stock movement record.

No inventory quantity should be modified directly without creating an audit trail.

---

# Core Modules

## Authentication & Authorization

Roles:

```text
Super Admin
Inventory Manager
Warehouse Staff
Procurement Officer
```

Permissions will be managed using Spatie Permission.

---

## Product Management

### Categories

Examples:

```text
Coffee Beans
Dairy
Syrups
Packaging
Cleaning Supplies
Food Ingredients
```

### Units

Examples:

```text
kg
g
L
ml
pcs
```

### Product Fields

```text
sku
name
description
cost_price
minimum_stock_level
category_id
unit_id
is_active
```

---

## Warehouse Management

Example Warehouses:

```text
Main Warehouse
Branch A Storage
Branch B Storage
```

Warehouse Fields:

```text
name
location
status
```

---

## Inventory Management

Inventory is tracked per warehouse.

Inventory Fields:

```text
warehouse_id
product_id
quantity
reserved_quantity
```

Available Stock Formula:

```text
available_stock = quantity - reserved_quantity
```

Available stock should be calculated, not stored.

Negative inventory is not allowed.

---

## Stock Movements

Every inventory change creates a movement record.

Movement Types:

```text
purchase
sale
reservation
release
transfer_in
transfer_out
adjustment
waste
```

Stock movements serve as the inventory audit trail.

---

## Procurement Management

Workflow:

```text
Request
Approval
Purchase Order
Receiving
Completed
```

Features:

* Supplier Management
* Purchase Orders
* Receiving Records
* Approval Workflow

---

## Supplier Management

Fields:

```text
company_name
contact_person
email
phone
address
```

Suppliers may provide multiple products.

---

## Warehouse Transfers

Workflow:

```text
Requested
Approved
In Transit
Completed
Cancelled
```

Transfer Process:

```text
Deduct Source Inventory
Create Transfer Out Movement

Increase Destination Inventory
Create Transfer In Movement
```

---

# Reporting

## Inventory Report

Metrics:

```text
Current Stock
Reserved Stock
Available Stock
Inventory Value
```

---

## Low Stock Report

Displays products below minimum stock levels.

---

## Stock Movement Report

Displays:

* Purchases
* Adjustments
* Waste
* Transfers
* Reservations

---

## Procurement Report

Metrics:

```text
Purchase Orders
Supplier Performance
Procurement Costs
```

---

# Dashboard

## Executive Metrics

```text
Total Products
Total Inventory Value
Active Warehouses
Low Stock Items
```

## Inventory Metrics

```text
Current Stock
Reserved Stock
Available Stock
```

## Operational Metrics

```text
Pending Procurement Requests
Pending Transfers
Recent Stock Movements
```

---

# Database Structure

Core Tables:

```text
users
roles
permissions

categories
units

products

warehouses
inventories

stock_movements

suppliers

procurement_requests
purchase_orders

warehouse_transfers
```

---

# Development Phases

## Phase 1

Foundation

```text
Authentication
Roles & Permissions
Categories
Units
Products
Warehouses
Inventory
Stock Movements
```

## Phase 2

Inventory Operations

```text
Stock Receiving
Inventory Adjustments
Inventory Reports
```

## Phase 3

Procurement

```text
Suppliers
Purchase Requests
Purchase Orders
Receiving
```

## Phase 4

Warehouse Transfers

```text
Transfer Requests
Approval Workflow
Transfer Execution
```

## Phase 5

Reporting & Dashboard

```text
Analytics
Charts
Executive Dashboard
```

---

# Portfolio Objective

This project is intended to demonstrate:

* Laravel Architecture
* Service Layer Design
* REST API Development
* Role-Based Access Control
* Database Design
* Inventory Audit Trails
* Transaction Management
* React + TypeScript Frontend Development
* Enterprise Application Structure

