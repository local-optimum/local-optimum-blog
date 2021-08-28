---
layout: post
title:  "The Invisible Tax: Python Project #0"
date:   2021-08-02 18:20:23 +0100
categories: InvisibleTaxProject
tags: inflation python
---
>## *"haha money printer go brrrrr"*
> @femalelandlords (account suspended)

Whilst governments all over the world continue to [print][1], [money][2] to pay down the [debt][3] created by their response to the Covid-19 pandemic, I began to realise just how difficult it was to keep track of this increasing cost of living in my personal finances.

My ISA app tells me the percentage return on my investments over the last few years  but not the difference in that percentage increase from the percentage loss the pound has taken in the meantime.

I can see the total amount of cash I have in my bank account, but not whether a recent pay rise has increased my standard of living or merely maintained it. 

Should I even be holding cash at all or paying off credit cards with low enough interest rates that my debt shrinks in line with inflation?

These don't feel like uncommon concerns for most people and they feel like increasingly pressing concerns in the current financial climate.

The information we need to inform these decisions is out there but it is often:
1. **Poorly or misleadingly presented** - rising and falling positive inflation is still compounding the cost of living.

2. **Too theoretical to be useful** - I can compare single amounts of money to current amounts, but not multiple deposits over multiple years.

3. **Heavily cherry picked** - A consumer price index that *doesn't* factor in house prices is hiding key information about modern citizens' ability to accumulate capital.

To that end I'm developing the [Invisible Tax Calculator][4], a tool that is designed to form the basis of what would ideally become a genuinely practical wealth analysis tool.

## The Proof of Concept

At its core **The Invisible Tax Calculator** is designed to address points 1. and 2. of the above. It should enable individuals to submit a table of GBP deposits and produce some informative graphs and statistics about the impact of inflation on those savings based on current UK CPI.

These results can then be used to compare against the actual performance of that cash when invested to understand how much return is required to outpace inflation.

Once the above has been achieved, I intend to expand the functionality of the program with additional measures such as house prices, gold prices and stock market returns to help mitigate what was mentioned in point 3.

Finally I want to build a front end site that enables users to model their finances with a much greater degree of flexibility and intuitiveness.

## Learning Python

It is worth noting that this project will be my first truly independent effort since I began learning Python. I will no doubt create inelegant solutions and make some mistakes along the way and I would welcome feedback or comments from anyone who tests out the current work in progress.

I felt like this would be an interesting starting project as it combines a few key areas I want to develop, namely:
* Dataframe creation and management
* Parsing APIs
* Data visualisation

In my next post I'll describe the initial structure of the program as well as sharing my data sources and calculations.

Thanks for reading!


[1]: https://www.independent.co.uk/news/business/news/bank-england-money-printing-coronavirus-b1610167.html
[2]: https://www.cityam.com/almost-a-fifth-of-all-us-dollars-were-created-this-year/
[3]: https://www.bbc.co.uk/news/business-53104734
[4]: https://github.com/local-optimum/invisible-tax-calculator
