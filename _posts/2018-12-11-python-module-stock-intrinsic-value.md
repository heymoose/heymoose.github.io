---
layout: post
title: Intrinsify
subtitle: An experiment creating a python command line tool that grabs stock data
show-avatar: true
social-share: false
---

I've been spending a lot of time learning and working with python lately.  The way it works,
and the culture surrounding the open source language is really interesting to me.  As such,
I've been trying to think of little projects to work on in order to sharpen my skills.

One of my go-to's in this area is working with stock data.  I have an interest in studying
financial data and making informed investing decisions in businesses that seem to be
undervalued.  I made a Google spreadsheet years ago that would help me make some of these
decisions.  Or, at the least, it helped me narrow down the list of businesses that I should
take a closer look at.  The spreadsheet would fetch stock data from Yahoo Finance and
automatically populate a bunch of cells.  Then the spreadsheet was set up to automatically
calculate the rough intrinsic value of each stock, in other words, a rough calculation
of how much the business is worth based on it's financial data.  You can read more about
intrinsic value and how it is calculated on [Joshua Kennon](https://www.joshuakennon.com/benjamin-graham-intrinsic-value-formula/)'s blog, which is the best description of it I know of.

<div class="polaroid">
    <img class="cardimg" src="/img/2018-12-11-python-module-stock-intrinsic-value/google-spreadsheet-iv.png" alt="Screenshot of Google spreadsheet for stock intrinsic value">
    <div class="cardimg-label">
        <p><i>My Google spreadsheet for calculating stock intrinsic value</i></p>
    </div>
</div>

Alas, the Google Finance API was deprecated years ago and is no longer reliable.  My spreadsheet
is still limping along, but the data is no longer reliable, and I can longer count on it working
in the long term.  And so it was time to come up with an alternative.

I decided it would be cool to have a python module that did the same thing, and sort of use it
as an excuse to experiment with a couple of different concepts.

The first challenge was finding a service that I could use to grab stock data.  Despite living
in the world of open source, this seems to have gotten harder over the years than easier.  It
used to be that Yahoo Finance had an API for every major language and it was free.  But those
days are over, as Yahoo Finance was suddenly shut down a while ago.  After some searching,
I finally landed on [IEX Trading](https://iextrading.com/developer/docs/#getting-started), which
already has a python wrapper around their free API to grab stock data.  Using the API is really
simple.  The following python class grabs the stock information I want:

```python
class StockData():
    def __init__(self, ticker):
        self.ticker = ticker
        self.stock = Stock(ticker, output_format='pandas')
        self.sector = self.stock.get_sector()['sector'][ticker]
        self.name = self.stock.get_company_name()['companyName'].to_string()
        self.price = self.stock.get_price()['price'][ticker]
        self.eps = self.stock.get_key_stats()[ticker]['latestEPS']
        self.flat_growth_estimate = 5
        self.aaa_corporate_bond_yield = 3.56
        self.intrinsic_value = (self.eps * (8.5 + (2 * self.flat_growth_estimate)) * 4.4) \
            / self.aaa_corporate_bond_yield
        self.norm_intrinsic_value = self.intrinsic_value / self.price
        self.attractive = u'\u2713' if self.norm_intrinsic_value > 1 else ' '
```

There are some magic numbers in there at the moment, like the hard coded flat growth estimate,
and the AAA corporate bond yield, but I haven't figured a good way to dynamically set those yet,
and they have to do with calculating the intrinsic value of a stock.  But this is a good start and
it gets me the same information that my spreadsheet would have been using.

From here I took python code I had, turned it into a package, and set it up so that I could use
it as a command from the terminal using the awesome [Click](https://click.palletsprojects.com/en/7.x/)
package.  The following code (after installing the intrinsify locally on my machine using the
'pip install .' command in the terminal) makes it so I can do the following:
intrinsify input.txt, where input.txt contains a comma separated list of ticker values.

```python
@click.command()
@click.argument('input', type=click.File('rb'), nargs=-1)
def intrinsify(input):
    click.echo("Parsing input file...")
    tickers = parse_file_input(input)

    click.echo("Fetching stock data...")
    stocks = [StockData(ticker) for ticker in tickers]

    stocks_tabular = [stock.construct_tabular_output() for stock in stocks]
    click.echo(tabulate(stocks_tabular, data_headers, tablefmt='psql'))
```

I'm also using the tabulate package in order to display the information in an orderly way
in the terminal window.  Provided an input.txt file with a bunch of tickers, the output looks
like this:

<div class="polaroid">
    <img class="cardimg" src="/img/2018-12-11-python-module-stock-intrinsic-value/intrinsify-result.png" alt="Screenshot of intrinsify results">
    <div class="cardimg-label">
        <p><i>The results in the terminal after running intrinsify on a list of stocks</i></p>
    </div>
</div>

One the right side, you can see the Intrinsic Value and Normalized IV columns.  Those are the
absolute intrinsic value calculated per share, and the normalized value gets a value where
anything greater than 1 is undervalue, and anything under 1 should be ignored as it's
overvalued.  On the left I added a column that simply prints a check mark if the stock
passes the test.

This essentially does the same thing as my spreadsheet that I used for so long.  I'm glad to
have a replacement that's a bit more future proof.  If for some reason the iexfinance package
stops working, I'm sure there will be another that I can simply replace it with.

I would have liked to go into more detail about this, but I'm writing this after the fact from
memory.  A lot of the lessons I learned in the moment and useful tidbits are now forgotten.  For
future posts I plan on doing the writing as I go along to prevent this from happening.

Feel free to check out the [intrinsify repo on GitHub](https://github.com/heymoose/intrinsify) if
you'd like to look at the full code.
