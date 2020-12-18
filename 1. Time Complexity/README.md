This interview question is about time complexity.

Time complexity refers to the amount of computer time it takes to run analgorithm.

There were 2 parts to this.

1) Given a list of stock price, write a function to return the best outcome possible.

Ex) input = [3, 6, 1, 8, 2, 4, 1, 5]

    output = 7 (bought on the 3rd day at $1 and sold on the 4th day at $8)


| function    | n = 1,000 | n = 10,000 |
| ----------- |:---------:| :---------:|
| efficient   | 1.04ms    | 7.7ms      |
| inefficient | 273ms     | 28.7s      |
