# LSBUD Insight
Smarter Insights. Safer Sites.

## Purpose

**LSBUD Foresight** is a proposed LSBUD-owned Safe Digging Hub with **OneCall embedded as the required core search service**.

The strategic intent is to protect the value of OneCall, avoid heavy dependency on Pelican Corp front-end redevelopment, and give LSBUD the strategic platform needed to become the **UK’s de facto Safe Digging Hub**.

LSBUD owns the new portal, user journey, value-add service layer and account experience. OneCall remains the branded, mandatory core search service, integrated through API, secure handoff, or a controlled embedded component.

Hindsight — historical records, legacy plans, previous surveys, incident learning.
Insight — current site context, curated guidance, compliance, risk awareness.
Foresight — preventing incidents before work starts, supporting future VAR planning and proactive safe digging decisions.

That is much stronger than “Dig Safe Portal” as a product name, because Foresight suggests a forward-looking risk engine, not simply a search or document library.

## Strategic Positioning

- LSBUD owns the safe digging journey.
- OneCall remains central and mandatory.
- Pelican Corp remains strategically relevant.
- The programme avoids full OneCall front-end redevelopment.
- The MVP can be delivered faster than a major OneCall platform change.
- The platform can scale into content, compliance, risk awareness, evidence packs and premium services.
- The approach aligns with the wider industry logic of integrated workflows and data sources.

Safe Digging Hub Gateway
│
├── OneCall Utility Search
│   └── Required / default / non-removable
│
├── Tailored Guidance
│   ├── HSG47
│   ├── Domestic works guidance
│   ├── Utility works guidance
│   ├── Highways guidance
│   └── Emergency works guidance
│
├── Risk Awareness
│   ├── High voltage / high pressure prompts
│   ├── Open water proximity
│   ├── Environmental restrictions
│   ├── Large site routing
│   └── Linear route checks
│
├── Compliance / Evidence
│   ├── Search evidence pack
│   ├── WKT record
│   ├── PDF reports
│   └── Saved enquiry summary
│
└── Premium / Partner Services
    ├── Top-up searches
    ├── PAS128 / GPR survey quotes
    ├── Equipment / safety support
    ├── Environmental screening
    └── Managed review

Prototype Scope

The current prototype demonstrates:

LSBUD-branded Dig Safe Portal homepage.
    Guest and simulated logged-in user states.
    Header quick links to LSBUD, USAG and NUAR.
    Free Guidance Library access.
    Enquiry details step.
    Dig site search and draw step.
    WKT generation from drawn geometry.
    Large-site prompt and handoff.
    Recommendations based on work type and risk context.
    Basket step.
    Downloads & Actions step.
    Login-gated execution.
    OneCall Utility Search as locked, mandatory core service.
    Account area with user icon after login.
    History tab with searchable jobs.
    Downloads tab with job-specific download links.
    Notifications tab with configurable 28-day repeat reminder settings.
    Profile and Security placeholders.   

OneCall Integration Options

1. API Integration - The LSBUD Dig Safe Portal captures all required enquiry data, then submits a structured payload to OneCall.
    Pros
        Best user experience.
        No iframe security issues.
        LSBUD controls the portal.
        OneCall remains core but not visually dominant.
        Payload can be versioned.
        Works well with future premium services.
    Cons
        Requires Pelican Corp/API agreement.
        Needs integration governance.
        Needs authentication and audit handling.
   
3. Secure Handoff / Deep Link - The portal prepares the payload and sends the user into OneCall with a token or reference.
    Pros
        Much cheaper than rebuilding the OneCall UI.
        Lower-risk MVP.
        Allows LSBUD to build quickly.
        Pelican Corp only needs a controlled import endpoint or reference lookup.
    Cons
        Still needs some Pelican Corp support.
        User may briefly leave the Dig Safe Portal.
        Less seamless than full API integration.
   
3. Embedded OneCall Component - Pelican Corp could expose a small embeddable OneCall widget or micro-frontend.
The widget would only handle the core OneCall submission, not the whole user journey.
    Pros
        OneCall remains visibly present.
        Better than embedding the entire OneCall site.
        Smaller Pelican Corp development scope.
        Easier to govern and secure.
    Cons
        Still requires Pelican Corp development.
        Needs authentication/session handling.
        Needs a strict API contract.
   
Recommended Build

Front End
Build the LSBUD site as a standalone web app.

Possible frameworks:
    React
    Next.js
    Vue
    Svelte
    Static HTML prototype for early MVP demonstration

Suggested Production Stack
    Azure Static Web Apps
    React or Next.js
    Mapbox or Leaflet
    Azure Functions API layer
    Azure AD B2C or Microsoft Entra External ID for login
    Application Insights

Back-End / API Layer
Use a thin LSBUD-owned orchestration API.
Suggested endpoints:
    /api/enquiries
    /api/onecall/payload
    /api/services/recommendations
    /api/reports/open-water
    /api/large-site/handoff
    /api/account/history
    /api/account/downloads
    /api/account/notifications

The purpose of this API layer is to keep LSBUD in control of the portal experience while isolating the portal from OneCall/Pelican Corp implementation detail.

Target Architecture
Plain Text
Browser
 |
 v
LSBUD Dig Safe Portal
 |
 |-- Authentication
 |-- Work type journey
 |-- Map / geometry / WKT
 |-- Recommendation engine
 |-- Basket
 |-- Reports
 |-- Account history
 |-- Download storage
 |-- Repeat reminders
 |
 v
