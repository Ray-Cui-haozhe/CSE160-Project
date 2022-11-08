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
