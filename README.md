# Homework 2

* Assigned: 10/10
* Due: 10/19 at 10:00AM electronically
* worth 3.75% of your grade


We want to emphasize that we have picked this dataset for educational purposes
and are not encouraging you to drink.


# 1. Analyze some data

**(2 points each, 10 points total)**



# 2. Relational Algebra

**(2 points each, 4 points total)**

        liquors(<u>lid</u>, name, price, manufacturer)
        sales(<u>month</u>, <u>seller</u>, <u>liquors</u>, county, quantity)

Given the simplified schema above (primary keys are surrounded by &lt;u> &lt;/u> tags), construct relational algebra for the following queries. Note: sales(liquors) references liquors(lid), and month is a text field (e.g. January, February).

* **Q1**: Find the names of liquors that had at least one sale in "Clarke" or "Marshall" counties for the month of October.

* **Q2**: Find the names of manufacturers that sold at least two different liquors during the month of October in "Clarke" county.



# 3. More Relational Algebra

**(1 point each, 6 points total)**

Given the following tables


T1

|A | B | C |  
|---|---|---|
|1 | x | a |
|2 | y | b |
|2 | z | c | 

T2

B | C | D
---|---|---
1 | x | c
2 | y | c
3 | x | a


Express the results for the relational algebra expressions:


1. π<sub>B,C</sub>(T2)
1. T1 × π<sub>A</sub>(T1)
1. T1 ⨝<sub>T1.C=T2.D</sub> T2 
1. T2 − (T1 ∩ T2)
1. T2 ⨝<sub>T1.A&lt;T2.B</sub> (σ<sub>B&lt;=2</sub>(T2))
1. T1 ⨝ (σ<sub>D=c</sub>(T2))



# Submission

Submit through [courseworks](https://courseworks2.columbia.edu/courses/6866/assignments/27330)

1. Submit `hw2.py` for part 1
1. Submit a pdf file for part 2 and part 3 

Include your name and UNI at the top of each page.


# Hints

* What does the `data` argument to the question functions contain? In `q1()`, try adding `print data[0]; print data[1]`
* Test your code on a small sample of data, so you can verify that it works before running it on the entire file.
* Importing the csv file into Google Sheets or Excel might help visually explore the data.
* Helper functions can make your code easier to understand. E.g to help refer to the columns by name instead of by position.
* Python dictionaries are very very useful.
