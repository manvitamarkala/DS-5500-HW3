# Homework 3 Solutions 

## Problem 1

### Import and explore the district-level fiscal data from 2015-16.Rank and visualize the states that take in the most federal funding (revenue).

I have imported the file Sdf16_1a.txt and pulled the metrics federal revenue, state name, district and number of students eligible for funding into a dataframe. After that, I have observed that there are negative values for federal revenue and upon reading the documentation, realised that these are different categories of missing data. Thus I eliminated these rows from the dataframe and then performed a sum operation for federal revenue grouped by states and ordered it in descending.

Below is the graph(figure 1) that shows the states that take in most of the federal funding. The plot below indicates that the top 3 states that are heavily funded are California, Texas and New York.

![fd[]{label="fig:FD"}](FD.png)
###### Figure 1: Federal revenue across states


### Which states spend the most federal funding per student?

Across every state, I then divided the federal revenue with the number of students that the government funds to calculate the spend per student. Figure 2 shows that District Of Columbia, Alaska and Louisiana are among the top states to spend the highest federal funding for their students

![fd_s[]{label="fig:FD_S"}](FD_S.png)
###### Figure 2: Federal fund spend per student across states

## Problem 2

### Visualize the relationship between school districts’ total revenue and expenditures.

I pulled in the columns for total revenue and total expenditure and aggregated them across districts(here considered LEAID for different districts) and sorted by the descending values of the total revenue. I plotted the relationship between the total revenue and expenditure by state and can be seen in figure 3.

![TR_TE[]{label="fig:TR_TE"}](TR_TE.png)
###### Figure 3: Relation between total revenue and expenditure


### Which states have the most debt per student?

I calculated the debt per student metric using the formula - ( total expenditure- total revenue)/ number of students funded. Figure 4 shows the top states that have maximum debt per student. North Dakota, District of Columbia and Alaska are among the top states.

![DEBT_S[]{label="fig:DEBT_S"}](DEBT_S.png)
###### Figure 4: Most debt per student across states


## Problem 3

### Write and explain a function for processing a single column of “blurred” metrics into usable numeric values.

I use the following function shown in figure 5 for processing blurred metrics:

Initially, I converted the column under consideration to a string format and then accordingly cast to integer based on the requirement
Using regex, for PS, NaN, empty strings and ., I imputed them with NaN, which I later replaced with the mean of the column values. Since the lower limit for the column range is 0 and the upper limit for column range is 100 

- For less than (LS50) , I took an average of 1 number less than 50, 49 with 0 i.e. (49+0)/2
- For less than equal (LE50) , I took an average of the number 50 with 0 i.e. (50+0)/2
- For greater than (GT50) , I took an average of 1 number more than 50, 51 with 100 i.e. (51+100)/2
- For greater than equal (GE50) , I took an average of the number 50 with 100 i.e. (50+100)/2.
- For ranged data like 15-20, I took the average of 15, 20.
- For all other formats numbers, just took the number itself.

![BLURRED[]{label="fig:BLURRED"}](BLURRED.PNG)
###### Figure 5: Blurred Function

### Use it to process and then visualize the distribution of a performance metric of your choice

I looked at the column 'ALL_MTH00PCTPROF_1516' which is nothing but the the percentage proficiency of all students who completed a state assessment in mathematics and for whom a proficiency level was assigned across all grades in SY 2015-2016 and found the following distribution.

![PP_M[]{label="fig:PP_M"}](PP_M.png)
###### Figure 5: Distribution of a performance metric 

# Problem 4:

### Choose which school districts will have their funding cut and how this will be done.

The total amount of Federal Revenue across all states is: 55602742000
15% budget cut amounts to:  *8340411300.0*
After cutting 15% of the revenue the amount that still remains: 47262330700.0

The table representing the leaids( districts) vs cuts is as belows:

![LEAID_CUT[]{label="fig:LEAID_CUT"}](LEAID_CUT.PNG)
###### Figure 6: LEAID-CUT 

# Problem 5:

### Provide a statement for your supervisor justifying your decisions on which school districts will lose funding.

As we have observed that different states have a lot of difference amongst each other interms of the revenue funding and the debt/student each state owes.

To balance out the difference and give equal importance to all the states interms of the funding, I feel the best way to do the 15% cost cutting for the federal revenue, is by checking which of the states have a surplus amount (Total Revenue - Total Expenditure) that is high enough and in turn also higher than the individual states' federal revenue itself and pull this amount worth the federal revenue from those states until we achieve  *8340411300.0*. We have captured roughly 5K districts.
