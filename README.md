# Exchange-Rate-Calculator
A quick solution to the following:

A currency pair is the quotation of two currencies, with the value of one currency being quoted against the other. Currencies are identified by a three letter alphabetic ISO code they are associated with on the international market.

The first listed currency of a currency pair is called the base currency and the second currency is called the quote currency. It indicates how much of the quote currency is needed to purchase one unit of the base currency.

For example, the quotation EURUSD 1.25 means that one Euro is exchanged for 1.25 US Dollars. EUR is the base currency and USD is the quote currency.

Given a list of currency pair quotations calculate the provided exchange rate.

If the requested currency pairs are the same, for example, USDUSD, then the exchange rate is always 1.00

Likewise if you have a rate for USDGBP and you need GBPUSD then you can invert the rate to obtain the exchange rate.

Input:

A list of currency exchange rates separated by ';'. A currency pair to calculate separated by '|' from the rest of the input.

Output:

Calculated exchange rate for the provided currency pair. Required precision is 2 decimal points.

If you cannot calculate the exchange rate the expected output should be:

'Unable to determine rate for <currency pair>'.
