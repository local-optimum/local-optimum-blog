---
layout: post
title:  "The Invisible Tax: Python Project #1"
date:   2021-08-28 21:20:23 +0100
categories: InvisibleTaxProject
tags: inflation python
---

>## *"The lesson is clear, inflation devalues us all."*
> Margaret Thatcher

Don't forget to check out [Part #0](https://local-optimum.github.io/local-optimum-blog/invisibletaxproject/2021/08/02/invisible-tax-project-part-0.html) for a recap of my motivations.
## Mapping the Problem

My first step was to map out the different steps of the process and determine how this would structure my code. I wanted to generate self contained modules that could be implemented and tested independently.

The structure I settled on is detailed below. It involves 4 main elements:
1. Taking an input of the user's transaction history (desposit amounts & dates) as a baseline to model the data.

2. Tailoring an API based on the date range provided by the user and using it to build a query to a Consumer Price Index API. I chose the [OECD.stat](https://stats.oecd.org/Index.aspx?DataSetCode=PRICES_CPI) website due to its felxibility. whilst initially I will only work with UK data I wanted to make it simple to extend this functionality at a later date.

3. The user input and inflation statistics would then be converted into one master dataframe that applied the CPI stats to the user's inputs, tailoring the impact of inflation for their specific case.

4. Finally we would want to present this information in a visually appealling and informative manner, as well as giving them the option to export the raw data themselves for further analysis

![image-title-here](/local-optimum-blog/assets/images/inf-program-map.jpeg)

All of the above would then be called via a main.py wrapper with helpful explanatory text to the user!

## Module 1: User Input

My initial attempt created a dictionary to take user inputs prompting them to create {date: deposit amount} pairs, however during testing I found it extremely time consuming to enter each desposit individually. There are already a large number of [sites](https://www.thisismoney.co.uk/money/bills/article-1633409/Historic-inflation-calculator-value-money-changed-1900.html) that allow users to model the impact of inflation on single transactions, therefore the USP of this project should be that it allows users to map multiple transactions across a range of dates.

After some research into Standard Input, I rewrote the code as follows.

```python
#import user transactions and convert to a dataframe
while True:
    try: 
        print("Please submit your deposits/withdrawls in the following format:\nYYYY-MM XXXX\nYYYY-MM XXXX\nUse Ctril+d to submit your data without entering a blank line")
        userdepositraw = sys.stdin.read().splitlines()
        deposits = [x.split() for x in userdepositraw]
        depositsdf = pd.DataFrame(deposits, columns = ['year_month','deposits'])
        depositsdf['deposits']= depositsdf['deposits'].astype(int)
        depositsdf['year_month'] = pd.to_datetime(depositsdf['year_month'])
        netdepositsdf = depositsdf.groupby(['year_month']).sum().reset_index()
        print()
        print("Deposits submitted, thank you.")
        break
    except:
        print("Input not accepted, please try again.")

#find the earliest date to query inflation data from

earliest_date = min(netdepositsdf['year_month'])

start_time =earliest_date.strftime("%Y-%m")
```

By reading in several lines in a standardised format I was able to allow the user to paste large numbers of deposits at once, input multiple deposits on a single date and immediately map the result to a dataframe, making the future integration with the inflation API result much easier.

As you can see I'm relying on any errors generated in the manipulation of the input to ensure the user input is in the correct format before proceeding. I'm sure there are a number of edge cases that could slip through however.

Finally, I used the dataframe to find the earliest deposit date which would act as an input for Module 2: The API Call...