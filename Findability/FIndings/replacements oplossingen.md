---
created: 2025-11-27T15:39
updated: 2025-11-27T16:35
tags:
  - findability/findings
---
![[Scherm­afbeelding 2025-11-27 om 15.40.38.png]]
```sql
WITH base AS (
SELECT
order_date,
customer_cd,
product_cd,
SUM(turnover_euro) AS turnover
FROM `kramp-edw-e-commerce-prd.presentation_common.pres__fct__date_customer_product_sales`
WHERE order_date >= '2024-11-25'
AND outlier IS NOT TRUE
GROUP BY ALL
),

repurchase as (
SELECT
order_date,
customer_cd,
product_cd,
turnover,
CASE
	WHEN order_date > FIRST_VALUE(order_date) OVER (
		PARTITION BY customer_cd, product_cd
		ORDER BY order_date
		ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
	)
	THEN TRUE
	ELSE FALSE
END AS is_repurchase
FROM base
ORDER BY customer_cd, product_cd, order_date
)

select order_date,
sum(case when is_repurchase is true then 1 else 0 end)/count(*) as repurchase_rate,
sum(case when is_repurchase is true then turnover else 0 end)/sum(turnover) as repurchase_turnover_rate
from repurchase
group by order_date
order by order_date
```
