# HM NOW — Quick Commerce for H&M, Powered by Klydo

---

## Slide 1: How It Works — End-to-End Process Flow

### H&M's Experience, Klydo's Engine

H&M keeps full customer ownership. Klydo is invisible infrastructure behind HM NOW.

```
H&M App / hm.com
        │
        ▼
┌─────────────────────────────────────────────────┐
│  H&M's Cloud Environment                       │
│                                                 │
│  ┌───────────────┐    ┌──────────────────────┐  │
│  │  HM NOW UI    │───▶│  Klydo Backend + AI  │  │
│  │  (H&M design  │    │  (deployed inside    │  │
│  │   system)     │    │   H&M's infra)       │  │
│  └───────────────┘    └──────────┬───────────┘  │
│                                  │              │
└──────────────────────────────────┼──────────────┘
                                   │
                    Secure API     │
                                   ▼
                         ┌──────────────────┐
                         │   Fynd Platform   │
                         │  (OMS + WMS + TMS)│
                         └────────┬─────────┘
                                  │
                    ┌─────────────┼─────────────┐
                    ▼             ▼              ▼
              Dark Store    Last-Mile       Reverse
              Fulfillment   Delivery       Logistics
```

### Order Placement Flow

| Step | What Happens | Who Owns It |
|------|-------------|-------------|
| 1. Browse & Discover | H&M customer opens HM NOW tab, sees quick-delivery eligible H&M catalog with AI-powered recommendations | H&M UI + Klydo AI |
| 2. Serviceability Check | Real-time pincode validation — is 15-min delivery available at this customer's location? | Klydo Backend |
| 3. Cart & Checkout | Customer places order within H&M's native checkout experience | H&M UI + Klydo OMS |
| 4. Payment Processing | Payment captured via H&M's existing payment gateway | H&M's Payment Infra |
| 5. Warehouse Assignment | Klydo assigns nearest dark store stocking H&M inventory, reserves units | Klydo Backend → Fynd WMS |
| 6. Dispatch & Delivery | Picker packs H&M order, rider dispatched, customer sees live tracking | Fynd TMS + Last-Mile Partner |
| 7. Delivered | Customer receives H&M order in 15–60 mins | Last-Mile Partner |

### Returns Flow

| Step | What Happens | Who Owns It |
|------|-------------|-------------|
| 1. Initiate Return | Customer requests return from H&M's app — same UX as regular H&M returns | H&M UI → Klydo Backend |
| 2. Eligibility Check | Auto-validated against H&M's return policy (time window, category rules) | Klydo Backend |
| 3. Auto-Approve | Return approved instantly, reverse shipment created | Klydo Backend → Fynd TMS |
| 4. Pickup Scheduled | Rider picks up from customer's location | Last-Mile Partner |
| 5. QC & Restock | Item received at dark store, quality checked, restocked if eligible | Dark Store Ops |
| 6. Refund Processed | Refund initiated to customer's original payment method | Klydo Backend → H&M's PSP |

**Key point**: The entire return loop is automated. No manual intervention. Average resolution: < 48 hours.

---

## Slide 2: User Journey — What H&M's Customer Sees

### From Opening HM NOW to Doorbell in 15 Minutes

```
┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐
│  Open     │   │  Browse   │   │  Add to  │   │  Pay     │   │  Track   │
│  HM NOW   │──▶│  H&M     │──▶│  Cart    │──▶│  (H&M's  │──▶│  Live    │
│  Tab      │   │  Catalog  │   │          │   │  gateway) │   │  Delivery│
└──────────┘   └──────────┘   └──────────┘   └──────────┘   └──────────┘
                    │                                             │
            AI-powered discovery                          Real-time rider
            + Bangalore location-aware                    tracking on map
            availability
```

**What H&M's customer never sees**: Klydo. The entire experience feels native to H&M.

### What HM NOW Unlocks for H&M

| H&M Today | H&M with HM NOW |
|-----------|------------------|
| 3–7 day delivery via standard e-com | 15 min – same day delivery in Bangalore |
| Loses impulse buyers to Myntra/Ajio | Captures impulse demand instantly |
| High cart abandonment on slow delivery | 50%+ cart conversion (proven at Klydo) |
| No dark store operations capability | Fully managed dark store fulfillment by Klydo |
| Building q-com in-house: 12–18 months | HM NOW go-live: 4–6 weeks |
| Competing with Slikk, Myntra minutes | First-mover in branded fashion q-com |

