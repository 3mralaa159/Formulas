## Problem: 
- Identifying Top-Selling Products by Category
## Scenario:
- You manage a retail store and want to identify the top-selling product in each category based on total sales. Your sales data includes the following columns:
  - Product Name
  - Category
  - Quantity Sold
  - Price per Unit
 
## Solution
- **Calculate Total Sales**:
    - Add a column for **Total Sales** using the formula:
 
        ```
      =Quantity Sold * Price per Unit
        ```
      
- **Find the Top-Selling Product in Each Category**:
    - Use the **MAXIFS** formula to find the maximum sales for each category.  
        Formula:
      
        ```
      =MAXIFS(Total Sales, Category, "Category Name")
        ```
      
- **Identify the Top Product**:
    - Use the **INDEX-MATCH** combination to return the product name corresponding to the maximum sales:

      ```
      =INDEX(Product Name Range, MATCH(MAXIFS(Total Sales, Category, "Category Name"), Sales, 0))
      ```

