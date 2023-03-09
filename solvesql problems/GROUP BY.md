### 우리 플랫폼에 정착한 판매자 1 (난이도 쉬움) [🔗](https://solvesql.com/problems/settled-sellers-1/)
```sql
SELECT seller_id, COUNT(DISTINCT(order_id)) AS orders
FROM olist_order_items_dataset
GROUP BY seller_id
HAVING 100<= orders
```

### 최고의 근무일을 찾아라 (난이도 쉬움) [🔗](https://solvesql.com/problems/best-working-day/)
```sql
SELECT day, SUM(tip) AS tip_daily
FROM tips
GROUP BY day
ORDER BY tip_daily DESC
limit 1
```

### 할부는 몇 개월로 해드릴까요 (난이도 보통) [🔗](https://solvesql.com/problems/installment-month/)
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
  payment_installments
```

### 일별 블로그 방문자 수 집계 (난이도 보통) [🔗](https://solvesql.com/problems/blog-counter/)
```sql
SELECT event_date_kst AS dt, COUNT(DISTINCT(user_pseudo_id)) AS users
FROM ga
WHERE dt BETWEEN '2021-08-02' AND '2021-08-09'
GROUP BY event_date_kst
HAVING COUNT(key) > 0
ORDER BY event_date_kst ASC
```
