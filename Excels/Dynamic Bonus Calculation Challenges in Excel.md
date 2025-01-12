# Problem 
I tackled real-world scenarios involving calculating dynamic bonuses for salespersons based on sales, performance ratings, and tenure. 
Each problem progressively added complexity.

## Solutions
1. Dynamic Bonus Based on Sales Thresholds
- Scenario: Bonuses vary based on sales thresholds:
  - No bonus for sales below $10,000.
  - A percentage bonus for sales between $10,000 and $20,000 = 5%.
  - A higher percentage bonus for sales above $20,000 = 10%, with an additional flat bonus for exceeding $25,000 = +500.
- Solution:

```
=IF(B2<10000, 0, 
   IF(B2<=20000, B2 * 5%, 
      B2 * 10% + IF(B2>25000, 500, 0)
   )
)
```
2. Capping the Bonus
- Scenario: To ensure fairness, introduce a maximum cap of $5,000 for bonuses.
- Solution:
```
=MIN(5000, 
   IF(B2<10000, 0, 
      IF(B2<=20000, B2 * 5%, 
         B2 * 10% + IF(B2>25000, 500, 0)
      )))

```
3. Dynamic Bonus Based on Sales Thresholds & Performance Ratings
- Scenario: Bonuses vary based on sales thresholds % Performance ratings:
  - Double bonus Excellent 
  - Same Bouns for good
  - Half the bouns for Average
- Solutions:
```
=IF(B2<10000,0,
IF(B2<20000,
B2 * (IF(D2="Excellent", 10% , IF(D2="Good", 5%, 2.5%))),
B2 * (IF(D2="Excellent", 20% , IF(D2="Good", 10%, 5%))) + IF(B2 >25000,500,0)))
```
4. Tiered Bonus Cap Based on Performance Rating
- Scenario: Adjust the cap dynamically:
   - $6,000 for "Excellent."
   - $5,000 for "Good."
   - $3,000 for "Average."
- Solution:
```
=MIN(
   IF(C2="Excellent", 6000, IF(C2="Good", 5000, 3000)),
   IF(B2<10000, 0, 
      IF(B2<=20000, B2 * (IF(C2="Excellent", 10%, IF(C2="Good", 5%, 2.5%))), 
         B2 * (IF(C2="Excellent", 20%, IF(C2="Good", 10%, 5%))) + IF(B2>25000, 500, 0)
      )))
  ```
5. Tenure-Based Bonus Cap Adjustment
- Scenario: Employees with 5+ years of tenure can exceed their bonus cap by $1,000.
- Solution:
```
=MIN(
   IF(C2="Excellent", 6000 + IF(D2>=5, 1000, 0), 
      IF(C2="Good", 5000 + IF(D2>=5, 1000, 0), 
         3000 + IF(D2>=5, 1000, 0)
      )
   ),
   IF(B2<10000, 0, 
      IF(B2<=20000, B2 * (IF(C2="Excellent", 10%, IF(C2="Good", 5%, 2.5%))), 
         B2 * (IF(C2="Excellent", 20%, IF(C2="Good", 10%, 5%))) + IF(B2>25000, 500, 0)
      )))
```
