# DATAS
data analyst course

DAX (Data Analysis Expressions)
# 🧮 DAX (DATA ANALYSIS EXPRESSIONS)

DAX is a language used to calculate things in **Power BI (Power Pivot)**.  
**DAX full form:** DATA ANALYSIS EXPRESSIONS  

---

## 💡 Why Do We Need DAX?

- In visuals, Power BI calculates values **automatically (implicit calculation)**.  
- With DAX, we calculate **explicitly** and have full control.  
- In DAX, we can **name our own measures** (titles).  
- In auto calculations, we **can’t name** them manually.

---

## ⚖️ Measure vs Columns

- When we create something using **DAX**, it **won’t add new columns** in the dataset.  
- It will only act as a **temporary measure** (used for visuals).  
- Columns are permanent, but **measures are reusable** and lightweight.

---

## 🔢 Basic DAX Formulas

### 1️⃣ Total Amount
```DAX
Total Amount = SUM(shipments[Amount])


→ Calculates the total amount of each product in the shipments table.
When you place this in a visual (like column chart), it automatically sums for each product.

2️⃣ Shipment Count
Shipment Count = COUNTROWS(shipments)


→ Counts the number of shipments for each product.

3️⃣ Total Boxes
Total Boxes = SUM(shipments[Boxes])


→ Shows the total number of boxes for each product.

♻️ Measure Reusability

You can reuse measures that are already calculated.

Boxes Per Shipment = [Total Boxes] / [Shipment Count]
Amount Per Shipment = DIVIDE([Total Amount], [Shipment Count])


👉 DIVIDE() is a safer way to divide (it handles divide-by-zero cases automatically).

🧮 CALCULATE FUNCTION

CALCULATE() changes the filter context to calculate results based on conditions.

Bar Amount = CALCULATE([Total Amount], people[Sales_person] = "Barr Faughny")


→ Calculates total amount for the sales person Barr Faughny.

Bar % = DIVIDE([Bar Amount], [Total Amount])


→ Converts the value into percentage for Barr Faughny.

Barr Bar amount = CALCULATE(
    [Total Amount],
    people[Sales_person] = "Barr Faughny",
    products[Category] = "Bars"
)


→ Calculates total amount for Barr Faughny from Bars category.

BBA in Mar = CALCULATE(
    [Barr Bar amount],
    'calendar'[Year] = 2024,
    'calendar'[Month_num] = 3
)


→ Calculates the total amount for March 2024 (Month 3 of Year 2024).

👥 Team Calculation

You can calculate total for a group of people.

Total Amount (My Team)2 =
CALCULATE(
    [Total Amount],
    people[Sales_person] = "Barr Faughny"
        || people[Sales_person] = "Beverie Moffet"
        || people[Sales_person] = "Ches Bonnell"
        || people[Sales_person] = "Husein Augar"
)


or a simpler version using the IN operator:

Total Amount (My Team) =
CALCULATE(
    [Total Amount],
    people[Sales_person] IN {"Barr Faughny", "Beverie Moffet", "Ches Bonnell", "Husein Augar"}
)

⚙️ Conditional Formulas (IF Function)
Simple Condition
TC V1 = IF([Total Amount] > [Sales Target], "Yes", "No")

Nested IF (Multiple Conditions)
TC V3 final =
IF([Total Amount] > 2500000, "⭐⭐⭐",
    IF([Total Amount] > 2250000, "⭐⭐",
        IF([Total Amount] > 2000000, "⭐", "🛑")
    )
)


→ Displays stars based on total amount value.

🔍 Evaluation Context

Evaluation Context is what happens behind the screen in visuals or measures.
It decides how and when DAX formulas are calculated.

Two main types:

Row Context: Works on each row (for calculated columns).

Filter Context: Works on filters applied in visuals or CALCULATE().

Understanding Evaluation Context is very important in DAX.

🧱 ACMBU — Very Important Concept
Letter	Meaning	Description
A	Acquire Business Knowledge	Understand the business before building the report
C	Clean Data	Prepare, fix, and format the dataset properly
M	Model	Create correct relationships between tables
B	Blocks not Black Box	Build modular, transparent calculations
U	DAX Query View / Use Variables	Use variables to make DAX easier to read and debug
✅ Summary

DAX = Data Analysis Expressions (used in Power BI)

Helps to calculate data explicitly

Measures are reusable and lightweight

CALCULATE() changes filter context

IF function helps in conditions

Evaluation context is the key concept

Follow ACMBU for perfect Power BI models
