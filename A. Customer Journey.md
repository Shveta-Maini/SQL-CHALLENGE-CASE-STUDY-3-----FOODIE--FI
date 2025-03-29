

# A. Customer Journey 🚀

*--Q1 Based off the 8 sample customers provided in the sample from the subscriptions table, write a brief description about each customer’s onboarding journey.*


<img width="261" alt="image" src="https://github.com/yaswanthteja/SQL_Dannys_Foodiee-Fi_CaseStudy3/blob/master/images/A.Customer%20journey/Img1.png">


## SQL QUERY:

```sql
select s.customer_id,p.plan_id,p.plan_name,s.start_date
from plans p
inner join subscriptions s 
on p.plan_id=s.plan_id
where s. customer_id in (1,2,11,13,15,16,18,19); -- selected 8 unique customers;
```

## ANSWER:

![Picture1](https://github.com/user-attachments/assets/8442c1db-6918-4ccb-a5dc-a6e1ecea5ec7)


## Brief description on the customers journey based on the results from the above query:

Customer 1 starts with a free trial plan on 2020-08-01 and when the trial ends, upgrades to basic monthly plan on 2020-08-08

Customer 2 starts with a free trial plan on 2020-09-20 and when the trial ends, upgrades to pro annual plan on 2020-09-27

Customer 13 starts with free trial plan on 2020-15-12 and when the trial ends subscribes to a basic monthly plan on the
2020-12-22, and 3 months later upgrades to a pro monthly plan on 2021-03-29




