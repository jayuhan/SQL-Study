### [우리 플랫폼에 정착한 판매자 1](https://solvesql.com/problems/settled-sellers-1/)
```sql
SELECT seller_id, COUNT(DISTINCT(order_id)) AS orders
FROM olist_order_items_dataset
GROUP BY seller_id
HAVING 100<= orders;
```

### [최고의 근무일을 찾아라](https://solvesql.com/problems/best-working-day/)
```sql
SELECT day, SUM(tip) AS tip_daily
FROM tips
GROUP BY day
ORDER BY tip_daily DESC
limit 1;
```

### [할부는 몇 개월로 해드릴까요](https://solvesql.com/problems/installment-month/)
```sql
SELECT
  payment_installments,
  COUNT(DISTINCT (order_id)) AS order_count,
  MIN(payment_value) AS min_value,
  MAX(payment_value) AS max_value,
  AVG(payment_value) AS avg_value
FROM
  olist_order_payments_dataset
WHERE
  payment_type = 'credit_card'
GROUP BY
  payment_installments;
```

### [일별 블로그 방문자 수 집계](https://solvesql.com/problems/blog-counter/)
```sql
SELECT event_date_kst AS dt, COUNT(DISTINCT(user_pseudo_id)) AS users
FROM ga
WHERE dt BETWEEN '2021-08-02' AND '2021-08-09'
GROUP BY event_date_kst
HAVING COUNT(key) > 0
ORDER BY event_date_kst ASC;
```

### [버뮤다 삼각지대에 들어가버린 택배](https://solvesql.com/problems/shipment-in-bermuda/)
```sql
-- 푸는중
SELECT
  DATE(order_delivered_carrier_date) AS delivered_carrier_date,
  COUNT(*) AS orders
FROM olist_orders_dataset
WHERE order_delivered_carrier_date BETWEEN '2017-01-01' AND '2017-01-31'
  AND order_delivered_customer_date IS NULL
GROUP BY DATE(order_delivered_carrier_date)
ORDER BY DATE(order_delivered_carrier_date) ASC;
```

### [점검이 필요한 자전거 찾기](https://solvesql.com/problems/inspection-needed-bike/)
```sql
SELECT bike_id
FROM rental_history
WHERE DATE(rent_at) BETWEEN '2021-01-01' AND '2021-01-31'
GROUP BY bike_id
HAVING SUM(distance) >= 50000;
```
