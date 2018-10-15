
# Homework 2 Solution

## Update logs


## 1. Relational Algebra

**(2 points each, 4 points total)**

Consider the simplified schema below (primary keys are in **bold**):

* liquors(**lid**, name, price, manufacturer)
  
* sales(**month**, **seller**, **liquors**, county, quantity)

Note: sales(liquors) references liquors(lid), and month is a text field (e.g. January, February).

Construct relational algebra for the following queries:

* **Q1**: Find the names of liquors that had at least one sale in "Clarke" or "Marshall" counties for the month of November.
	* $\rho$(Clarke, $\Pi$liquors($\sigma$month="November" $\wedge$ county="Clarke" $\wedge$ quantity>0(sales))
	* $\rho$(Marshall, $\Pi$liquors($\sigma$month="November" $\wedge$ county="Marshall" $\wedge$ quantity>0(sales))
	* $\rho$(S(liquors$\rightarrow$lid), Clarke $\cup$ Marshall)
	* $\Pi$name(S $\bowtie$ liquors)


* **Q2**: Find the names of manufacturers that sold at least three different liquors during the month of January in "Marshall" county.
	* $\rho$(S(liquors$\rightarrow$lid), $\Pi$liquors($\sigma$month="January" $\wedge$ county="Marshall" $\wedge$ quantity>0(sales))
	* $\rho$(Liq, $\Pi$lid, manufacturer(S $\bowtie$ liquors)
	-   $\rho$(M(1$\rightarrow$lid1, 3$\rightarrow$lid2), Liq $\bowtie$manufacturer  Liq)
	-   $\Pi$manufacturer($\sigma$lid1$\neq$lid2(M))



## 2. More Relational Algebra

**(1 point each, 6 points total)**

Simply answer NULL if you believe the resulting table is empty or there are some errors with the expressions.

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


Write the result table for the relational algebra expressions:


1. π<sub>A,B</sub>(T1)

|A | B | 
|---|---|
|1 | x | 
|2 | y | 
|2 | z | 

2. T1 × π<sub>A</sub>(T1)

|A | B | C | A |
|---|---|---|---|
|1 | x | a | 1 |
|2 | y | b | 1 | 
|2 | z | c | 1 |
|1 | x | a | 2 |
|2 | y | b | 2 |
|2 | z | c | 2 |

3. T1 ⨝<sub>T1.B=T2.C</sub> T2 

|A | B | C | B | C | D
|---|---|---|---|---|---|
|1 | x | a | 1 | x | c |
|2 | y | b | 2 | x | a | 
|2 | z | c | 2 | y | c |

4. T1 − (T1 ∩ T2)

|A | B | C |  
|---|---|---|
|1 | x | a |
|2 | y | b |
|2 | z | c | 

5. T1 ⨝<sub>T1.A&lt;T2.B</sub> (σ<sub>B&lt;=2</sub>(T2))

|A | B | C | B | C | D
|---|---|---|---|---|---|
|1 | x | a | 2 | y | c |

6. T1 ⨝ (σ<sub>B=c</sub>(T2))

NULL

## 3. SQL
Write the following relational algebra expressions in SQL. Make sure your SQL can be executed.

1. π<sub>name,age</sub>(Student)

```
select name, age from student
```

2. Student × π<sub>age</sub>(Student)

```
select * from student, (select age from student);
```
OR
```
select * from student cross join (select age from student);
```
OR
```
select distinct * from student, (select age from student);
```
OR
```
select distinct * from student cross join (select age from student);
```

3. Student ⨝<sub>Student.name=Teacher.name</sub> Teacher 

```
select * from student, teacher where student.name=teacher.name
```
OR
```
select * from student, teacher on student.name=teacher.name
```
OR
```
select * from student natural join teacher
```

4. Student − (Student ∩ Teacher)

```
select * from student
except
(select * from(
	(select * from student)
	intersect
	(select * from teacher)
))
```

5. (σ<sub>year=2018</sub>(Student) )⨝<sub>Student.age&lt;Teacher.age</sub> (σ<sub>name=engene</sub>(Teacher))

```
select * from
student , (select * from teacher where name="engene") teacher
where student.year=2018 and student.age<teacher.age
```
OR
```
select * from teacher, student
where 
	student.year=2018 
	and student.age<teacher.age 
	and student.name="engene"
```

6. Student ⨝ (σ<sub>age&lt;=50</sub>(Teacher))
```
select * from 
student, (select * from teacher where age <= 50);
```
OR
```
select * from 
student cross join (select * from teacher where age <= 50);
```


