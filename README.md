# 🥑 SQL Case Study: Foodie-Fi 🥑

## 📌 **About This Repository**  

This repository hosts the solutions to the **3rd challenge (Week 3)** of the **8 Weeks SQL Challenge** by Danny Ma.

[📌 View the Full Challenge Here](https://8weeksqlchallenge.com/case-study-3/)

## 🚀 Contribute & Support   

🍴 Fork this repository, make improvements, and submit a Pull Request!  

⭐ Found this project useful? Don’t forget to give it a star! 🌟  

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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

## 📊 Case Study Solutions

Part A. Customer Journey - [View Solution](https://github.com/ShvetaMaini/SQL-CHALLENGE-CASE-STUDY-3-----FOODIE--FI/blob/main/A.%20Customer%20Journey.md)

Part B - Data Analysis Questions

Part C -  Outside the Box Questions

## 🔑 Key Insights 

**📈 Key Metrics:**

✔️ Month-over-Month (MoM) Revenue Growth %

✔️ Total Revenue Growth % (112% increase from Jan 2020 to Apr 2021)

**👥 Customer Breakdown:**

👤**Total Unique Customers**: 1000 (Trial Visitors)

✅ **Active Subscribers**: 1343

📌 **Plan-wise Subscriptions**:

🟢 **Basic Monthly**: 546 subscribers ($9.90/month)

🔵 **Pro Monthly**: 539 subscribers ($19.90/month)

🟠 **Pro Annual**: 258 subscribers ($199/year)

❌ **Churned Customers**: 307 (after trial)

💰 **Revenue Insights:**

📉** Fluctuations observed** – **drops in Nov 2020, Feb 2021, and Mar 2021**, followed by recovery.

📆 **Peak Revenue**: **$7758.7 in Oct 2020 (holiday influence)**.

🟠 **Pro Annual Plan** is the **highest revenue generator** despite its higher price.

📈 **112% total revenue growth** from **Jan 2020 to Apr 2021.**

## 📢 Recommendations for Growth

Check the attached PDF for detailed recommendations.

## 💬 **Feel free to connect with me!** 🚀 

📧 **Email:** shvetamaini6@gmail.com




