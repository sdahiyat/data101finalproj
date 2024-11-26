# queries

Use this as a recommended location to put any SQL (or other) queries.

SELECT city, COUNT(*) AS total_reviews
FROM businesses b
JOIN reviews r ON b.business_id = r.business_id
WHERE b.categories ILIKE '%Restaurant%'
GROUP BY city
ORDER BY total_reviews DESC
LIMIT 10;