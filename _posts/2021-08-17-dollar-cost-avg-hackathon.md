---
layout: post
title:  "Dollar-Cost Averaging Crypto: 1-Day Hackathon Project"
date:   2021-08-02 18:20:23 +0100
categories: python crypto
---

>## *"BTC & ETH do seem high lol"*
> [@elonmusk][1]

As crypto markets start to move upwards once more I've been reading up on the concept of [dollar-cost averaging][4]. The idea of removing emotion from investment and damping some of crypto's wilder oscillations is a tempting idea, even if studies show that with [reduced risk comes reduced gains][3].

I pitched [MintyFresh][2] on the idea of modelling this strategy ourselves over a one day hackathon. 

He agreed.
### The Back End (local-optimum)

My role was to design and serve a new API that delivered a table of deposits and running portfolio values within a specified time period across a range of crypto and fiat currencies. I also decided to include a benchmark running total that modelled the user investing their total funds on day zero for comparison.

The code can be found [here][6], but the **tl;dr** is:

{% highlight python %}
def costAverageFunc(coin, deposit, currency, frequency, startdate):
    """function that takes the above strings as inputs, 
    converts them into an API query to coingecko
    then creates a dataframe of dollar cost averaging 
    returns vs a single bulk deposit"""
{% endhighlight %}

The output of this function is then wrapped in a flask app, the dataframe is jsonify'd and the resulting API is hosted on [heroku][7]. If you want to call the API yourself, simply append the following to the linked address 

>/dca/query?coin=INPUT&deposit=INPUT&currency=INPUT&frequency=INPUT&startdate=INPUT

[Example here][8].
### The Front End (MintyFresh)

As the interface designer, MintyFresh built a web app in JavaScript that allowed the user to choose the parameters for my **costAverageFunc**, call the API and return a simple Plotly visualisation of the returns over time. Have a go below!

<iframe src="https://mintyfresh.me/dca-crypto/" width="600" height="800" style="border: none;"></iframe>
<br/>
You can also find his code [here][9]

## Conclusions

Crypto in general has had such an astronomical rise in value over the last few years that any modelling that goes back more than 18 months generates significantly lower returns compared to going all in early. 

However there are situations where dollar-cost averaging does come out on top, intuitively this is true when starting the model at one of the peaks (eg mid March 2021 where DCA actually generates a profit versus a 20% loss for those that buy only at the peak). In general losses are reduced as the market dips and the investor is getting more crypto for their money to compensate.

We must also consider that there are many situations where the recreational investor is only able to put money in periodically rather than all at once. In this case it may be reassuring to know that buying regularly rather than saving up for a "dip" may be a better strategy (the classic "time in the market is better than timing the market"), however I'm not confident our current visualisations can prove that assertion.

## Next Steps

This project was my first experience creating APIs and using Flask so I'm sure there are some more elegant alternatives to my approach. However the real stretch goals for this project are in the visualisations, not just in opportunities to tidy up formatting but in how to clearly define and answer useful questions around DCA. 

Comparing regular investment vs an initial bulk buy was the best we could think of within the time constraints. Going forward I would be interested in allowing users to hand pick buy-in points to simulate saving up to time the market or simply model their previous investment decisions.

If you have any ideas for visualisations or further expansion of this work please leave a comment on [github][6].



[1]: https://twitter.com/elonmusk/status/1363021091086561285
[2]: https://mintyfresh.me/
[3]: https://www.cnbc.com/2021/08/12/which-investment-strategy-is-better-lump-sum-or-dollar-cost-averaging.html
[4]: https://www.vanguardinvestor.co.uk/articles/latest-thoughts/how-it-works/what-is-pound-cost-averaging
[5]: https://www.coingecko.com/en/api
[6]: https://github.com/local-optimum/dollar-cost-avg-widget
[7]: https://dca-crypto.herokuapp.com/
[8]: https://dca-crypto.herokuapp.com/dca/query?coin=bitcoin&deposit=100&currency=usd&frequency=1&startdate=2021-01-05
[9]: https://github.com/MintyFresh-2/dca-crypto