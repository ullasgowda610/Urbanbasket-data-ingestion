# UrbanBasket – Design Decisions

| Decision | Reason |
|---|---|
| Batch ingestion for stores | End-of-day data does not require continuous ingestion. |
| Real-time/streaming for delivery | Delivery events can happen continuously and may need quick availability. |
| Frequent/API-based ingestion for customer app | Customer information can be updated regularly. |
| Raw/Landing area | Preserves incoming information and supports troubleshooting/reprocessing. |
| Validation | Prevents incomplete or invalid information from entering the trusted platform. |
| Deduplication | Prevents the same record/event from being processed repeatedly. |
| Upsert/change handling | Allows corrected information to update an existing record. |
| Business/event date | Helps process late-arriving information against the correct business period. |
| Incremental processing | Processes only new or changed information. |
| Monitoring and alerts | Helps identify failures and data-quality problems. |
| Central data platform | Provides one integrated place for business and analytics use. |

## Key Design Principle
> Choose the ingestion method according to the source's arrival pattern and the business freshness requirement.

## Important Terms
- **Batch:** Data is collected and processed together at scheduled intervals.
- **Real-time/Streaming:** Events are processed continuously or with very low delay.
- **Raw/Landing:** Initial area where incoming source data is preserved.
- **Quarantine:** Area for invalid or incomplete records that need review.
- **Upsert:** Update an existing record or insert it when it does not exist.
- **Incremental Processing:** Process only new or changed data instead of everything.
