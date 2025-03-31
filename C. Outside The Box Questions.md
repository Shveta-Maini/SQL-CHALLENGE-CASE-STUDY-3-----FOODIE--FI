# <p align="center" style="margin-top: 0px;">🥑 Case Study #3 - Foodie-Fi 🥑

## <p align="center"> 🎞 Solution- C. Outside The Box Questions🚀

### *--Q1 How would you calculate the rate of growth for Foodie-Fi?

- The rate of growth for Foodie- Fi can be claculated in two ways:-

   **(1.) Month Over Month (MoM) Revenue Growth %** 

### SQL QUERY:

```sql
with monthly_revenue as
(
    select 
        format(s.start_date, 'yyyy-MM') as month_year, 
        sum(p.price) as total_revenue
    from subscriptions s
    join plans p on s.plan_id = p.plan_id
    where s.plan_id != 0  
    and s.start_date between '2020-01-01' and '2021-04-30'
    group by format(s.start_date, 'yyyy-MM')
),
previous_month_revenue as
(
   select 
        month_year,
        total_revenue,
        lag(total_revenue)over (order by month_year)as previous_month_revenue
        from monthly_revenue
),
revenue_growth as
(
    select 
        month_year,
        total_revenue,
        previous_month_revenue,
        cast(round((total_revenue - previous_month_revenue) * 100.0 /nullif(previous_month_revenue, 0), 2)as decimal(10,2))
        as revenue_growth_percentage
    from previous_month_revenue 
)
select * from revenue_growth;

```

### ANSWER:

![Picture1](https://github.com/user-attachments/assets/b5c0995c-89d8-445a-985b-abc2e3d3b0c8)

   **(2.) Total Revenue Growth %** 

### SQL QUERY:

```sql
with monthly_revenue as
(
   select
        format(s.start_date, 'yyyy-MM') as month_year, 
        sum(p.price) as total_revenue
    from subscriptions s
    join plans p on s.plan_id = p.plan_id
    where s.plan_id != 0  
    and s.start_date between '2020-01-01' and '2021-04-30'
    group by format(s.start_date, 'yyyy-MM')
),
first_last_revenue as
(
    select 
        max(case when month_year = '2020-01' then total_revenue end) as first_month_revenue,
        max(case when month_year = '2021-04' then total_revenue end) as last_month_revenue
    from monthly_revenue
)
select 
    first_month_revenue,
    last_month_revenue,
    cast(round((last_month_revenue - first_month_revenue) * 100.0 / nullif(first_month_revenue, 0), 2) as decimal(10,2)) 
    as total_revenue_growth_percentage
from first_last_revenue;
```

### ANSWER:

![Picture2](https://github.com/user-attachments/assets/a2e5013c-f34d-4dd5-baa1-c8728de74090)
