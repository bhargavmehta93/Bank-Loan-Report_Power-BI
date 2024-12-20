# Bank-Loan-Report_Power-BI

# Used DAX 
1. Date Table = CALENDAR(MIN('financial_loan(1)'[issue_date]),MAX('financial_loan(1)'[issue_date]))
2. Month = FORMAT('Date Table'[Date], "mmm")
3. Month Number = MONTH('Date Table'[Date])
4. Select Measure 2 = {
    ("Total Loan Applications", NAMEOF('financial_loan(1)'[Total Loan Applications]), 0),
    ("Total Amount Received", NAMEOF('financial_loan(1)'[Total Amount Received]), 1),
    ("Total Funded Amount", NAMEOF('financial_loan(1)'[Total Funded Amount]), 2)
}
5. Avg DTI = AVERAGE('financial_loan(1)'[dti])
6. Avg Int Rate = AVERAGE('financial_loan(1)'[int_rate])
7. Bad Loan % = [Bad Loan Applications]/[Total Loan Applications]
8. Bad Loan Applications = CALCULATE([Total Loan Applications],'financial_loan(1)'[Good vs Bad Loan] = "Bad Loan")
9. Bad Loan Funded Amount = CALCULATE([Total Funded Amount],'financial_loan(1)'[Good vs Bad Loan] = "Bad Loan")
10. Bad Loan Total Received = CALCULATE([Total Amount Received],'financial_loan(1)'[Good vs Bad Loan] = "Bad Loan")
11. Good Loan % = (CALCULATE([Total Loan Applications], 'financial_loan(1)'[Good vs Bad Loan]="Good Loan")/COUNT('financial_loan(1)'[id]))
12. Good Loan Applications = CALCULATE([Total Loan Applications],'financial_loan(1)'[Good vs Bad Loan] = "Good Loan")
13. Good Loan Funded Amount = CALCULATE([Total Funded Amount],'financial_loan(1)'[Good vs Bad Loan] = "Good Loan")
14. Good Loan Total Received = CALCULATE([Total Amount Received],'financial_loan(1)'[Good vs Bad Loan] = "Good Loan")
15. LMTD Avg DTI = CALCULATE(AVERAGE('financial_loan(1)'[dti]), DATESMTD(DATEADD('Date Table'[Date].[Date],-1,MONTH)))
16. LMTD Avg Int Rate = CALCULATE(AVERAGE('financial_loan(1)'[int_rate]),DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))
17. LMTD Loan Applications = CALCULATE(COUNT('financial_loan(1)'[id]), DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))
18. LMTD Total Amont Received = CALCULATE([Total Amount Received],DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))
19. LMTD Total Funded Amont = CALCULATE([Total Funded Amount],DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))
20. MTD Amount Received = CALCULATE(TOTALMTD([Total Amount Received],'Date Table'[Date]))
21. MTD Applications = CALCULATE(TOTALMTD(COUNT('financial_loan(1)'[id]),'Date Table'[Date].[Date]))
22. MTD Avg DTI = CALCULATE(TOTALMTD(AVERAGE('financial_loan(1)'[dti]),'Date Table'[Date]))
23. MTD Avg Int Rate = CALCULATE(TOTALMTD(AVERAGE('financial_loan(1)'[int_rate]),'Date Table'[Date]))
24. MTD Funded Amount = CALCULATE(TOTALMTD([Total Funded Amount],'Date Table'[Date]))
25. Total Amount Received = SUM('financial_loan(1)'[total_payment])
26. Total Funded Amount = SUM('financial_loan(1)'[loan_amount])
27. Total Loan Applications = 
COUNT(
    'financial_loan(1)'[id]
    )
28. YOY Amount Received = ([MTD Amount Received]-[LMTD Total Amont Received])/[LMTD Total Amont Received]
29. YOY Avg Int Rate = ([MTD Avg Int Rate]-[LMTD Avg Int Rate])/[LMTD Avg Int Rate]
30. YOY DTI = ([MTD Avg DTI] - [LMTD Avg DTI])/[LMTD Avg DTI]
31. YOY Loan Amount = ([MTD Funded Amount]-[LMTD Total Funded Amont])/[LMTD Total Funded Amont]
32. YOY Loan Applications = ([MTD Applications]-[LMTD Loan Applications])/[LMTD Loan Applications]


 
