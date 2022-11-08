# CSE160-Project - Fraud Detection

One way to determine fraud in election results is to examine the least significant digits of the vote totals — the ones place and the tens place. The ones place and the tens place don’t affect who wins. They are essentially random noise, in the sense that in any real election, each value is equally likely. Another way to say this is that we expect the ones and tens digits to be uniformly distributed — that is, 10% of the digits should be “0”, 10% should be “1”, and so forth. If these digits are not uniformly distributed, then it is likely that the numbers were made up by a person rather than collected from ballot boxes (people tend to be poor at making truly random numbers.)

## Problem 1: Read and clean Iranian election data

There were four candidates in the 2009 Iranian election: Ahmadinejad, Rezai, Karrubi, and Mousavi. The file election-iran-2009.csv contains data, reported by the Iranian government, for each of the 30 provinces. We are interested in the vote counts for each of these candidates. Thus, there are 120 numbers we care about in the file.

Write a function called `extract_election_votes(filename, column_names)` that

- takes a filename and a list of column names and
- returns a list of integers that contains the values in those columns from every row (the order of the integers does not matter).

## Problem 2: Make a histogram

Write a function `ones_and_tens_digit_histogram(numbers)` that
- takes a list of numbers and
- produces the output as a list of 10 numbers.

n the returned list, the value at index i is the frequency with which digit i appeared in the ones place or the tens place in the input list (we are pooling together all the digits found in the ones places and the tens places in the input list).

## Problem 3: Plot election data

Write a function called `plot_iran_least_digits_histogram(histogram)` that

- takes a histogram (as created by ones_and_tens_digit_histogram),
- graphs the frequencies of the ones and tens digits for the Iranian election data, and
- saves the plot to a file named `iran-digits.png` and returns nothing

- `import matplotlib.pyplot` as plt to import the plt package
- `plt.plot(`) for the line itself (in order to make this line, you will need a list of length 10 in which every element is 0.1)
- `plt.title()` for the title
- `plt.legend(loc='upper left')` for the legend
- `plt.savefig()` to save the plot
- `plt.show()` to have Python open a new window and show the plot

## Problem 4: Smaller samples have more variation

From the previous problem, the Iran election data is rather different from the expected flat line at y = 0.1. Is the data different enough that we can conclude that the numbers are probably fake? No — you can’t tell just by looking at the graphs we have created so far. We will show more principled, statistical ways of making this determination.

With a small sample, the vagaries of random choice might lead to results that seem different than expected. As an example, suppose you plotted a histogram of 20 randomly-chosen digits (10 random numbers, 2 digits per number):

## Problem 5: Comparing variation of samples

In the previous problem, you can visually see that some lines we have plotted are closer to the ideal line than others. Rather than judging the closeness of two lines with our eyeballs, we can calculate how similar the two lines are by using a metric called the mean squared error (MSE).

Essentially, the MSE is a number that determines closeness of the two lines, where the larger the number is, the more different the two lines are. If the MSE is 0 then two lines are identical.

The MSE is computed as follows:

- For each point in one dataset, compute the difference between it and the corresponding point in the other dataset and then square the difference.
Take the average of these squared differences.
- The use of squares means that one really big difference among corresponding data points yields greater weight than several small differences. It also means that the distance between A and B is the same as the distance between B and A. That is, (9 - 4)^2(9−4) 
2
  is the same as (4 - 9)^2(4−9)^2
  
  
## Problem 6: Comparing variation of samples

### Part 1
Write a function called `calculate_mse_with_uniform(histogram)` that

takes a histogram (as created by `ones_and_tens_digit_histogram`) and
returns the mean squared error of the given histogram with the uniform distribution.
Example:

Calling `calculate_mse_with_uniform` with the histogram from the Iranian election results for the ones and tens digits should return the result 0.000739583333333.

### Part 2

Write a function called `compare_iran_mse_to_samples(iran_mse, number_of_iran_datapoints)` that

- takes two inputs: the Iranian MSE (as computed by calculate_mse_with_uniform()) and the number of data points in the Iranian dataset (120 but this should not be hardcoded),
- builds 10,000 groups of random numbers, where each number x is randomly generated such that 0 <= x < 100, and each group is the same size as the Iranian election data,
-computes the MSE with the uniform distribution for each of these groups,
-compares the 10,000 MSEs to the Iranian MSE by determining and printing
how many of the 10,000 random MSEs are larger than or equal to the Iran MSE,
how many of the 10,000 random MSEs are smaller than the Iran MSE, and
the Iranian election null hypothesis rejection level.
Each of these values should be printed after the Iran MSE from part 1.
