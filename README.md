# Milon ERP

### Engineering case study — Arabic-first mobile-phone retail operations

**Portfolio owner:** [Firas Ahmed Sadiq](https://github.com/x97-bit)  
**Focus:** full-stack business applications · typed APIs · inventory workflows

> **What this repository contains:** a technical case study, not the application source or a runnable demo. The source remains private. No customer records, live credentials, operational exports or device identifiers are included here.

## The business problem

A phone retailer manages more than a product count. Each device has an IMEI, purchase cost, supplier and stock state. Accessories are quantity-based. A sale can create cash income, a customer balance, an installment obligation or a delivery-related balance.

Milon connects those workflows in an Arabic RTL interface so inventory, sales and collection records can be understood as one operational process.

This case study makes no claim about customer numbers, revenue, conversion gains or independently measured business impact.

## Product scope

- Device inventory with IMEI-oriented lookup and purchase/cost context.
- Quantity-based accessories and related stock operations.
- Supplier purchases, maintenance state and sales availability.
- Sales, customer balances, installments and delivery-related collection records.
- Store-aware roles, permissions, operational reporting and financial-record workflows.

## Architecture at a glance

**React / TypeScript interface → tRPC procedures and server-side validation → domain operations → Drizzle / MySQL**

| Layer | Main technologies | Responsibility |
| --- | --- | --- |
| Interface | React, TypeScript, Tailwind CSS | Arabic RTL screens, forms and operational workflows |
| Client data | tRPC, TanStack Query | Typed calls and request-state management |
| Server | Node.js, Express, tRPC, Zod | Input validation, access checks and business operations |
| Persistence | Drizzle ORM, MySQL | Inventory, invoices, balances and related domain records |

Types improve the client/server contract. They do not replace runtime authorization, transaction tests or financial reconciliation.

## Three engineering decisions

### 1. Model devices and quantities differently

Individual phones are tracked as identifiable devices; accessories are managed as quantities. This reflects the operating domain rather than forcing every item into the same inventory model.

**Tradeoff:** state transitions, duplicate checks and concurrent updates need explicit testing. Application checks alone should not be presented as database-level guarantees.

### 2. Keep the API contract visible

The client derives its tRPC types from the server router, while server-side schemas validate submitted input. This provides an explainable path from a form to a backend operation.

**Tradeoff:** a correctly typed identifier still needs ownership and permission checks. Static type safety is not proof of tenant isolation.

### 3. Separate the sale's core transaction from follow-up effects

The sales workflow groups core records and inventory changes transactionally, with additional follow-up operations handled separately.

**Tradeoff:** successful core persistence does not by itself demonstrate successful completion of every follow-up record. Reconciliation and failure-path tests are important evidence to collect.

## Recorded validation

**Snapshot date: 25 September 2026.** Checks were executed in a clean Linux review environment using Node.js 22.13.0 and the locked pnpm 10.4.1 dependency graph.

| Check | Recorded outcome |
| --- | --- |
| TypeScript, no emit | Passed |
| Browser and server production build | Passed, with existing analytics/chunk-size warnings |
| Selected service-free tests | **254 tests passed across 20 files** |
| Four database/Redis-dependent test files | Not run |
| Browser acceptance, live integrations and desktop packaging | Not run |

The selected tests include mocked dependencies, local logic and source assertions. **This is not a passing full integration suite or a production-readiness certificate.** The public case-study repository does not contain those private tests, so it does not display a misleading CI badge.

## A focused interview walkthrough

1. Explain why device identity, purchase cost and collection method belong in the same workflow.
2. Trace purchase → availability → sale → collection → reporting.
3. Describe the typed request boundary, server checks and database transaction.
4. Explain which checks passed and which still need an isolated integration environment.
5. Discuss an improvement and the test that would justify it before changing financial behavior.

A future live demonstration should use a disposable environment and wholly synthetic stores, customers, products and device identifiers. No such public demonstration is currently claimed here.

## Next engineering evidence

- Reproducible clean-database setup and synthetic fixtures.
- Cross-store authorization tests at the real API boundary.
- Concurrent stock/invoice and transaction rollback tests.
- Reconciliation checks across sales, collection and financial records.
- Arabic RTL browser acceptance and accessibility checks.

These are follow-up items, not completed work presented as features.

## Ownership and disclosure

This is a maintainer-curated portfolio case study, not a sole-author claim. Tool-assisted contributions remain part of the original history; author attribution is not rewritten for portfolio appearance. This document does not grant access to, or relicense, the private application source or third-party assets.

[Contact Firas](mailto:firasalsamaraai@gmail.com) · [LinkedIn](https://linkedin.com/in/firas-alsamaraai-255051257)
