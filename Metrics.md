## Calculated Fields 
### Total Sales
- Order Date (Year)
```
YEAR([Order Date])
```
- Parameter to select year
  - Data Type: Integer
  - Current value: Recent year from the data source
  - Add values from Order Date (Year) - The calculated Field
  - List to display all years
  - Display Format: Remove Thousand separators and decimals
- Current Year Sales
```
IF YEAR([Order Date]) = [Select Year] THEN [Sales] END
```
- Previous Year Sales
```
IF YEAR([Order Date]) = [Select Year] - 1 THEN [Sales] END
```
- % Difference Sales
```
(SUM([CY Sales]) - SUM([PY Sales]))/SUM([PY Sales])
```

Change to percent -> Right-click on the calculated field -> Default Properties -> Number Format -> Percentage -> Remove Decimals -> OK

Format the % Diff Sales -> Right-click -> Format -> ▲0.00%; ▼-0.00%;

- Min/Max Sales
```
IF SUM([CY Sales]) = WINDOW_MAX(SUM([CY Sales]))
THEN SUM([CY Sales])
ELSEIF SUM([CY Sales]) = WINDOW_MIN(SUM([CY Sales]))
THEN SUM([CY Sales])
END
```

Under All in the Marks pane: Change the SUM([CY Sales]) to {SUM([CY Sales])} and [% Diff Sales] to {[% Diff Sales]} to return from revenue range to total revenue for the selected year

- Current Year
```
[Select Year]
```
- Previous Year
```
[Select Year] - 1
```

Convert both to dimension

Tooltip
```
Sales of <MONTH(Order Date)>, <ATTR(Current Year)>: <SUM(CY Sales)>
Sales of <MONTH(Order Date)>, <ATTR(Previous Year)>: <SUM(PY Sales)>
Sales Differences: <AGG(% Diff Sales)>
Highest/Lowest Sales: <AGG(Min/Max Sales)>
```

### Total Profit
- Current Year Profit
```
IF YEAR([Order Date]) = [Select Year] THEN [Profit] END
```
- Previous Year Profit
```
IF YEAR([Order Date]) = [Select Year] - 1 THEN [Profit] END
```