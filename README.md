# Tata Supply Chain Co. Ltd. — Procurement & Inventory DBMS

> An enterprise-grade Database Management System designed for Procurement, Quality Inspection, and Material Issue Management.

## 📋 Table of Contents
- [Academic Context](#academic-context)
- [Project Scope & Business Logic](#project-scope--business-logic)
- [Database Architecture](#database-architecture)
- [Entity Data Model](#entity-data-model)
- [Getting Started](#getting-started)

---

## 🎓 Academic Context
- **Institution:** Vidyalankar Institute of Technology (VIT), Mumbai
- **Program:** Computer Engineering (CMPN) - Batch A
- **Course:** Final Project Vidyanidhi (MySQL & MongoDB Credit Transfer Course)
- **Team Members:** - Ali Mehdi Mirza (24102C0054)
  - Kaab Ansari (24102C0056)
  - Ziyad Mujawar (24102C0082)

---

## 📌 Project Scope & Business Logic

This database is engineered to handle the operational logistics of a mid-to-large scale supply chain, ensuring high data integrity and zero redundancy. 

- **Inventory Scale:** Manages approximately 200 raw material items and 75 finished parts, each uniquely categorized and tracked for dynamic stock levels, ordering metrics, and pricing.
- **Procurement Pipeline:** Materials received via vendor Challans are systematically recorded as auto-generated Goods Received Reports (GRR).
- **Quality Assurance Routing:** Enforces a strict quality control workflow where only inspected and approved quantities are inducted into live stock; rejected items are isolated.
- **Internal Distribution:** Automates material distribution to internal production departments through Material Issue Requisitions (MIR).
- **Vendor & Logistics Mapping:** Models a complex ecosystem involving 5 primary transporters and multiple vendors using a many-to-many relationship structure (resolved via bridge tables) to accurately track vendor-specific pricing and multi-source procurement.

---

## ⚙️ Database Architecture

The schema is optimized for data integrity and rapid transactional logging.

| Metric | Detail |
| :--- | :--- |
| **Total Entities** | 15 Tables (12 Master/Transaction + 3 Child Detail) |
| **Normalization** | Optimized to **Third Normal Form (3NF)** |
| **Primary Key Strategy** | Natural keys for Master tables (e.g., `PartNo`, `VendorCode`); Surrogate auto-increment IDs for Transaction/Log tables. |
| **Relationship Types** | Primarily One-to-Many (1:M); Many-to-Many (M:M) resolved via `VendorPart`. |
| **Automation** | System auto-generation for `GRRNo` and `MIRNo` based on business rules. |

---

## 🗄️ Entity Data Model

The database is logically partitioned into three domains: Master Data, Transactional Data, and Inventory Tracking.

### Master Entities
* **`PartCategory`:** Classifies parts (Raw Material / Finished Part / Bought-out component).
* **`Part`:** Master directory of all materials and parts, detailing rates, Unit of Measurement (UOM), and stock thresholds.
* **`Vendor`:** Directory of supplying vendors, including contact details and active status.
* **`VendorPaymentTerms`:** Financial agreements configured per vendor and supply type.
* **`Transporter`:** Registry of authorized logistics partners handling deliveries.
* **`Department`:** Internal production units that consume the procured materials.

### Relational Bridge Entities
* **`VendorPart`:** Resolves the M:M relationship between Vendors and Parts, storing critical vendor-specific supply rates.

### Transactional & Operations Entities
* **`PurchaseOrder` & `PODetail`:** Header and line-item records of official company orders issued to vendors.
* **`GRR` & `GRRDetail`:** Header and itemized logs for goods received against vendor Challans.
* **`QualityInspection`:** Granular tracking of accepted vs. rejected quantities for every GRR line item.
* **`MIR` & `MIRDetail`:** Header and itemized tracking of internal requisitions raised by production departments.

### Ledger & Tracking
* **`StockLedger`:** The core operational ledger recording running stock balances, tracking all valid receipts and issues to support minimum stock alerts and opening balances.

---

## 🚀 Getting Started

### Prerequisites
* MySQL Server (v8.0+)
* MongoDB (for NoSQL credit transfer components, if applicable)

### Installation
1. Clone this repository:
   ```bash
   git clone [https://github.com/yourusername/tata-supply-chain-db.git](https://github.com/yourusername/tata-supply-chain-db.git)
