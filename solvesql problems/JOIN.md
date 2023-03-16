### [쇼핑몰의 일일 매출액](https://solvesql.com/problems/olist-daily-revenue/)
```sql
SELECT
  DATE(order_purchase_timestamp) AS dt,
  ROUND(SUM(payment_value),2) AS revenue_daily
FROM olist_orders_dataset
JOIN olist_order_payments_dataset
ON olist_orders_dataset.order_id = olist_order_payments_dataset.order_id
WHERE DATE(order_purchase_timestamp) >= '2018-01-01'
GROUP BY DATE(order_purchase_timestamp)
ORDER BY DATE(order_purchase_timestamp);
```

### [쇼핑몰의 일일 매출액과 ARPPU](https://solvesql.com/problems/daily-arppu/)
```sql
SELECT
  DATE(order_purchase_timestamp) AS dt,
  COUNT(DISTINCT(customer_id)) AS pu,
  ROUND(SUM(payment_value),2) AS revenue_daily,
  ROUND(SUM(payment_value)/COUNT(DISTINCT(customer_id)),2) AS arppu
FROM olist_orders_dataset
JOIN olist_order_payments_dataset
ON olist_orders_dataset.order_id = olist_order_payments_dataset.order_id
WHERE DATE(order_purchase_timestamp) >= '2018-01-01'
GROUP BY DATE(order_purchase_timestamp)
ORDER BY DATE(order_purchase_timestamp);
```

### [멘토링 짝꿍 리스트](https://solvesql.com/problems/mentor-mentee-list/)
```sql
--푸는 중
SELECT
mentee.employee_id AS mentee_id,
mentee.name AS mentee_name,
employees.employee_id AS mentor_id,
employees.name AS mentor_name

FROM (
  SELECT employee_id, name, join_date, department
  FROM employees
  WHERE join_date >= DATE('2021-12-31', '-3 months')
  ORDER BY employee_id
  ) AS mentee
JOIN employees ON employees.department != mentee.department
WHERE employees.join_date <= DATE('2021-12-31', '-2 years')
AND mentee.department != employees.department
ORDER BY employees.employee_id;
```

### [작품이 없는 작가 찾기](https://solvesql.com/problems/artists-without-artworks/)
```sql
SELECT 
artists.artist_id AS artist_id,
artists.name AS name
FROM artists
LEFT JOIN artworks_artists ON artists.artist_id = artworks_artists.artist_id
WHERE death_year IS NOT NULL AND artwork_id IS NULL;
```
