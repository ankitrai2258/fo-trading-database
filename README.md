# fo-trading-database
# Futures & Options Trading Database Design

## Overview

This project designs and implements a relational database for storing and analyzing high-volume Futures & Options (F&O) trading data from Indian exchanges such as NSE, BSE, and MCX. The dataset used is the **NSE Future and Options Dataset (3M)** from Kaggle containing over **2.5 million records**.

The objective is to build a scalable schema capable of supporting time-series analytics and cross-exchange derivatives analysis.

# Database Design

The schema follows **Third Normal Form (3NF)** to remove redundancy and improve consistency.

Entities used:

1. Exchanges
2. Instruments
3. Contracts
4. Trades

### Relationships

Exchange → Instruments → Contracts → Trades

This hierarchical design allows efficient storage of contract metadata while keeping the high-volume trade data separate.

---

# Why Normalization (3NF)?

Normalization was chosen to:

• eliminate redundant contract metadata
• reduce storage footprint for large datasets
• maintain referential integrity
• support scalable ingestion pipelines

For example, contract attributes such as:

* expiry date
* strike price
* option type

are stored once in the **contracts table** rather than repeating in millions of trade records.

# Why Star Schema Was Avoided

A star schema is typically used for **analytical data warehouses**.
However this dataset is **transactional time-series market data**, where:

• joins are predictable and hierarchical
• ingestion speed is critical
• updates occur frequently

Using normalized tables provides better **write performance and data integrity**.


# Scalability for High-Frequency Trading (HFT)

To support **10M+ rows** of trading data:

• Indexing on timestamp, symbol, and exchange
• Partitioning of trades table by timestamp
• BRIN indexes for large time-series tables
• Window functions for efficient analytics

These optimizations allow the database to efficiently support trading analytics queries.

# Dataset

Kaggle Dataset:

NSE Futures and Options Dataset (3M)

Contains:

• symbol
• instrument type
• expiry date
• strike price
• option type
• open/high/low/close prices
• settlement price
• open interest
• trading timestamp

---

# Technologies Used

• PostgreSQL
• Python (Pandas)
• Jupyter Notebook
• SQL Window Functions
• GitHub

# Repository Contents

| Folder         | Description                                     |
| -------------- | ----------------------------------------------- |
| er_diagram     | ER diagram of the schema                        |
| sql            | Table creation, indexing, and partition scripts |
| queries        | Advanced SQL analytics queries                  |
| data_loader    | Notebook to load Kaggle dataset                 |
| sample_outputs | Sample query results                            |

# Example Analytics Queries

• Top symbols by open interest change
• 7-day rolling volatility for NIFTY options
• Cross-exchange futures comparison
• Option chain summary by strike and expiry
• Highest trading volume in last 30 days

# Author

Ankit Rai
