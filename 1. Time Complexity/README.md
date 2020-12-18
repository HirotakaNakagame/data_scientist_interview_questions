This interview question is about time complexity.

Time complexity refers to the amount of computer time it takes to run analgorithm.

There were 2 parts to this.

**1) Given a list of stock price, write a function to return the best outcome possible with a single buy/sell**

Ex) 
    input = [3, 6, 1, 8, 2, 4, 1, 5]<br />
    output = 7 (bought on the 3rd day at 1 USD and sold on the 4th day at 8 USD)

One solution to this would look like

```
def inefficient(ls):
    max_prof = 0
    for i in range(len(ls)):
        for j in range(i + 1, len(ls)):
            prof = ls[j] - ls[i]
            if prof > max_prof:
                max_prof = prof
    return max_prof
```    

This gets the job done but it turns out that it is very inefficient.
If the list had n elements, prof is calculated N times where N is 

N = (n - 1) + (n - 2) + ... + 1<br />
  = n * (n - 1)

It can actually be done much more efficiently with 1 for loop.

```
def efficient(ls):
    max_prof = 0
    min_price = ls[0]
    for i in range(1, len(ls)):
        if min_price > ls[i - 1]:
            min_price = ls[i - 1]
        if ls[i] - min_price > max_prof:
            max_prof = ls[i] - min_price
    return max_prof
```

Below is computational times for each function when the input list's lengths are 1,000, 10,000, and 100,000 respactively

| function    | n = 1,000 | n = 10,000 | n = 100,000 |
| ----------- |:---------:| :---------:| :---------: |
| efficient   | 1.04ms    | 7.7ms      | 63.8ms      |
| inefficient | 273ms     | 28.7s      | 45m 4s      |

You can see the "inefficient" function is very inefficient compared to the "efficient" function.

We don't want to spend 45 minutes when the same thing could be done in 64ms.

More importantly, we don't want to spend 45 minutes on cloud computing when it can be done in less than a second.

Especially in the era of big data, be aware of time complexity and write smart and efficient codes!!


**2) Given a list of stock price, write a function to return the best outcome possible with multiple buy/sell**

Ex) 
    input = [3, 6, 1, 8, 2, 1, 4, 5]<br />
    output = 14

It turns out that the max profit happens if you sell when the price is lower the following day.

This is not a realistic situation and you know the price in the future and you can also alter buy date as well.

With 1 loop, such function can be written as

```
def find_best_outcome(ls):
    profit = 0
    price_buy = ls[0]

    for i in range(1, len(ls)):
        # if you sell, the buy price will be the price of the following day(which can be updated if the price decreases)
        if i == len(ls) - 1:  #Case 1: this is the last day. sell if you can make profit, dont if you cant
            if price_buy < ls[i]: # you can make profit
                price_sell = ls[i]
                profit += price_sell - price_buy
            else: # you cant make profit
                pass
        else: # Case 2: this is not the last day and you still have an option to sell the following day
            if price_buy < ls[i]: # price is higher than the price_buy => sell if the price doesnt increase the following day
                if ls[i] > ls[i + 1]: # the price decreseas the following day => SELL
                    price_sell = ls[i]
                    profit += price_sell - price_buy
                    price_buy = ls[i+1] #update the buy price witht the following day's price
                else: # the price increases => dont buy and dont sell
                    pass
            else: # price is lower than the price_buy => dont sell. update the price_buy 
                price_buy = ls[i]
    return profit
```







As mentioned earlier, time complexity is a big topic in the big data era. It is important and crucial to write efficient codes more than ever.




Hope you enjoyed this.

Please check out other contents as well and leave me any comments!
