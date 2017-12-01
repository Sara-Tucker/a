# Financial Analysis Report
An explanation of how I used Python and the NumPy and Matplotlib packages for data analysis to create a company's financial report.

*Since financial information is involved, this is only an explanation of the process used to create a section of the report. The final fiscal report presentation has not been included.*

<br>
<br>

### The problem
Once every year, a local company needs to preform the tedious task of creating a report to analyze their finances over a 12 month period. The report involves doing many calculations to generate all their finance data.

Instead of manually creating the report by hand once a year like they previously have, they decided to hire a data analyst to create a reusable program where they can simply input the data of their revenue and expenses each year, and have the report automatically created for them.

<br>

### My approach
I decided the best way to solve the problem would be by using Python to preform the calculations on the datasets and then use the [NumPy](http://www.numpy.org/) and [MatPlotLib](https://matplotlib.org/) packages to plot and present data visually.

<br>

### The dataset
```python
#Dataset
revenue = [130574.49, 79606.46, 86611.41, 97175.41, 81058.65, 89105.44, 81496.28, 91766.09, 75305.32, 145379.96, 109713.97, 152433.50]
expenses = [22751.82, 51695.07, 100319.20, 124089.72, 87658.57, 85340.20, 34285.73, 55821.12, 67976.93, 112618.61, 92054.37, 34803.96]
```
The company supplied two lists of data from their 2016 financial period, one of the company's revenue and the other of their expenses.

<br>

### Calculating profit before and after tax
```python
#Calculate the profit of each month
monthly_profit = []
for i in range(0,len(revenue)):
    monthly_profit.append(revenue[i]-expenses[i])    
```
To find the profit of each month before tax, I simply do **Revenue - Expenses** for each month. I use a *for loop* to iterate over the data of each month in the data sets, which will be the main process I will use when iterating over data sets throughout this project.

<br>

```python
#Calculate the 30% tax of profits of each month
tax = [round(i * .30, 2) for i in profit]
    
#Calculate the profit of each month after tax is deducted
monthly_profit_after_tax = []
for i in monthly_profit:
    monthly_profit_after_tax.append(i-(i*.30))
```
Next I need to calculate how much the company needs to pay each month for the the 30% tax on profits. This is done by doing **Profit x .30**, which I round the result of to two decimal places. After the amount of tax owed each month is found, I calculate the profit of each month after tax is deducted with **Profit - Tax**.

<br>

```python
#Plot profit after tax is deducted
import numpy as np
import matplotlib.pyplot as plt

monthNames = ['January','February','March','April','May','June','July','August','September','October','November','December']

%matplotlib inline
plt.rcParams['figure.figsize'] = 12,5

plt.plot(monthly_profit_after_tax, ls='--', marker='o', ms=8)
plt.legend(loc='upper left', bbox_to_anchor=(1,1))
plt.xticks(list(range(0, 12)), monthNames)
plt.show()
```
![](https://i.imgur.com/hqOX5qT.png)

To begin visualizing the information, I import the NumPy and MatPlotLib libraries to plot the profit after tax data. By plotting this data, we can derive that profits seem to increase significantly during Winter, but fall off sharply in February leading to deficits for the months in Spring. I will touch on which months have the highest and lowest profits a bit later.

<br>

### Analyzing the mean monthly profit
```python
#Find the total profit for the year and the mean yearly profit
totalProfit = sum(monthly_profit_after_tax)
mean = totalProfit / len(monthly_profit_after_tax)
```
After adding together the profits of every month we find that **$245,568** is the total profit for the year. To find the mean monthly profit, which is the average amount of money made each month over an entire year, I do **Total Profit / 12 Months**, which makes the mean monthly profit **$20,464**. Interestingly, the profit for most months are a few ten thousand higher or lower than the monthly mean. This shows that there is a lot of variance month to month in profits.

<br>

```python
#Find which months preformed above or below the mean monthly profit
goodMonths = []
badMonths = []
for e in monthly_profit_after_tax:
    if e > sum(monthly_profit_after_tax)/len(monthly_profit_after_tax):
        goodMonths.append(e)
    elif e < sum(monthly_profit_after_tax)/len(monthly_profit_after_tax):
        badMonths.append(e)


#Find the best and worst month of the year for profits
bestMonth = max(monthly_profit_after_tax)
worstMonth = min(monthly_profit_after_tax)

```
With the mean monthly profit calculated, we can compare each month's profit to it and realize that months below the mean underperformed, and the months above the mean exceeded profit expectations. After that I use the min and max functions to find the months with the highest and lowest profits.

<br>

### Calculating profit margin
```python
#Calculate the profit margin of each month
monthly_profit_margin = []
for i in range(0,len(monthly_profit_after_tax)):
    monthly_profit_margin.append((monthly_profit_after_tax[i] / revenue[i])*100)
```
**Profit After Tax / Revenue** is the calculation done to find the net profit margin; the result of which is multiplied by 100 to show profit margin as a percentage.

<br>
<br>

*The rest of the analysis for the report has not been included.*
