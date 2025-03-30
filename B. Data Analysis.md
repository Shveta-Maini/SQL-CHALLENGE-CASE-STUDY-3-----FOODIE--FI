# <p align="center" style="margin-top: 0px;">🥑 Case Study #3 - Foodie-Fi 🥑

## <p align="center"> 🎞 Solution- B. Data Analysis Questions🚀

### *--Q1 How many customers has Foodie-Fi ever had?*

### SQL QUERY:

```sql
select count( distinct customer_id) as unique_customers
from subscriptions;
```

### ANSWER:

![Picture1](https://github.com/user-attachments/assets/63f47bbd-ff64-4618-9ff8-017aa7a66282)

- Foodie-Fi has 1,000 unique customers

### *--Q2 What is the monthly distribution of trial plan start_date values for our dataset - use the start of the month as the group by value*

### SQL QUERY:

```sql
select
      datepart(month,start_date)as month_date,
      datename(month,start_date) as month_name,
      count(*) as customers_count
from subscriptions s
inner join plans p
  on s.plan_id = p.plan_id
where s.plan_id = 0
group by datepart(month,start_date),
         datename(month,start_date)  
order by month_date;
```

### ANSWER:

![Picture2](https://github.com/user-attachments/assets/323a4f8d-3348-4c8f-94ce-ecd5b85da057)

- March has the highest number of trial plans, whereas february has the lowest number of trial plans.

### *--Q3 What plan start_date values occur after the year 2020 for our dataset? Show the breakdown by count of events for each plan_name*

### SQL QUERY:

```sql
select 
  p.plan_id, 
  p.plan_name, 
  count(
    case when year(s.start_date) = 2020 then 1 end
        ) as event_2020, 
  count(
    case when s.start_date >= '2021-01-01' then 1 end
       ) as event_2021 
from 
  plans p 
  inner join subscriptions s
  on p.plan_id = s.plan_id 
group by 
  p.plan_id, 
  p.plan_name 
order by 
  plan_id;
```

### ANSWER:

![Picture3](https://github.com/user-attachments/assets/f8206f1d-be5e-4547-8007-f7a2a99f3cb1)

- Trial plan was highly used in 2020 but disappeared in 2021.
- Basic monthly declined while pro monthly and pro annual plan grew in 2021.

### *--Q4 What is the customer count and percentage of customers who have churned rounded to 1 decimal place?*

### SQL QUERY:

```sql
select 
       count(*) as churn_count,
       round(
	     (cast(count(*) as float)) / (select count (distinct customer_id) from subscriptions) * 100,1)
       as churn_percentage
from 
  subscriptions 
where 
  plan_id = 4;
```

### ANSWER:

![Picture4](https://github.com/user-attachments/assets/b50a645d-a943-4606-ba11-84699315419e)

- There are 307 customers who have churned, which is 30.7% of Foodie- Fi customer base.

### *--Q5 How many customers have churned straight after their initial free trial - what percentage is this rounded to the nearest whole number?*

### SQL QUERY:

```sql
with ranking as
(
  select
         s.customer_id,
         s.plan_id,
         p.plan_name,
         row_number()over(partition by s.customer_id order by s.start_date)as plan_rank 
  from subscriptions s
  join plans p
  on s.plan_id = p.plan_id
)
 select
        count(*) as churn_count,
        round(count(*) * 100 / (select count(distinct customer_id) from subscriptions), 0) as percentage_churn
  from ranking
  where plan_id = 4
        and plan_rank = 2; 
```

### ANSWER:

![Picture5](https://github.com/user-attachments/assets/268a4c8b-2ef3-4cb4-a3ae-8985078024c6)

- There are 92 customers who churned straight after the initial free trial which is 9% of entire customer base of foodie-fi.

### *--Q6 What is the number and percentage of customer plans after their initial free trial?*

### SQL QUERY:

```sql
With customer_transitions as
(
  select customer_id,
	     plan_id, 
	     lead(plan_id) over(partition by customer_id order by start_date) as next_plan
         from subscriptions 
)
select  p.plan_name,
        count(*) as customer_count, 
        round(cast(count(*) as float) / (select count(distinct customer_id) from subscriptions)* 100, 1) as percentage_customer
from customer_transitions ct
left join plans p 
on p.plan_id= ct.next_plan
where ct.plan_id = 0 and ct.next_plan is not null
group by p.plan_name
order by p.plan_name; 
```

### ANSWER:

!![Picture6](https://github.com/user-attachments/assets/e28c72b9-1500-4420-91b8-a01fe8533064)


- More than 80% of customers are on paid plans with small 3.7% on pro annual plan.

### *--Q7 What is the customer count and percentage breakdown of all 5 plan_name values at 2020-12-31?*

### SQL QUERY:

```sql
with last_active_plan as
 (
    select customer_id, 
           plan_id, 
           lead(start_date) over(partition by customer_id order by start_date) as next_date
    from subscriptions
    where start_date <= '2020-12-31'
),
plan_summary as
(
    select plan_id,
           count(distinct customer_id) as customer_count,  
           round(cast(count(distinct customer_id)as float) * 100.0 / (select count(distinct customer_id) from subscriptions 
           where start_date <= '2020-12-31'), 1) as percentage_customer 
    from last_active_plan
    where next_date is null  
    group by plan_id
)
select 
    p.plan_name,  
    ps.customer_count,  
    ps.percentage_customer
from plan_summary ps
left join plans p 
on ps.plan_id = p.plan_id
order by ps.plan_id;
```

### ANSWER:

![Picture7](https://github.com/user-attachments/assets/6b6770af-dab8-4c76-ac66-07bfe1ac8364)

- On 31st Dec 2020, more people subscribed or upgraded to the pro monthly plan, but fewer plan signed up for the trial plan.

### *--Q8 How many customers have upgraded to an annual plan in 2020?*

### SQL QUERY:

```sql
select
       count(distinct customer_id) as unique_customers
from subscriptions
where plan_id=3
      and start_date <='2020-12-31'
```

### ANSWER:

![Picture8](https://github.com/user-attachments/assets/1d6bdc83-4a44-4bac-853d-c39509141efb)

- 195 customers upgraded to an annual plan in 2020.

 ### *--Q9 How many days on average does it take for a customer to an annual plan from the day they join Foodie-Fi?*

### SQL QUERY:

```sql
with customer_joining as
(
    select customer_id, 
           start_date as join_date
    from subscriptions
    where plan_id = 0  
),
annual_plan as 
(
    select customer_id, 
           start_date as annual_date
    from subscriptions
    where plan_id = 3  
)
select
      round(avg(datediff(day, join_date, annual_date)), 0) as avg_days_to_annual_upgrade
from customer_joining cj
join annual_plan ap
on cj.customer_id = ap.customer_id;
```

### ANSWER:

![Picture9](https://github.com/user-attachments/assets/e784e00c-5ab6-4b6e-9aab-bdc5a03810c3)

- On average it takes 104 days for customers to upgrade to an annual plan afer they join Foodie- Fi.

### *--Q10 Can you further breakdown this average value into 30 day periods (i.e.31-60 days etc)?*

### SQL QUERY:

```sql
with customer_joining as 
(
    select customer_id, 
           start_date as join_date
    from subscriptions
    where plan_id = 0  
),
annual_plan as 
(
    select customer_id, 
           start_date as annual_date
    from subscriptions
    where plan_id = 3  
),
day_period as 
(
    select 
        cj.customer_id,
        datediff(day, cj.join_date, ap.annual_date) as diff
    from customer_joining cj
    left join annual_plan ap 
    on cj.customer_id = ap.customer_id
    where ap.annual_date is not null
),
bins as 
(
    select diff, 
           floor(diff/ 30) as bins
    from day_period
)
select 
    concat((bins * 30)+1,' - ', (bins + 1) * 30,' days') as days_range,
    count(diff) as total_customers,
    round(avg(diff), 0) as avg_days_to_annual_upgrade
from bins
group by bins
order by bins;
```

### ANSWER:

![Picture10](https://github.com/user-attachments/assets/64265e7a-96f3-4dc5-aa47-2a99d9406db1)

- The majority of customers opt to subscribe or upgrade to an annual plan within the first 30 days.
- After 270 days, there is almost no customer activity in terms of purchasing a plan.

### *--Q11  How many customers downgraded from a pro monthly to a basic monthly plan in 2020?*

### SQL QUERY:

```sql
With plan_moves as 
(
  select customer_id,
         plan_id,
         start_date,
         lead(plan_id)over(partition by customer_id order by start_date) as next_plan
         from subscriptions
)
select count(*) as downgraded
from plan_moves
where start_date <= '2020-12-31'
and plan_id = 2 and next_plan = 1;
```

### ANSWER:

![Picture11](https://github.com/user-attachments/assets/0eab8190-5238-4aa3-9603-be45e4fa4581)

- No customer has downgraded from pro monthly to basic monthly in 2020
