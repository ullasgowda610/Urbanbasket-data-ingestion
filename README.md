# UrbanBasket – The Data Challenge

## 1. Case Study
UrbanBasket is a growing grocery delivery company that wants to bring information from **stores, delivery teams, and the customer application** into one central data platform.

The sources have different arrival patterns and freshness requirements. Some information arrives late, some records are incomplete or duplicated, and sometimes a store corrects information that was already shared.

## 2. Problem Statement
UrbanBasket needs a simple and reliable data ingestion approach that can:
- Bring data from all three sources into one central platform.
- Support different freshness requirements.
- Handle late-arriving, incomplete, and duplicate records.
- Handle corrected information without creating unnecessary duplicates.
- Avoid repeatedly processing information that has not changed.
- Provide trusted data for analytics and business teams.

## 3. Objective
To propose an ingestion architecture that matches the ingestion method to each source and provides a clear flow for validation, change handling, error handling, and delivery of trusted data.

## 4. Proposed Approach

| Source | Proposed Ingestion | Reason |
|---|---|---|
| Stores | Batch ingestion | Store information is generally shared at the end of the day. |
| Delivery Team | Real-time / Streaming | Delivery events need to be available as they happen. |
| Customer App | Frequent / API-based | Customer information can be updated regularly. |

The three ingestion paths converge into a common **Raw / Landing Area**, followed by validation and change handling before trusted data reaches the central platform.

## 5. Proposed Ingestion Flow

![UrbanBasket Data Ingestion Architecture](architecture/urbanbasket-ingestion-flow.png)

**High-level flow:** Sources → Ingestion → Raw/Landing → Validation → Change Handling → Central Data Platform → Business/Analytics

## 6. Handling Data Problems

### Late-arriving data
Use the relevant **business/event date** together with the ingestion timestamp so late information can be associated with the correct business period.

### Incomplete or invalid data
Validate required fields, data types, formats, and relevant business rules. Invalid or incomplete records go to **Quarantine / Review** and can be corrected and reprocessed.

### Duplicate data
Use a unique business key, record identifier, or event ID to identify duplicates. A duplicate should not create another write to the trusted data.

### Corrected data
Use change detection and an **upsert** approach:
- Existing record → update.
- New record → insert.

### Unchanged data
Use **incremental processing** so only new or changed information is processed. Unchanged information is skipped.

## 7. Why This Architecture?
1. Different sources have different freshness requirements.
2. The Raw/Landing area preserves incoming information and supports reprocessing.
3. Validation protects the trusted platform from incomplete or invalid data.
4. Change handling supports corrected information.
5. Incremental processing reduces unnecessary work.
6. Monitoring helps identify failures and data-quality issues.

## 8. Expected Outcome
- A single central view of information.
- Appropriate ingestion for each source.
- Better handling of late and incomplete data.
- Controlled duplicate and correction handling.
- Reduced unnecessary processing.
- Trusted data for business and analytics.

## 9. Conclusion
Our proposed ingestion flow provides UrbanBasket with a simple and flexible way to bring data from stores, delivery teams, and the customer application into a central platform. By combining **batch, real-time, and frequent ingestion** with **validation, change handling, and incremental processing**, the design addresses the key challenges in the case study while keeping the overall architecture simple and manageable.
