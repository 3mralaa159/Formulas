## **Overview**

This project demonstrates how to efficiently apply bulk find-and-replace transformations in **Power Query (M Language)** using `List.Accumulate`. The method iterates through a mapping table, replacing text values in a specified column of the target dataset. This approach is useful for standardizing inconsistent text entries, such as customer names, product codes, or categories.

## **Problem:**

In data transformation tasks, maintaining **consistent naming conventions** is crucial. A common challenge is handling slight variations in names due to typos, abbreviations, or alternative formats. Manually correcting these inconsistencies is inefficient, especially for large datasets.

**Example Scenario:** We have two tables:
- **Table 1:** Contains sales data with inconsistent customer names.
- **Table 2:** A mapping table specifying the incorrect name variations and their corresponding standardized versions.

## **Solution:**

```
= List.Accumulate(
    {0..List.Count(FindReplace[Find]) - 1}, // Loop over the index of FindReplace table 
    #"Changed Type", // Initial state (original Table 1)
    (state, current) => Table.ReplaceValue( 
        state, // Current table state
        FindReplace[Find]{current}, // The value to find (current row in "Find" column)
        FindReplace[Replace]{current}, // The value to replace (current row in "Replace" column)
        Replacer.ReplaceText, // Replacement mode (replaces text)
        {"Name"} // Column to apply the replacement
    )
)

```

## **How It Works**

1. **List.Accumulate Iteration:**
    - Loops through each row index (`current`) in the `FindReplace` table.
    - Extracts the `Find` value (`FindReplace[Find]{current}`) and `Replace` value (`FindReplace[Replace]{current}`).
    - Applies `Table.ReplaceValue` to update occurrences in the **Name** column.
2. **Dynamic Execution:**
    - Automates replacements without requiring manual function calls for each pair.
    - Scales easily for large datasets.

Example
- **Iteration 1 (Find: "Wicks Ltd", Replace: "Wicks Limited")**
	- No changes because "Wicks Ltd" does **not** exist in Table 1.
- **Iteration 2 (Find: "Wick’s Limited", Replace: "Wicks Limited")**
	- "Wick’s Limited" (row 8) is replaced with "Wicks Limited".
- **Iteration 3 (Find: "Sarah Toote (t/a Epic Designs)", Replace: "Sarah Toote")**
	- No changes because "Sarah Toote (t/a Epic Designs)" does **not** exist in Table 1.
- **Iteration 4 (Find: "Marvin Hillton", Replace: "Magic Marvin")**
	- No changes because "Marvin Hillton" does **not** exist in Table 1 (note: "Marvin Hilton" exists, but it’s not an exact match).


## **Ref**
https://www.youtube.com/watch?v=Wlxx2NSAwZg
https://exceloffthegrid.com/power-query-replace-values-from-list/#Example
