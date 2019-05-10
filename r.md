# R Functions
c() or concatenate command
- Create Vector
> a <- c(1.8, 4.5)   #numeric
class()
- Check the class of any object
> class(a)
as command
- Convert the class of a vector
> a = as.integer(a)
list function
- Create a vector with elements of different data types
> my_list <- list(22, "ab", TRUE, 1 + 2i)
access a list element
> my_list[[3]]
access a list element with index
> my_list[3]
matrix function
- Create a 2 D data structure with elements of same class
> my_matrix <- matrix(1:6, nrow=3, ncol=2)
dim() or attributes()
- Find the dimensions of a matrix
```
> dim(my_matrix)
> attributes(my_matrix)
> age <- c(23, 44, 15, 12, 31, 16)
> age
[1] 23 44 15 12 31 16
> dim(age) <- c(2,3)
> age
[,1] [,2] [,3]
[1,] 23 15 31
[2,] 44 12 16
> class(age)
[1] "matrix"
```
cbind() and rbind()
- Join two vectors - column bind and row bind
```
> x <- c(1, 2, 3, 4, 5, 6)
> y <- c(20, 30, 40, 50, 60)
> cbind(x, y)
> rbind(x, y)
> class(cbind(x, y))
[1] “matrix”
```
### DataFrame
In a matrix, every element must have same class. 
Data frame consist of list of vectors containing different classes. 
This means, every column of a data frame acts like a list. 
Every time we read data in R, it will be stored in the form of a data frame.

```
> df <- data.frame(name = c("ash","jane","paul","mark"), score = c(67,56,87,91))
> df
name score
1 ash 67
2 jane 56
3 paul 87
4 mark 91

> dim(df)
[1] 4 2

> str(df)
'data.frame': 4 obs. of 2 variables:
$ name : Factor w/ 4 levels "ash","jane","mark",..: 1 2 4 3
$ score: num 67 56 87 91

> nrow(df)
[1] 4

> ncol(df)
[1] 2
```
dim()
- Returns the dimension of data frame.

str()
- Returns the structure of a data frame i.e. the list of variables stored in the data frame. 

nrow() and ncol()
- Return the number of rows and number of columns in a data set 
```
Continuous variables are those which can take any form such as 1, 2, 3.5, 4.66 etc. 
Categorical variables are those which takes only discrete values such as 2, 5, 11, 15 etc. 
In R, categorical values are represented by factors. 
In df, name is a factor variable having 4 unique levels. 
Factor or categorical variable are specially treated in a data set.
```
> is.na(df) #checks the entire data set for NAs and return logical output
> df[!complete.cases(df),] #returns the list of rows having missing values
> mean(df$score, na.rm = TRUE)
> new_df <- na.omit(df)

### Response Variable (a.k.a Dependent Variable)
In a data set, the response variable (y) is one on which we make predictions.

### Predictor Variable (a.k.a Independent Variable)
In a data set, predictor variables (Xi) are those using which the prediction is made on response variable.