---

## Slide 3: Security & Data Architecture — H&M's Data Stays with H&M

### Deployment Model: H&M's Cloud, H&M's Data, Klydo's Code

```
┌─ H&M's Cloud (AWS / GCP / Azure) ──────────────────────────┐
│                                                              │
│  ┌─────────────────────┐     ┌────────────────────────────┐  │
│  │  Klydo Backend      │     │  H&M's Database            │  │
│  │  (containerized)    │────▶│  (PostgreSQL — dedicated)   │  │
│  │                     │     │  H&M owns all data          │  │
│  └─────────┬───────────┘     └────────────────────────────┘  │
│            │                                                 │
│  ┌─────────▼───────────┐     ┌────────────────────────────┐  │
│  │  Redis Cache        │     │  Object Storage (S3/GCS)   │  │
│  │  (session, catalog) │     │  Media, invoices           │  │
│  └─────────────────────┘     └────────────────────────────┘  │
│                                                              │
└──────────────────────────────────────────────────────────────┘
         │                              │
         │ Encrypted API (TLS 1.3)      │ No H&M customer PII
         ▼                              │ leaves H&M's cloud
   ┌──────────┐                         │
   │   Fynd   │  ◀──────────────────────┘
   │ Platform  │  Only order + inventory
   └──────────┘  data (no customer PII)
```

### Security Guarantees for H&M

| Concern | How We Handle It |
|---------|-----------------|
| **Data Residency** | All H&M customer data (PII, payment, orders) lives in H&M's cloud account. Klydo has zero access to production data outside deployment windows. |
| **Code Isolation** | Klydo backend runs as isolated containers (Kubernetes) within H&M's infrastructure. No shared compute with Klydo's own platform or any other brand. |
| **Network Security** | All external communication over TLS 1.3. Internal services communicate within H&M's VPC. No public endpoints except H&M's own load balancer. |
| **PII Boundary** | H&M customer PII never leaves H&M's cloud. Only fulfillment data (SKU, quantity, dark store address) is sent to Fynd for dispatch. |
| **Payment Security** | Klydo never touches card data. Payments flow through H&M's existing PCI-DSS compliant gateway. Klydo only receives payment confirmation tokens. |
| **Access Control** | Klydo engineers get time-boxed, audited access for deployments only. No standing access to H&M's infra. All access governed by H&M's IAM policies. |
| **Audit Trail** | Every order, payment, refund, and inventory change is logged with immutable audit trails in H&M's database. Fully auditable by H&M's compliance team. |
| **Software Updates** | All Klydo software updates are delivered automatically via Kubernetes rolling deployments within H&M's cloud. Zero downtime, no manual intervention from H&M's team. H&M retains full visibility and approval control over what gets deployed in their cluster. |

### What Fynd Sees vs What It Doesn't

| Fynd Receives | Fynd Never Sees |
|--------------|-----------------|
| H&M SKU IDs, quantities | H&M customer name, email, phone |
| Dark store location | Payment details |
| Delivery pincode | H&M customer browsing history |
| Order status updates | H&M's pricing or discount strategy |

---

## What H&M Needs to Provide

| From H&M | Purpose |
|----------|---------|
| Load balancer routing for HM NOW tab | Traffic routing to Klydo-powered UI |
| Mobile codebase access (or webview slot) | Embed HM NOW experience natively |
| Cloud account / namespace | Deploy Klydo backend in H&M's infra |
| H&M catalog feed (SKU, pricing, media) | Populate HM NOW catalog |
| Payment gateway credentials | Process payments through H&M's PSP |

**Everything else — backend, AI, fulfillment ops, dark store management, logistics — is Klydo.**

---

### Why H&M Should Move Now

- **First-mover advantage**: No fashion brand in India has branded quick-commerce today. H&M can own this category.
- **Battle-tested**: Klydo is already live, processing orders at scale — 45% WoW growth, NPS 72, 50%+ cart conversion.
- **Zero build risk**: This is not a POC. It's production-grade infrastructure deployed in 4–6 weeks.
- **Zero data risk**: H&M's customer data never leaves H&M's cloud. Klydo is plumbing, not a platform.
- **Shared economics**: Klydo's dark store network is already operational in Bangalore. H&M gets instant access without building a single warehouse.
