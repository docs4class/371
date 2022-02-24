# Data Analytics I Quizzes

## Quiz One (Linear Regression)

Name: __________________________

 
1. Add a another variable (column) to the `women` dataframe called GPA which is these 15 numbers: 1.5, 3.7, 4,1, 3, 2.5, 3.8, 0.8, 2, 4, 1, 3, 2.5, 3.0, 4.0

<br>
<br>

2. Use GPA and weight to predict the height of a person who is 155 pounds and has a GPA if 3.33. What is your prediction? _______

3. Is GPA a significant predictor of height and how do you know? 

<br>
<br>

4. Create a figure showing a best fit line on of height and GPA.  

<br>
<br>

5. Install the dplyr package into your Rstudio session.


## Quiz Two

Name:___________________________________


```
#>      [,1] [,2] [,3] [,4] [,5]
#> [1,]    1    4    7   10   13
#> [2,]    2    5    8   11   14
#> [3,]    3    6    9   12   15
```



1. Write the code that creates this matrix:


2. Write DIFFERENT code that creates this matrix in an alternate way:


3. In the matrix above, what does `[,4]` mean?


4. What code would return the value in the 3rd column and 3rd row?


5. What single line of would give you the average of the all the numbers in columns 2, 4, and 5 and in rows 1 and 3?


## Quiz Three

Name: __________________________







```r
df
#>    X1 X2 X3 X4 X5 X6 X7 X8 X9 X10
#> 1   1 11 21 31 41 51 61 71 81  91
#> 2   2 12 22 32 42 52 62 72 82  92
#> 3   3 13 23 33 43 53 63 73 83  93
#> 4   4 14 24 34 44 54 64 74 84  94
#> 5   5 15 25 35 45 55 65 75 85  95
#> 6   6 16 26 36 46 56 66 76 86  96
#> 7   7 17 27 37 47 57 67 77 87  97
#> 8   8 18 28 38 48 58 68 78 88  98
#> 9   9 19 29 39 49 59 69 79 89  99
#> 10 10 20 30 40 50 60 70 80 90 100
```

1.  Consider the dataframe above called `df`.  What would running this code return `sum(df[7,7:10])`



2. How can you tell if an object in R is a dataframe?


3. How could you create the dataframe above called `df`?


4. What code would return the average of row 2 of `df`?


5. Consider `mtcars` dataset that comes preloaded with R that looks like this:

```r
head(mtcars)
#>                    mpg cyl disp  hp drat    wt  qsec vs am
#> Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1
#> Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1
#> Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1
#> Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0
#> Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0
#> Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0
#>                   gear carb
#> Mazda RX4            4    4
#> Mazda RX4 Wag        4    4
#> Datsun 710           4    1
#> Hornet 4 Drive       3    1
#> Hornet Sportabout    3    2
#> Valiant              3    1
```

6. Why do I get this error when I run the code below: `Error in plot(hp, mpg) : object 'hp' not found`?


```r
plot(hp,mpg)
```

`Error in plot(hp, mpg) : object 'hp' not found`

Bonus: What is a topic that you find confusing at this point in class? 
