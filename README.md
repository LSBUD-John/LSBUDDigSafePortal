LSBUD-owned Safe Digging Hub with OneCall embedded as the required core search service.
This protects the value of OneCall, avoids heavy dependency on Pelican front-end development, and gives LSBUD the strategic platform needed to become the UK’s de facto Safe Digging Hub.
LSBUD owns the new portal and value-add journey. OneCall remains the branded mandatory core search service, integrated through API, secure handoff, or a controlled embedded component.

LSBUD owns the safe digging journey.
OneCall remains central and mandatory.
Pelican remains strategically relevant.
Avoids full OneCall front-end redevelopment.
Supports faster MVP delivery.
Creates a scalable platform for content, compliance, risk and premium services.
Aligns with the industry logic of integrated workflows and data sources.

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

Architecture options:

API integration - the LSBUD Dig Safe Portal captures all required enquiry data, then submits a structured payload to OneCall.
    Pros
        Best user experience.
        No iframe security issues.
        LSBUD controls the portal.
        OneCall remains core but not visually dominant.
        Payload can be versioned.
        Works well with future premium services.
    Cons
        Requires Pelican/API agreement.
        Needs integration governance.
        Needs authentication and audit handling.
        
Secure handoff / deep link - the portal can prepare the payload and send the user into OneCall with a token/reference.
    Pros
        Much cheaper than rebuilding OneCall UI.
        Lower-risk MVP.
        Lets LSBUD build quickly.
        Pelican only needs a controlled import endpoint or reference lookup.
    Cons
        Still needs some Pelican support.
        User may briefly leave the Dig Safe Portal.
        Less seamless than full API.

Embedded OneCall component - Pelican Corp could expose a small embeddable OneCall widget or micro-frontend
    The widget would only handle the core OneCall submission, not the whole user journey.
    Pros
        OneCall remains visibly present.
        Better than embedding the entire site.
        Smaller Pelican development scope.
        Easier to govern and secure.
    Cons
        Still requires Pelican development.
        Needs authentication/session handling.
        Needs strict API contract.

Recommended Build

Front-end
Build the LSBUD site as a standalone web app:
    React / Next.js / Vue / Svelte
    or simple static HTML prototype for MVP

Suggested production stack:
    Azure Static Web Apps
    React or Next.js
    Mapbox or Leaflet
    Azure Functions API layer
    Azure AD B2C / Entra External ID for login
    Application Insights

Back-end/API layer   
Use a thin LSBUD-owned orchestration API:
    /api/enquiries
    /api/onecall/payload
    /api/services/recommendations
    /api/reports/open-water
    /api/large-site/handoff

Target architecture
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
      |
      v
    LSBUD Integration API
      |
      |-- OneCall payload service
      |-- Service recommendation service
      |-- Evidence/report service
      |-- Audit/event log
      |
      +--> OneCall / Pelican API
      +--> Large Site Service
      +--> Premium service providers
      +--> NUAR/other sources where permitted

Recommended phased delivery
Phase 1 — MVP without Pelican Corp dependency
    LSBUD Dig Safe Portal
    Guest journey
    Map and WKT
    Value-add recommendations
    Basket
    PDF demo reports
    Large Site handoff
    OneCall payload preview/export
Phase 2 — Light Pelican Corp integration
    Secure handoff token
    OneCall import endpoint
    Pre-populated enquiry
    Return reference/status
Phase 3 — Full API integration
    Submit OneCall enquiry from LSBUD portal
    Receive status
    Retrieve responses
    Save evidence pack
Phase 4 — Partner ecosystem
    Premium services
    Survey quotes
    Guidance packs
    Environmental checks
    Compliance reporting
    Member-specific workflows
