# Logistic Regression

## Introduction

In the previous chapter we discussed linear regression, a type of supervised machine learning often used to make qualitative predictions. Now, we are moving on to logistic regression, another form of supervised machine learning that is commonly used for making predictions of some Boolean variable.  

This form of machine learning is typically used when using a prediction to answer a yes or no question. For instance, let's say we wanted to predict whether or not someone will suffer from a stroke. Using logistic regression, we can determine the probability that someone will either have a stroke (yes/true/positive result) or will not have a stroke (no/false/negative result). 

Also in this chapter we will discuss the difference between training and test data sets, why they are important, and how we apply them in logistic regression. This will help us to discuss the interpretation of these models and how we can test their accuracy. 

As stated previously, these topics may be difficult, and will be especially difficult if you still don't understand previous machine learning topics discussed in this course. Be sure to ask questions and seek help if you begin to struggle. This section will call on concepts from the very beginning of the course. 


## Training Data and Test Data

In supervised machine learning, we provide the computer with data and in essence "teach" it how to treat the data and create predictions with it. Training data is the data we feed our model so that it can make accurate predictions of the probability of an outcome. Meanwhile, test data is the data we compare our model to in order to assess its accuracy. 

So, using the example above, if we were building a model to test the probability of someone having a stroke, we would segment our main data set into two parts, a training set and a test set. Then, after we build our model, we would compare the model's output to the actual data and see how many times it made accurate predictions, this would in turn give us our model's accuracy. 


## Model Structure

Let's use the Auto data set to create a basic logistic regression model. Warning, we are going to be calling on information from earlier in the class a lot during these sections, so if you see any code you are unfamiliar with, first look in earlier class materials as it will not be reexplained here. 

Let's load in some data from the ISLR package and make some predictions using the "mpg" variable. We want to find the median of the variable, and then predict whether a vehicle will have an mpg above or below that middle point. To do this with logistic regression, we must create a factor object using mpg that our model will try to predict. 


```r
library(ISLR)
library(dplyr)

data("Auto")
attach(Auto)
summary(Auto)
#>       mpg          cylinders      displacement  
#>  Min.   : 9.00   Min.   :3.000   Min.   : 68.0  
#>  1st Qu.:17.00   1st Qu.:4.000   1st Qu.:105.0  
#>  Median :22.75   Median :4.000   Median :151.0  
#>  Mean   :23.45   Mean   :5.472   Mean   :194.4  
#>  3rd Qu.:29.00   3rd Qu.:8.000   3rd Qu.:275.8  
#>  Max.   :46.60   Max.   :8.000   Max.   :455.0  
#>                                                 
#>    horsepower        weight      acceleration  
#>  Min.   : 46.0   Min.   :1613   Min.   : 8.00  
#>  1st Qu.: 75.0   1st Qu.:2225   1st Qu.:13.78  
#>  Median : 93.5   Median :2804   Median :15.50  
#>  Mean   :104.5   Mean   :2978   Mean   :15.54  
#>  3rd Qu.:126.0   3rd Qu.:3615   3rd Qu.:17.02  
#>  Max.   :230.0   Max.   :5140   Max.   :24.80  
#>                                                
#>       year           origin                      name    
#>  Min.   :70.00   Min.   :1.000   amc matador       :  5  
#>  1st Qu.:73.00   1st Qu.:1.000   ford pinto        :  5  
#>  Median :76.00   Median :1.000   toyota corolla    :  5  
#>  Mean   :75.98   Mean   :1.577   amc gremlin       :  4  
#>  3rd Qu.:79.00   3rd Qu.:2.000   amc hornet        :  4  
#>  Max.   :82.00   Max.   :3.000   chevrolet chevette:  4  
#>                                  (Other)           :365

Auto <- Auto %>% 
  mutate(mpg01 = ifelse(Auto$mpg > 22.75, 1, 0))
Auto[Auto$mpg01 == 0,]$mpg01 <- "Below"
Auto[Auto$mpg01 == 1,]$mpg01 <- "Above"
Auto$mpg01 <- as.factor(Auto$mpg01)

attach(Auto)
```

Now that we have a variable to predict, we can build the model. 


```r
glm.auto <- glm(mpg01 ~ weight + cylinders, data = Auto, family = "binomial")
```

As you can see, the structure is very similar to that of a linear regression model except for our specification of the data set we want it to use (this can be done in linear regression, but we did not earlier in the class) and the family argument which we have not seen before. 

In this course, we will only every specify family to be binomial, this tells R that the variable we are predicting only has two outcomes. The data argument is used to specify a training data set if we were using one, which we are not in this example. 


## Model Interpretation

This is where things start to make a more complicated turn. We are going to look at how we evaluate the model's performance. First, we must tell R to make the prediction and store the results in an object. 


```r
mpg01.probs <- predict(glm.auto, type = 'response')
mpg01.probs[1:10]
#>         1         2         3         4         5         6 
#> 0.9769013 0.9866197 0.9719307 0.9716889 0.9729552 0.9979876 
#>         7         8         9        10 
#> 0.9980630 0.9978088 0.9984275 0.9915263
```

If we were to look at the mpg01.probs object it would contain the probability of the desired response, which is the true/positive response by default. However, we want this to be more intuitive, so we will make everything in the data set say "Below" unless the percentage is above what we consider a fair odds. So, in our case we will say that anything over 50% has a fair chance of being above the median mpg. 


```r
mpg01.pred <- rep('Below',392)
mpg01.pred[mpg01.probs>.5] = 'Above'
```

Finally, we can test our accuracy with a confusion matrix. The matrix will show our models predictions compared to the actual outcome. We can use this to test our accuracy and from there tweak different aspects of the model to help reduce variance. 


```r
table(mpg01.pred,mpg01)
#>           mpg01
#> mpg01.pred Above Below
#>      Above    18   170
#>      Below   178    26
```

Looking at the table we just produced, our accuracy is not the greatest. In fact, it's pretty terrible. We get our accuracy by adding up the two areas where our model and the actual data match (in this case where above/above and below/below overlap) and then we divide this number by the total number of observations we had in the data set. Using our R arithmetic knowledge, we find our accuracy to be .1122 or 11.22%...as stated before, a terrible accuracy. In fact, we typically aim for accuracy of 95% or better.

However, having lower prediction accuracy is common and not necessarily a terrible thing. In fact, we sometimes learn more from inaccurate models than we do the more effective ones. For instance, we now know that perhaps our variables are not as correlated as we once thought, or perhaps we set the value for our mpg01.probs object too low. From here, the best thing to do is gather insights, tweak your model, and move on. 

## Review Questions

1) What is the difference between logistic regression and linear regression? What is an example of an application for each of them?

2) From scratch, create a logistic regression model using the "Smarket" data set from the ISLR package. You are to create a model predicting the "direction" variable. 

3) Test the accuracy of the model you created in the last question.

4) Segment the Auto data set into training and test sets. 

5) The following code shows a logistic regression model using test and training data. Recreate a similar model using the Auto data set and the mpg variable. 


```r
library(ISLR)
data("Smarket")
attach(Smarket)

train=(Year<2005)
Smarket.2005=Smarket[!train,]
Direction.2005=Direction[!train]
glm.fits=glm(Direction~Lag1+Lag2+Lag3+Lag4+Lag5+Volume,data=Smarket,family=binomial,subset=train)
glm.probs=predict(glm.fits,Smarket.2005,type="response")
glm.pred=rep("Down",252)
glm.pred[glm.probs>.5]="Up"
```

