Data Migration Task (Cosmos → Azure SQL) — Advanced

Overview
One-time migration tool (Function or Durable Function) to move documents from Cosmos Products container into Azure SQL Products table, flatten nested tags arrays into ProductTags child table, and produce a migration report.

Requirements
Read all documents from Cosmos Products container.
Insert into SQL Products table columns: id, name, price, category.
For tags array, insert rows into ProductTags(productId, tag).
Handle Cosmos pagination (continuation tokens), throttling (429) and use batching for SQL inserts.
Produce migration report: total migrated, failures, time taken.

Architecture
Durable Function (recommended) or simple Function that iterates over Cosmos SDK feed with continuation tokens, writes to SQL with batched prepared statements.
Tech Stack
python + azure-cosmos + pyodbc / SQLAlchemy

Setup
Install:
pip install azure-cosmos pyodbc sqlalchemy

local.settings.json keys:
{
  "Values": {
    "COSMOS_ENDPOINT": "...",
    "COSMOS_KEY": "...",
    "COSMOS_DATABASE": "...",
    "COSMOS_CONTAINER": "Products",
    "SQL_CONNECTION_STRING": "..."
  }
}
Implementation Guidelines
Use Cosmos query_items with maxItemCount and loop using continuation token u
