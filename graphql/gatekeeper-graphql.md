# Gatekeeper GraphQL Schema

## Overview

This conceptual GraphQL schema models the Gatekeeper contract lifecycle management (CLM) and vendor management platform. Gatekeeper provides procurement, legal, and finance teams with tools to capture, approve, store, and renew supplier contracts with workflow automation, e-signature, spend analytics, and risk monitoring.

The schema is derived from the Gatekeeper REST API surface, which exposes vendors, contracts, employees, custom data records, files, workflows, and events. The GraphQL representation provides a unified graph for integrating Gatekeeper data with ERP, HRIS, and finance systems.

## Schema Source

- **Provider:** Gatekeeper
- **API Reference:** https://knowledge.gatekeeperhq.com/en/docs/configuring-api
- **Base URL:** https://app.gatekeeperhq.com
- **Authentication:** Tenant-specific API key (per-tenant scoped)

## Core Domains

### Contracts
The central resource in Gatekeeper. Contracts have a lifecycle status, type, value, terms, parties, categories, milestones, and renewal/expiration tracking.

Types: `Contract`, `ContractDetails`, `ContractType`, `ContractStatus`, `ContractValue`, `ContractTerms`, `ContractParty`, `PartyDetails`, `PartyRole`, `ContractOwner`, `ContractCategory`

### Categories
Hierarchical classification of contracts and vendors into business categories.

Types: `Category`, `CategoryDetails`

### Suppliers and Vendors
Supplier and vendor profiles with contacts, risk scores, and relationship metadata.

Types: `Supplier`, `SupplierDetails`, `SupplierContact`, `SupplierProfile`, `Vendor`, `VendorDetails`, `VendorContact`

### Documents and Attachments
File management for contracts including versioned documents and attachments.

Types: `Document`, `DocumentDetails`, `DocumentVersion`, `Attachment`

### Reviews and Approvals
Structured review and approval workflows with chaining support.

Types: `Review`, `ReviewDetails`, `ReviewComment`, `Approval`, `ApprovalDetails`, `ApprovalChain`

### Milestones and Reminders
Time-based tracking for key contract events, deadlines, and automated reminders.

Types: `Milestone`, `MilestoneDetails`, `Reminder`, `ReminderDetails`

### Expiration and Renewal
Lifecycle management for contract end dates, renewal options, and renewal workflows.

Types: `Expiration`, `Renewal`, `RenewalDetails`

### Custom Fields
Tenant-configurable fields for extending core objects with domain-specific metadata.

Types: `CustomField`, `FieldType`, `FieldValue`

### Tags
Flexible tagging system for contracts, vendors, and documents.

Types: `Tag`, `TagDetails`

### Users and Teams
Identity and access management for Gatekeeper platform users.

Types: `User`, `UserDetails`, `UserRole`, `Team`, `TeamDetails`

### Webhooks and Events
Event-driven integration support via webhooks.

Types: `Webhook`, `WebhookEvent`

### Search and Reporting
Full-text search and analytics reporting capabilities.

Types: `SearchQuery`, `SearchResults`, `Report`, `ReportDetails`

### Authentication
API key and token management for tenant API access.

Types: `APIKey`, `Token`

## Schema File

See `gatekeeper-schema.graphql` for the full GraphQL type definitions.

## Usage Notes

- All queries are scoped to the authenticated tenant.
- Pagination uses `limit` and `offset` arguments on list fields.
- Date/time values use ISO 8601 format via the `DateTime` scalar.
- Monetary values use the `Float` type with an accompanying currency code field.
- Custom fields are returned as `[FieldValue]` on supported objects.
