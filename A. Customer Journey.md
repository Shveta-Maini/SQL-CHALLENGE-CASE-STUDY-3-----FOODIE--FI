

# A. Customer Journey 🚀



## SQL Code - Step 1: Identifying Customer Plans  
```sql
SELECT customer_id, plan_id, start_date  
FROM subscriptions  
WHERE plan_id IN (0, 1, 2, 3, 4); 