LSBUD Integration API
 |
 |-- OneCall payload service
 |-- Service recommendation service
 |-- Evidence/report service
 |-- Download storage service
 |-- Notification service
 |-- Audit/event log
 |
 +--> OneCall / Pelican API
 +--> Large Site Service
 +--> Premium service providers
 +--> NUAR/other sources where permitted

Account, History and Download Storage
The portal should support logged-in users through a persistent account area.

Account Features
    User profile.
    Job history.
    Downloads by job.
    Products selected or ordered by job.
    28-day repeat reminder settings.
    Password/security settings.
    
Job History
Each saved job should include:
    Portal reference.
    OneCall reference, where available.
    User reference.
    Work category.
    Work type.
    Search value.
    Geometry type.
    WKT.
    Area or route length.
    Status.
    Products selected.
    Download links.
    Reminder settings.

Download Storage
Jobs and products should be delivered back to the Dig Safe Portal and saved as controlled download links.

Stored outputs may include:
    OneCall submission receipt.
    OneCall response pack.
    Safe Digging Guidance Pack.
    Open Water Proximity Risk Report.
    Environmental Restrictions Check.
    PAS128 summary or route card.
    WKT file.
    Evidence pack.
    Premium service request summary.

Recommended storage approach:
    Database = metadata
    Blob storage = files
    API = access control and download authorisation

Recommended Data Model
Users
    {
     "userId": "usr_001",
     "email": "user@example.com",
     "name": "John Bennett",
     "organisation": "LSBUD",
     "defaultReminderDays": 28,
     "defaultReminderEnabled": true
    }

Jobs
    {
     "jobId": "job_42819372",
     "portalReference": "DSP-42819372",
     "userReference": "Your Reference",
     "userId": "usr_001",
     "status": "submitted",
     "createdAt": "2026-07-21T09:40:00Z",
     "submittedAt": "2026-07-21T09:55:00Z",
     "enquiryType": "Information Only",
     "worksCategory": "Domestic Works (General public)",
     "worksType": "Fencing / gates",
     "searchType": "Postcode/Town",
     "searchValue": "SY5 6PR",
     "geometryType": "polygon",
     "wkt": "POLYGON((...))",
     "areaHa": 0.42,
     "lengthKm": null,
     "repeatReminderEnabled": true,
     "repeatReminderDays": 28,
     "nextReminderDate": "2026-08-18"
    }

Products Selected
    {
     "jobProductId": "jp_001",
     "jobId": "job_42819372",
     "productCode": "ONECALL_SEARCH",
     "productName": "OneCall Utility Search",
     "productType": "core",
     "status": "submitted",
     "selectedAt": "2026-07-21T09:52:00Z"
    }

Downloads
    {
     "downloadId": "dl_001",
     "jobId": "job_42819372",
     "productCode": "OPEN_WATER_REPORT",
     "fileName": "Open_Water_Proximity_Risk_Report_42819372.pdf",
     "fileType": "pdf",
     "storagePath": "jobs/job_42819372/reports/open-water.pdf",
     "downloadUrl": "/api/jobs/job_42819372/downloads/dl_001",
     "createdAt": "2026-07-21T09:58:00Z",
     "expiresAt": null
    }

Recommended Phased Delivery
Phase 1 — MVP Without Pelican Corp Dependency
    LSBUD Dig Safe Portal.
    Guest journey.
    Map and WKT.
    Value-add recommendations.
    Basket.
    PDF demo reports.
    Large Site handoff.
    OneCall payload preview/export.
    Simulated account history and downloads.
Phase 2 — Light Pelican Corp Integration
    Secure handoff token.
    OneCall import endpoint.
    Pre-populated enquiry.
    Return reference/status.
    Store OneCall reference against the Portal job.
Phase 3 — Full API Integration
    Submit OneCall enquiry from LSBUD portal.
    Receive status updates.
    Retrieve OneCall responses.
    Save evidence pack.
    Save download links against the job.
Phase 4 — Partner Ecosystem
    Premium services.
    Survey quotes.
    Guidance packs.
    Environmental checks.
    Compliance reporting.
    Member-specific workflows.
    Repository Contents

Suggested repository structure:
    /
    ├── index.html
    ├── README.md
    ├── /docs
    │ ├── architecture.md
    │ ├── onecall-integration.md
    │ ├── account-history.md
    │ ├── download-storage.md
    │ └── roadmap.md
    └── /assets
     └── screenshots


Running the Prototype
This is currently a static HTML prototype.

To run locally:
    Save the prototype as index.html.
    Open index.html in a modern browser.
    For map tiles and external libraries, internet access is required.

To deploy using GitHub Pages:
    Place index.html in the repository root or the configured Pages folder.
    Commit and push.
    Enable GitHub Pages for the selected branch/folder.
    Open the published GitHub Pages URL.
    
Important Notes
    This is a prototype, not a production implementation.
    Authentication is simulated.
    Job history and download storage are simulated in browser memory.
    OneCall submission is simulated.
    Production delivery will require secure authentication, API integration, storage, audit logging and governance.
    
Summary
The LSBUD Dig Safe Portal provides a route to an LSBUD-owned safe digging platform while keeping OneCall central, mandatory and strategically visible.
The recommended approach is to build the Portal independently, integrate OneCall through API or secure handoff, and use the Portal to orchestrate guidance, risk awareness, evidence, account history, downloads and premium partner services.
