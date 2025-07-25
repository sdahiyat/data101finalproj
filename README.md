# Data 101 Final Project: Database Systems Comparison

## Overview

Please read the full spec on the [Data 101 Website](https://data101.org/fa24/assignments/final-project/)

---

## Repository Structure

The final project contains this starter setup. You may adapt it as needed, but please make sure you don't commit large files which can be complicated to undo.

```
.
├── README.md           # Project documentation
├── 0-checkpoint.md     # Outline of the checkpoint submission
├── 1-final-report.md   # Outline of our final report
├── code/               # Scripts
├── data/               # Data directory 
├── queries/            # SQL queries
```

---

# Analyzing User Reviews and Business Trends with PostgreSQL and MongoDB

**Group Members:**  
Sierra Dahiyat, Sophia Ladyzhensky, Ananya Chawla, Aidana Jakulina

## Project Summary

This project explores the Yelp dataset using two different database paradigms: PostgreSQL (relational) and MongoDB (non-relational). We aimed to compare their performance, usability, and effectiveness in handling analytical queries involving user reviews, business attributes, and city-level trends.

We:
- Sampled and cleaned ~1GB of Yelp data
- Built schemas and collections for PostgreSQL and MongoDB
- Wrote complex analytical queries
- Benchmarked and compared execution performance
- Reflected on practical database design decisions

---

## Key Questions Explored

- What cities have the most active restaurant review scenes?
- Where are restaurants rated most highly?
- Who are the most active users in high-review cities?
- What business category dominates in each city?

---

## Dataset Summary

We downsampled the 10GB Yelp dataset to:
- 10,000 businesses
- 445,853 reviews
- 295,709 users

Extracted from:
- `yelp_academic_dataset_business.json`
- `yelp_academic_dataset_review.json`
- `yelp_academic_dataset_user.json`

Saved as:
- `sampled_businesses.csv`
- `filtered_reviews.csv`
- `filtered_users.csv`

---

## System and Database Setup

### PostgreSQL
- Loaded and normalized data with foreign key constraints
- Used `psycopg` with `executemany()` for bulk inserts
- Defined schema: `businesses`, `users`, and `reviews`
- Used `EXPLAIN ANALYZE` for query optimization

### MongoDB
- Imported CSVs using `pymongo` and `pandas`
- Created collections: `businesses`, `reviews`, and `users`
- Used aggregation pipelines for filtering, grouping, and sorting
- Analyzed performance using `db.command({ explain: ... })`

---

## Example Queries

### SQL: Top Cities by Review Volume
```sql
SELECT city, COUNT(*) AS total_reviews
FROM businesses b
JOIN reviews r ON b.business_id = r.business_id
WHERE b.categories ILIKE '%Restaurant%'
GROUP BY city
ORDER BY total_reviews DESC
LIMIT 10;
```

### MongoDB: Top Cities by Avg Restaurant Rating
```python
pipeline = [
    {"$match": {"categories": {"$regex": "Restaurant", "$options": "i"}}},
    {"$group": {"_id": "$city", "average_rating": {"$avg": "$stars"}, "total_reviews": {"$sum": "$review_count"}}},
    {"$match": {"total_reviews": {"$gte": 100}}},
    {"$sort": {"average_rating": -1}},
    {"$limit": 10}
]
```

---

## Tool Comparison

| Feature          | PostgreSQL                           | MongoDB                             |
|------------------|--------------------------------------|-------------------------------------|
| Schema           | Structured, normalized               | Flexible, semi-structured           |
| Performance      | Better for joins and complex filters | Better for nested/unstructured data |
| Query Language   | SQL + CTEs                           | Aggregation pipeline                |
| Use Case Fit     | Structured analytics                 | Rapid prototyping / No strict schema |
| Setup Difficulty | Higher due to schema constraints     | Easier and more flexible            |

---

## Performance Insights

- PostgreSQL queries benefit from indexing and structured joins.
- MongoDB’s `COLLSCAN` can be fast for small datasets, but indexing would help scalability.
- MongoDB pipelines handle nested structures well (e.g., `$unwind`).
- Indexing the `categories` and `city` fields improves performance in both systems.


---

## Tools Used

- Python, pandas
- PostgreSQL 14.14
- MongoDB 6.0
- psycopg, pymongo
- JupyterHub
- GitHub for version control
