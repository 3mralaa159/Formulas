# **Project Overview**

In retail business data, sales reports often contain **region abbreviations** instead of full names. This inconsistency can lead to **misinterpretation** in reporting, dashboards, and analytics.

This project demonstrates how to **automate bulk replacements** in Excel using the `REDUCE` and `SUBSTITUTE` functions. The approach ensures consistent, readable, and accurate sales reports without manual intervention.

---

## **Problem Statement**

Retail businesses often receive sales data where region names are abbreviated, such as:

|**Region Code**|**Sales**|
|---|---|
|NY|$10,000|
|CA|$15,000|
|TX|$7,500|
|FL|$9,200|

However, for better reporting and visualization, **full region names** are required:


|**Region Name**|**Sales**|
|---|---|
|New York|$10,000|
|California|$15,000|
|Texas|$7,500|
|Florida|$9,200|


Instead of manually replacing values, we use an **automated formula-based approach** in Excel.

---

## **Solution Approach**

We utilize **Excel’s dynamic array functions (`REDUCE` & `SUBSTITUTE`) to replace abbreviations with their full region names based on a reference lookup table.

**Find & Replace Mapping Table:**


| **Find (Abbreviation)** | **Replace (Full Name)** |
| ----------------------- | ----------------------- |
| NY                      | New York                |
| CA                      | California              |
| TX                      | Texas                   |
| FL                      | Florida                 |



Formula: 

```Excel 
=REDUCE(A2:A100,$F$2:$F$5,LAMBDA(a,b,SUBSTITUTE(a,b,OFFSET(b,0,1))))
```
### **How the Formula Works:**

1. `REDUCE` Function: Iterates through the list of abbreviations dynamically.
2. `SUBSTITUTE` Function: Replaces the abbreviation with the correct full region name.
3. `Offset` Function: Maps the replacement values correctly from the lookup table.
4. `LAMBDA ' Function: Wraps everything in a reusable formula.
