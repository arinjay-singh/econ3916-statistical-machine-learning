# The Cost of Living Crisis: A Data-Driven Analysis

### Customizing Inflation Metrics for the Modern Student

## 1. The Problem: The "Average" Fallacy

Official government metrics, such as the Consumer Price Index (CPI), are built to reflect the "average" American household. However, as a 21-year-old student living in Boston, my "average" is fundamentally different. While the national index includes costs like new car prices or medical care, a student's budget is hyper-concentrated in **Tuition, Rent, and Food**.

When the price of groceries or a month of rent doubles, it doesn't matter if the national inflation rate is only 3%—my personal reality is far more expensive. This project was born from a simple question: **How much has the "Student Cost of Living" actually diverged from the official narrative since I started school in 2016?**

---

## 2. Methodology

To answer this, I built a custom economic model using a professional data science pipeline:

* **Real-Time Data Sourcing:** I utilized the `fredapi` to extract eight distinct economic series directly from the Federal Reserve (FRED) database, including regional data specifically for the **Boston-Cambridge-Newton** area.
* **The Laspeyres Index:** In economics, a Laspeyres Index measures the change in the cost of a fixed "basket" of goods. I defined a custom "Student Basket" with the following weights to reflect a realistic budget:
* **Tuition:** 40%
* **Rent:** 25%
* **Food/Groceries:** 17%
* **Transportation/Utilities/Misc:** 18%


* **Normalization (The 100-Base Rule):** Raw data is messy—Tuition is measured in thousands, while a burrito is measured in dollars. I re-indexed every data point so that **January 1, 2016 = 100**. This creates a "level playing field" where we can see the exact percentage growth of every item side-by-side.

---

## 3. Key Findings

### **A. The "Sticker Shock" of Essentials**

My analysis reveals that the primary drivers of the student crisis are **Rent and Utilities**, both of which have surged nearly **50%** since 2016. While items like clothing remained relatively flat, the "non-negotiables" of student life (housing and power) showed an almost vertical trajectory starting in 2021.

### **B. The Inflation Gap: Official vs. Reality**

The most striking discovery was the divergence between the **National CPI** and my **Student SPI (Student Price Index)**:

* **National CPI:** Climbed to ~137, representing a 37% total increase.
* **Student SPI:** Reached ~133.
* **The Insight:** While the *percentage growth* of the student basket was slightly lower than the national average, the **"Inflation Gap"** (visualized in red in my charts) shows that student costs are "stickier". Students don't see the relief of falling gas prices or used car auctions; our biggest costs (Tuition/Rent) almost never go down, creating a permanent high-cost floor.

### **C. The "Boston Premium"**

By layering in the **Boston-specific CPI**, the data confirms a regional disparity. Living in Boston adds a significant "tax" on top of national inflation, consistently keeping the local cost of living higher than the national average throughout the last decade.

---

## 4. Conclusion: The Real-World Impact

This project demonstrates that inflation is not a single number—it is a personal experience. By the end of 2025, my analysis shows that a student needs roughly **$1.33** to buy what **$1.00** bought when they started in 2016. For a recruiter or hiring manager, this project showcases my ability to:

1. Identify a complex problem.
2. Acquire and clean "noisy" real-world data via APIs.
3. Apply economic theory to generate actionable, visual insights.
