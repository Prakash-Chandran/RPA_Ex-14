# RPA_Ex-14

# Capstone Project - Personal Finance Categorization and Summary Automation
~~~
Name : PRAKASH.C
Reg. No : 212223240122
~~~

## Aim
To automate the process of reading personal transaction data from a CSV file, categorizing expenses into various groups (Food, Transport, Bills, Others), and generating a summary report with total amounts and current date in an Excel file using UiPath.

## Materials Required
UiPath Studio (Community/Enterprise Edition)
Windows OS
Input transaction file (CSV format)
Basic knowledge of UiPath:
Read CSV
For Each Row
If Condition
Dictionary & Variables
Add Data Row
Write CSV

## Procedure

### Step 1: Prepare Input File
  Create a CSV file named transactions.csv
  Columns: Date, Description, Amount
  Example:
  ~~~
  2025-05-21, TNEB Online Payment, 600
  2025-05-21, Swiggy Order, 250
  ~~~

### Step 2: Build Category Logic
  Read the CSV file using Read CSV → Output: dtTransactions.
  Create a Dictionary variable:
  Name: categoryTotals
  Type: Dictionary<String, Double>
  Default value:
  ~~~
  New Dictionary(Of String, Double) From {
     {"Food", 0},
     {"Transport", 0},
     {"Bills", 0},
     {"Others", 0}
  }
  ~~~
  Loop through each row in dtTransactions with For Each Row.
  
  Inside the loop:
  
  Assign: desc = row("Description").ToString.ToLower
  
  Assign: amount = Convert.ToDouble(row("Amount").ToString)
  
  Use If conditions to match descriptions:
  
  If desc.Contains("swiggy") Or desc.Contains("zomato") Or desc.Contains("food")
      → categoryTotals("Food") += amount
  
  ElseIf desc.Contains("uber") Or desc.Contains("ola") Or desc.Contains("bus") Or desc.Contains("train")
      → categoryTotals("Transport") += amount
  
  ElseIf desc.Contains("tneb") Or desc.Contains("recharge") Or desc.Contains("bill")
      → categoryTotals("Bills") += amount
  
  Else
      → categoryTotals("Others") += amount📊 
      
  ### Step 3: Create a Summary Table
  Add Build Data Table activity → Name it dtSummary
  
  Columns: Category (String), Total (Double), Date (String)
  
  Use For Each item In categoryTotals
  
  Add Data Row:
  ~~~
  { item.Key, item.Value, Now.ToString("dd-MM-yyyy") }📤
  ~~~
  
  ### Step 4: Write Output
  Use Write CSV activity
  

# Sequence :
![14-1](https://github.com/user-attachments/assets/2b33c2c9-1b7d-44e5-89e4-a5d7e0d530cf)

![14-2](https://github.com/user-attachments/assets/2e0d9c17-55f0-42a3-a986-0638e6763666)

![14-3](https://github.com/user-attachments/assets/69a78c00-d6cb-4c40-b02e-18da4b9a6541)

![14-4](https://github.com/user-attachments/assets/a4058523-06d2-4413-b8b1-59b6933b5f70)

![14-5](https://github.com/user-attachments/assets/ee9ebc0b-1c5e-4326-9487-573015758198)

![14-6](https://github.com/user-attachments/assets/6d3341e4-5c84-4265-a913-da6078c204d2)


# Input:
![14-7](https://github.com/user-attachments/assets/2b837ffe-01b2-48de-a16a-d44c43fd6dac)

# Output :
![14-8](https://github.com/user-attachments/assets/1de34c3c-6bc1-4a1b-aca7-7fc9b9efc36a)

# Result :
The workflow successfully categorizes transaction data based on their description into 4 groups and generates a daily summary in a structured CSV file with date tracking.
