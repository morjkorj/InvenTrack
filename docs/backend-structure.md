# Backend Structure

## Overview

This project follows a Service Layer Architecture using Laravel 12.

Principles:

* Thin Controllers
* Business Logic in Services
* Form Request Validation
* API Resources
* Eloquent Relationships
* Database Transactions
* Auditability through Stock Movements

---

# Directory Structure

```text
app/
│
├── Http/
│   │
│   ├── Controllers/
│   │   ├── Auth/
│   │   │
│   │   ├── CategoryController.php
│   │   ├── UnitController.php
│   │   ├── ProductController.php
│   │   ├── WarehouseController.php
│   │   ├── InventoryController.php
│   │   ├── StockMovementController.php
│   │   ├── SupplierController.php
│   │   ├── ProcurementController.php
│   │   └── WarehouseTransferController.php
│   │
│   ├── Requests/
│   │   │
│   │   ├── Category/
│   │   │   ├── StoreCategoryRequest.php
│   │   │   └── UpdateCategoryRequest.php
│   │   │
│   │   ├── Unit/
│   │   │   ├── StoreUnitRequest.php
│   │   │   └── UpdateUnitRequest.php
│   │   │
│   │   ├── Product/
│   │   │   ├── StoreProductRequest.php
│   │   │   └── UpdateProductRequest.php
│   │   │
│   │   ├── Warehouse/
│   │   │
│   │   ├── Inventory/
│   │   │
│   │   ├── Procurement/
│   │   │
│   │   └── Transfer/
│   │
│   └── Resources/
│       │
│       ├── CategoryResource.php
│       ├── UnitResource.php
│       ├── ProductResource.php
│       ├── WarehouseResource.php
│       ├── InventoryResource.php
│       ├── StockMovementResource.php
│       └── SupplierResource.php
│
├── Models/
│   │
│   ├── Category.php
│   ├── Unit.php
│   ├── Product.php
│   ├── Warehouse.php
│   ├── Inventory.php
│   ├── StockMovement.php
│   │
│   ├── Supplier.php
│   ├── ProcurementRequest.php
│   ├── PurchaseOrder.php
│   ├── WarehouseTransfer.php
│   │
│   └── User.php
│
├── Services/
│   │
│   ├── ProductService.php
│   ├── InventoryService.php
│   ├── StockMovementService.php
│   ├── ProcurementService.php
│   ├── WarehouseTransferService.php
│   └── ReportService.php
│
├── Enums/
│   │
│   ├── MovementType.php
│   ├── WarehouseStatus.php
│   ├── ProcurementStatus.php
│   └── TransferStatus.php
│
├── Policies/
│
├── Jobs/
│
├── Events/
│
└── Listeners/
```

---

# Current Phase Models

These are the models that should exist immediately.

```text
Category
Unit
Product
Warehouse
Inventory
StockMovement
```

Current Database Tables:

```text
categories
units
products
warehouses
inventories
stock_movements
```

---

# Service Responsibilities

## ProductService

Responsible for:

```text
Create Product
Update Product
Deactivate Product
SKU Validation
```

---

## InventoryService

Responsible for:

```text
Receive Stock
Adjust Stock
Reserve Stock
Release Stock
```

All inventory changes should go through this service.

---

## StockMovementService

Responsible for:

```text
Create Movement Logs
Audit Trail
Movement History
```

No inventory operation should occur without creating a stock movement.

---

## ProcurementService

Responsible for:

```text
Create Requests
Approve Requests
Generate Purchase Orders
Receive Deliveries
```

---

## WarehouseTransferService

Responsible for:

```text
Request Transfer
Approve Transfer
Execute Transfer
Update Inventories
Generate Logs
```

---

# Routes Structure

```text
routes/
│
├── api.php
├── web.php
└── console.php
```

Example API Routes:

```php
Route::apiResource('categories', CategoryController::class);
Route::apiResource('units', UnitController::class);
Route::apiResource('products', ProductController::class);
Route::apiResource('warehouses', WarehouseController::class);
```

---

# Inventory Rule

The most important rule in the system:

```text
Inventory quantity must never be updated directly.
```

Correct Process:

```text
InventoryService
    ↓
StockMovement Created
    ↓
Inventory Updated
```

This guarantees:

* Auditability
* Inventory Accuracy
* Easier Debugging
* Realistic ERP Workflow

---

# Current Development Priority

Phase 1:

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

Do not build Procurement, Transfers, Reports, or Dashboard Analytics until Phase 1 is complete.

The first milestone is:

Create Product
→ Receive Inventory
→ Create Stock Movement
→ Display Inventory


