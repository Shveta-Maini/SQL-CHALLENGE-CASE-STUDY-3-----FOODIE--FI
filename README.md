# 🥑 SQL Case Study: Foodie-Fi 🥑

## 👋 Welcome!  

Hello everyone! Excited to share my **SQL project**, where I analyzed **Foodie-Fi**, a streaming service for food-related content 🍕📺

![Picture2](https://github.com/user-attachments/assets/b050bd60-8ad3-4446-8a9b-d9c3ddc60a0c)


## 🎯 Project Overview

**📝 Business Context**: Foodie-Fi offers **monthly & annual subscriptions** for premium cooking content.

**📌 Objective**: CEO **Danny** aims to make **data-driven decisions** to analyze growth & improve business strategies.

## 📊 Data Overview

The analysis utilises two datasets:

**Table 1: plans**

🔹The plans table includes :- plan_id,plan_name, price

🔹It defines plan options and pricing structure

<img width="207" alt="Table1" src="https://github.com/user-attachments/assets/68ab238f-1605-432a-98b7-95dd7e1ceb9c" />

🔹Customers can choose which plans to join Foodie-Fi when they first sign up.

🔹Basic plan customers have limited access and can only stream their videos and is only available monthly at $9.90

🔹Pro plan customers have no watch time limits and are able to download videos for offline viewing. Pro plans start at $19.90 a month or $199 for an annual subscription.

🔹Customers can sign up to an initial 7 day free trial will automatically continue with the pro monthly subscription plan unless they cancel, downgrade to basic or upgrade to an annual pro plan at any point during the trial.

🔹When customers cancel their Foodie-Fi service - they will have a churn plan record with a null price but their plan will continue until the end of the billing period.

**Table 2: subscriptions**

🔹The subscriptions table includes :- customer_id, plan_id , start_date.

🔹It tracks customer actions, upgrades,downgrades, cancellations, and billing periods)

<img width="245" alt="Table2" src="https://github.com/user-attachments/assets/40754f05-a930-4161-af88-9ad3504f1acb" />


🔹Customer subscriptions show the exact date where their specific plan_id starts.

🔹If customers downgrade from a pro plan or cancel their subscription - the higher plan will remain in place until the period is over - the start_date in the subscriptions table will reflect the date that the actual plan changes.

🔹When customers upgrade their account from a basic plan to a pro or annual pro plan - the higher plan will take effect straightaway.

🔹When customers churn - they will keep their access until the end of their current billing period but the start_date will be technically the day they decided to cancel their service.

## Entity Relationship Diagram

![Entity Relationship](https://github.com/user-attachments/assets/b73ebecd-9700-4fb4-9813-99c980df68fa)


## 🎯 SQL Concepts Used

🔹 Basic Queries: SELECT, DISTINCT, WHERE, GROUP BY, ORDER BY

🔹 Aggregations: SUM(), COUNT(), AVG(), MIN(), MAX()

🔹 Functions: CAST(), ROUND(), CASE-WHEN-THEN

🔹 Joins & Subqueries

🔹 CTEs (Common Table Expressions)

🔹 Window Functions: ROW_NUMBER(), OVER(), PARTITION BY, LAG(), LEAD()

## 📊 Case Study Questions

**Part A. Customer Journey** - [View Solution Here](https://github.com/ShvetaMaini/SQL-CHALLENGE-CASE-STUDY-3-----FOODIE--FI/blob/main/A.%20Customer%20Journey.md)

Q-Based off the 8 sample customers provided in the sample from the subscriptions table, write a brief description about each customer’s onboarding journey.

**Part B - Data Analysis Questions**

Q-1 How many customers has Foodie-Fi ever had?

Q-2 What is the monthly distribution of trial plan start_date values for our dataset - use the start of the month as the group by value

Q-3 What plan start_date values occur after the year 2020 for our dataset? Show the breakdown by count of events for each plan_name

Q-4 What is the customer count and percentage of customers who have churned rounded to 1 decimal place?

Q-5 How many customers have churned straight after their initial free trial - what percentage is this rounded to the nearest whole number?

Q-6 What is the number and percentage of customer plans after their initial free trial?

Q-7 What is the customer count and percentage breakdown of all 5 plan_name values at 2020-12-31?

Q-8 How many customers have upgraded to an annual plan in 2020?

Q-9 How many days on average does it take for a customer to an annual plan from the day they join Foodie-Fi?

Q-10 Can you further breakdown this average value into 30 day periods (i.e. 0-30 days, 31-60 days etc)

Q-11 How many customers downgraded from a pro monthly to a basic monthly plan in 2020?

**Part C -  Outside the Box Questions**

## 🚀 Contribute & Support   

🍴 Fork this repository, make improvements, and submit a Pull Request!  

⭐ Found this project useful? Don’t forget to give it a star! 🌟 

## 💬 **Feel free to connect with me!** 🚀 

📧 **Email:** shvetamaini6@gmail.com




