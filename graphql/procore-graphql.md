# Procore GraphQL Schema

## Overview

This is a conceptual GraphQL schema for the Procore construction management platform. Procore exposes its data via a REST API (v1) at `https://api.procore.com`, documented at `https://developers.procore.com/reference/rest/v1/`. This schema represents how Procore's core domain objects would be expressed as a GraphQL API, covering project management, financials, quality and safety, field productivity, documents, scheduling, and platform administration.

## Source

- REST API Docs: https://developers.procore.com/reference/rest/v1/
- Developer Portal: https://developers.procore.com
- GitHub Organization: https://github.com/procore-oss
- Base URL: https://api.procore.com

## Domain Coverage

The schema covers the following Procore platform domains:

### Company and User Management
Types: `Company`, `CompanyDetails`, `CompanyUser`, `CompanyRole`, `User`, `UserDetails`, `UserRole`, `UserPermissions`

Companies are the top-level organizational unit in Procore. Each company contains projects and users. Users belong to companies with specific roles and permissions governing what they can access.

### Project Management
Types: `Project`, `ProjectDetails`, `ProjectStage`, `ProjectStatus`

Projects are the central organizing unit for construction work. Each project has a stage (e.g., Pre-Construction, Construction, Closeout) and a status (Active, Inactive, Archived). Project details capture location, dates, contract amounts, and associated company and owner information.

### Submittals
Types: `Submittal`, `SubmittalItem`, `SubmittalRevision`

Submittals track the review and approval of project documents and materials. Each submittal can have multiple items and revisions, with workflow states progressing from open through revision requests to final approval.

### RFIs (Requests for Information)
Types: `RFI`, `RFIResponse`

RFIs are formal requests from the field or from contractors seeking clarification on project documents. Each RFI can receive one or more responses and tracks due dates, priority, and status.

### Correspondence
Types: `Correspondence`, `CorrespondenceType`

Correspondence tracks formal written communications on a project, categorized by type (e.g., letters, notices, transmittals).

### Daily Logs
Types: `DailyLog`, `WorkLog`, `WeatherLog`

Daily logs capture field productivity data including labor, equipment, materials, weather conditions, and notes recorded each day on a project.

### Quality and Safety - Inspections
Types: `Inspection`, `InspectionDetail`, `InspectionTemplate`, `InspectionItem`, `Checklist`

Inspections and checklists are used to conduct quality and safety audits on site. Templates define the structure of inspection items; individual inspections reference a template and record pass/fail/NA results per item.

### Observations
Types: `Observation`, `ObservationItem`

Observations are field-reported items (deficiencies, punch list items, safety concerns) that require follow-up action. Each observation can have multiple items with status tracking.

### Incidents
Types: `Incident`, `IncidentType`

Incidents capture safety events on the project site, categorized by type (near miss, injury, property damage, environmental). They include details on involved parties, witnesses, and corrective actions.

### Drawings
Types: `Drawing`, `DrawingSet`, `DrawingRevision`

Drawings represent the construction documents managed on a project. Drawing sets group drawings by discipline or submission package. Revisions track superseded versions.

### Specifications
Types: `Specification`, `SpecSection`, `SpecRevision`

Specifications define the technical requirements for materials and workmanship. They are organized by section (following CSI MasterFormat divisions) with revisions tracked over time.

### Meetings
Types: `Meeting`, `MeetingItem`, `MeetingMinutes`

Meetings are scheduled or recorded gatherings on a project, with agenda items, action items, and formal minutes published after the meeting.

### Documents
Types: `Document`, `DocumentFolder`, `DocumentVersion`

Documents covers file management in Procore's document management module, organizing files in folder hierarchies with version history.

### Photos
Types: `Photo`, `Album`, `AlbumPhoto`

Photos are images captured on site and organized into albums with captions and location metadata.

### Schedule
Types: `Schedule`, `ScheduleTask`, `ScheduleMilestone`

Schedule management covers project timelines with tasks (activities) and milestones, supporting import from and export to standard scheduling tools.

### Budget and Financials
Types: `Budget`, `BudgetLineItem`, `BudgetChange`, `CostCode`, `DirectCost`

The budget module tracks the original contract value, approved changes, projected costs, and actuals by cost code. Budget changes record approved and pending adjustments.

### Contracts and Procurement
Types: `SubContractor`, `Contract`, `ContractChange`, `Bid`, `BidPackage`

Contracts cover subcontracts and owner contracts with full change order management. Bids and bid packages support the procurement workflow before a contract is awarded.

### Invoices and Payments
Types: `Invoice`, `Payment`, `ComplianceDocument`

Invoices track subcontractor and owner billing with schedule of values. Payments record amounts disbursed. Compliance documents (insurance certificates, lien waivers) are linked to contracts and invoices.

### Platform Administration
Types: `APIKey`, `OAuthToken`, `Webhook`

Platform administration types cover authentication credentials and event notification configuration. Procore uses OAuth 2.0 for API access. Webhooks allow subscribing to real-time events on company or project resources.

## Schema File

See `procore-schema.graphql` for the full GraphQL SDL type definitions.

## Usage Notes

- All IDs are represented as `ID` (integer-backed in Procore's REST API).
- Timestamps use the `String` scalar (ISO 8601); a `DateTime` custom scalar is defined.
- Monetary values use `Float` (USD).
- Enums reflect Procore's documented status strings; additional values may exist in practice.
- This schema is conceptual. Procore does not currently publish an official GraphQL endpoint.
