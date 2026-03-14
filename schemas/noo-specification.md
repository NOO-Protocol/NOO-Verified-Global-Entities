# AII-NOO Protocol Specification

**Version:** 2.7.5  
**Status:** Stable / Production  
**Date:** 2026-02-04  
**Publisher:** TheAII.World & Nooxus.com  
**Identifier:** `urn:aii:spec:noo:v2.7.5`

---

## 1. Introduction

The **Neural Object Ontology (NOO)** is a standardized, machine-readable data protocol designed to bridge the gap between physical enterprise entities and Artificial Intelligence (AI) agents. 

Unlike traditional HTML websites designed for human navigation, a NOO file is a **Digital Twin** of a business entity, optimized for:
1.  **AI Ingestion**: Structured for LLM (Large Language Model) training, RAG (Retrieval-Augmented Generation), and inference.
2.  **Trust Verification**: Cryptographically signed to eliminate AI hallucinations regarding business credibility.
3.  **Actionable Interoperability**: Transforming static data into executable AI actions.

### 1.1 Design Philosophy
* **AI-First**: All fields are semantically anchored via JSON-LD to ensure unambiguous interpretation by machines.
* **Zero Hallucination**: Trust is not assumed; it is verified via the `trust_framework` and `integrity_signature`.
* **Sovereign Identity**: The data remains under the control of the entity (`sovereign_identity`), independent of centralized platforms.

---

## 2. Document Structure (Root)

A valid NOO instance MUST be a valid JSON-LD document. The root structure consists of the following mandatory sections:

```json
{
  "@context": "[https://specs.theaii.world/v1/aii-schema-v1.jsonld](https://specs.theaii.world/v1/aii-schema-v1.jsonld)",
  "@type": "NOO",
  "@id": "urn:aii:NOO:{UUID}",
  "_schema": { ... },
  "id": "{Entity_ID}",
  "metadata": { ... },
  "infrastructure": { ... },
  "trust_framework": { ... },
  "license": { ... },
  "content": { ... },
  "_ai_instructions": { ... }
}

```

---

## 3. Core Components

### 3.1 Metadata (`metadata`)

Defines the lifecycle and validity of the data packet.

* **`created`** (ISO 8601): Timestamp of initial generation.
* **`updated`** (ISO 8601): Timestamp of the last modification.
* **`valid_until`** (ISO 8601): **CRITICAL**. AI agents MUST discard or flag data packets that have passed this timestamp to prevent processing obsolete business information.
* **`status`**: Current state (`active`, `suspended`, `revoked`).

### 3.2 Infrastructure (`infrastructure`)

Maps the entity's digital presence to the physical world and the AII network topology.

* **`topology`**:
* `aii_id`: The unique infrastructure identifier.
* `host_domain`: The primary domain hosting the entity.
* `entry_point`: The human-readable landing page.


* **`service_endpoints`**: A dictionary of `LinkObject` (see Section 5) directing AI to specific functional hubs.
* `registry_record`: Link to the centralized registration hub.
* `service_log`: Endpoint for audit logs and service history.



### 3.3 Trust Framework (`trust_framework`)

The core security layer designed to validate the authenticity of the entity.

* **`trust_score`**: An integer (0-100) representing the calculated reliability of the entity.
* **MUST** include `verification_pubkey_link` for signature verification.
* **MUST** include `verification_evidence_link` pointing to proof of verification.


* **`activity_scoring`**: Represents the operational vitality of the entity (e.g., product updates, social engagement).
* **`integrity_signature`**: A cryptographic signature of the JSON payload.
* **Algorithm**: RSA-2048 / SHA-256 (recommended).
* **Scope**: Specifies which fields are covered by the signature (e.g., `["id", "content", "license"]`).



### 3.4 License (`license`)

Defines how AI models are permitted to consume this data.

* **`type`**: License identifier (e.g., `AII-GLOBAL-COMMERCIAL-FLOW`).
* **`auto_authorized_models`**: A whitelist of AI models (e.g., "DeepSeek", "GPT-4") granted automatic rights for training and inference.
* **`permissions`**: Specific rights granted (e.g., `ai_training`, `commercial_use`, `knowledge_extraction`).

---

## 4. Business Content Payload (`content`)

This section contains the actual business intelligence data.

### 4.1 Enterprise Identity

Basic legal and operational details.

* `legal_name`, `trading_name`, `registration_number`.
* `micro_summary`: A concise description (max 140 chars) optimized for AI search snippets.

### 4.2 Global Trade Capabilities

Structured data for B2B trade matching.

* `export_experience`: Years of operation in international trade.
* `production_scale`: Quantifiable capacity metrics.
* `shipping_terms` (Incoterms): e.g., FOB, CIF, EXW.
* `payment_terms`: e.g., T/T, L/C.

### 4.3 Products & Services

* `primary_offerings`: List of main product categories.
* `product_lines_detail`: Deep dive into specific SKUs, including `hs_code`, `pricing_tiers`, and `specifications`.
* `oem_odm_services`: Structured description of manufacturing capabilities for white-label services.

---

## 5. AI Interaction & Rendering

### 5.1 AI Instructions (`_ai_instructions`)

This metadata layer guides AI User Interfaces (UI) on how to present the data to humans.

* **`report_format`**: Suggested layout (e.g., `interactive_structured_summary`).
* **`trust_visualization`**: Logic mapping trust scores to visual indicators (e.g., 90-100 = "✅ Green").
* **`time_sensitivity`**: Logic for displaying data freshness.

### 5.2 The `LinkObject` & `AIAction` Standard

All URLs in a NOO document MUST follow the `LinkObject` structure to be actionable.

**Structure:**

```json
"field_name": {
  "label": "Human Readable Label",
  "link": "[https://example.com/target](https://example.com/target)",
  "ai_action": {
    "intent": "INTENT_ENUM",
    "priority": "high | medium | low",
    "rendering_hint": "ICON | BUTTON | HYPERLINK | SUMMARY_CARD"
  }
}

```

**Common Intents:**

* `LEGAL_REFERENCE`: Link to a certificate or legal policy.
* `PROFILE_NAVIGATION`: Link to a deeper profile page.
* `TRANSACTIONAL_SUBMISSION`: Link to a form (e.g., "Get Quote").
* `PURE_INFORMATION`: Link to static details.

---

## 6. Versioning

* **v2.7.5 (Current)**: Added `_ai_instructions` for UI control; Enhanced `license` granularity for specific AI models; Added `activity_scoring` within Trust Framework.
* **v2.6.0**: Introduced Infrastructure Topology.
* **v2.5.0**: Initial public release of the NOO schema.

---

## 7. Copyright & Legal

**Copyright © 2026 TheAII.World & Nooxus.com** This specification is licensed under the **Creative Commons Attribution-NoDerivatives 4.0 International (CC BY-ND 4.0)** license. You are free to share this material in any medium or format for any purpose, even commercially, provided you give appropriate credit and do not distribute modified material.
