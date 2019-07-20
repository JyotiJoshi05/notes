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

### Data Munging
- Transforming data
- Raw data to usable data
- Data must be cleaned first

### Data Munging Tasks
- Renaming variables
- Data type conversion
- Encoding values
- Merging data sets
- Converting units
- Handling missing data
- Handling anomalous data

### Clean Data
- No errors
- No missing values
- Properly encoded: date
- Internally consistent: numerical or decimal

## Data Munging/Cleaning/Transforming/ETL/Wrangling/Cleansing
### Main steps when working with data
Import data from some source - File based/ Web-based/ Databases/ Statistical data
### Clean data
Reshaping data
Renaming Columns
Converting data types
Ensure proper encoding
Ensure internal Consistency
Handling errors and outliers
Handling missing values
### Transform cleaned data
Select columns
Filter rows
Group rows
Order rows
Merge tables
### Export to share
File based formats
Web based
Databases
Statistical
Packages - tidyr, reshape2, stringr, lubridate, validate
Transform Packages - base, plyr,dplyr, data.table, sqldf

### Profiling
Profiling R code gives you the chance to identify bottlenecks and pieces of code that needs to be more efficiently implemented [1].

Profiling R code is usually the last thing I do in the process of package (or function) development. In my experience we can reduce the amount of time necessary to run an R routine by as much as 90% with very simple changes to our code. Just yesterday I reduced the time necessary to run one of my functions from 28 sec. to 2 sec. just by changing one line of the code from
```
x = data.frame(a = variable1, b = variable2)
to

x = c(variable1, variable2)
```
```
Rprof and summaryRprof approach

The standard approach to profile R code is to use the Rprof function to profile and the summaryRprof function to summarize the result.

1
2
3
4
5
6
7
8
9
10
Rprof("path_to_hold_output")
## some code to be profiled
Rprof(NULL)
## some code NOT to be profiled
Rprof("path_to_hold_output", append=TRUE)
## some code to be profiled
Rprof(NULL)
 
# summarize the results
summaryRprof("path_to_hold_output")
Rprof works by recording at fixed intervals (by default every 20 msecs) which R function is being used, and recording the results in a file. summaryRprof will give you a list with four elements:

by.self: time spent in function alone.
by.total: time spent in function and callees.
sample.interval: the sampling interval, by default every 20 msecs.
sampling.time: total time of profiling run. Remember that profiling does impose a small performance penalty.
Profiling short runs can be misleading, so in this case I usually use the replicate function

# Evaluate shortFunction() for 100 times
replicate(n = 100, shortFunction())
R performs garbage collection from time to time  to reclaim unused memory, and this takes an appreciable amount of time which profiling will charge to whichever function happens to provoke it. It may be useful to compare profiling code immediately after a call to gc() with a profiling run without a preceding call to gc [1].

A short default example collected from the help files is
Rprof(tmp <- tempfile())
example(glm)
Rprof()
summaryRprof(tmp)

$sample.interval
[1] 0.02

$sampling.time
[1] 0.22
Alternative approaches

The following code uses profr package and produces Figure 1.

require(profr)
require(ggplot2)
x = profr(example(glm))
ggplot(x)
The following code uses proftools package and produces Figure 2. Although it is hard to see, there are function names within each node in Figure 2. If you save the picture as a pdf file and zoom in you can actually read the names clearly, which might be useful to visually identify which function is a bottleneck in your code.

Rprof(tmp <- tempfile())
example(glm)
Rprof()
plotProfileCallGraph(readProfileData(tmp),
                     score = "total")

To successfully use proftools you need to make sure you have Rgraphviz properly installed. You need to install it directly from the bioconductors site [2]:

source("<a class="vglnk" href="http://bioconductor.org/biocLite.R" rel="nofollow"><span>http</span><span>://</span><span>bioconductor</span><span>.</span><span>org</span><span>/</span><span>biocLite</span><span>.</span><span>R</span></a>")
biocLite("Rgraphviz")
```

```

# Add tenure
emp_tenure <- emp_jhi %>%
  mutate(tenure = ifelse(status == "Active", 
                         time_length(interval(date_of_joining, cutoff_date), 
                                     "years"), 
                         time_length(interval(date_of_joining, last_working_date), 
                                     "years")))

# Compare tenure of active and inactive employees
ggplot(emp_tenure, aes(x = status, y = tenure
)) + 
  geom_boxplot()
 ```
 # Compare compensation of Active and Inactive employees across levels
ggplot(emp_tenure, 
       aes(x = level, y = compensation, fill = status)) + 
  geom_boxplot()
  
It's important that the else keyword comes on the same line as the closing bracket of the if part!
# Find the highest multiplier (BustedAt value) achieved in a game
bustabit %>%
    arrange(desc(BustedAt)) %>%
    slice(1)
# Create the mean-sd standardization function
mean_sd_standard <- function(x) {
    # .... YOUR CODE FOR TASK 4 ....
    (x - mean(x))/sd(x)
    
}

# Apply the function to each numeric variable in the clustering set
bustabit_standardized <- bustabit_clus %>%
    mutate_if(is.numeric, mean_sd_standard)
              
# Summarize our standardized data
summary(bustabit_standardized)

# Group by the cluster assignment and calculate averages
bustabit_clus_avg <- bustabit_clus %>%
    group_by(bustabit_clus$cluster) %>%
    summarize_if(funs(is.numeric),mean )

# View the resulting table
bustabit_clus_avg

# Remove align level
comics_filtered <- comics %>%
  filter(align != "Reformed Criminals") %>%
  droplevels()
```
# Create side-by-side barchart of alignment by gender
ggplot(comics, aes(x = gender, fill = align)) + 
  geom_bar(position="dodge") +
  theme(axis.text.x = element_text(angle = 90))
  ```
 ### Faceting
 It breaks a dataset based on levels in a categorical data
 faceted barcharts
 You can improve the interpretability of the plot, though, by implementing some sensible ordering. Superheroes that are "Neutral" show an alignment between "Good" and "Bad", so it makes sense to put that bar in the middle.
 
 # Plot of alignment broken down by gender
ggplot(comics, aes(x = align)) + 
  geom_bar() +
  facet_wrap(~ gender)
  
  # Put levels of flavor in decending order
lev <- c("apple", "key lime", "boston creme", "blueberry", "cherry", "pumpkin", "strawberry")
pies$flavor <- factor(pies$flavor, levels = lev)

# Create barchart of flavor
ggplot(pies, aes(x = flavor)) + 
  geom_bar(fill = "chartreuse") + 
  theme(axis.text.x = element_text(angle = 90))

# Alternative solution to finding levels
# lev <- unlist(select(arrange(cnt, desc(n)), flavor))

# Check out the currently attached packages again
search()

# Chunk 1
library(data.table)
require(rjson)

# Chunk 2
library("data.table")
require(rjson)

# Chunk 3
library(data.table)
require(rjson, character.only = TRUE)
-If character.only is set to TRUE, require() does not allow you to pass the package you want to load as a simple name; you'll have to surround it with quotes in this case.
# Chunk 4
library(c("data.table", "rjson"))
- Package must be of length 1

### lapply
lapply takes a vector or list X, and applies the function FUN to each of its members. If FUN requires additional arguments, you pass them after you've specified X and FUN (...). The output of lapply() is a list, the same length as X, where each element is the result of applying FUN on the corresponding element of X.

Writing your own functions and then using them inside lapply() is quite an accomplishment! But defining functions to use them only once is kind of overkill, isn't it? That's why you can use so-called anonymous functions in R.

```
# Definition of split_low
pioneers <- c("GAUSS:1777", "BAYES:1702", "PASCAL:1623", "PEARSON:1857")
split <- strsplit(pioneers, split = ":")
split_low <- lapply(split, tolower)

# Generic select function
select_el <- function(x, index) {
  x[index]
}

# Use lapply() twice on split_low: names and years
names <- lapply(split_low, select_el, index = 1)
years <- lapply(split_low, select_el, index = 2)
```
str(TRUE)
on its own prints only the structure of the logical to the console, not NULL. That's because str() uses invisible() behind the scenes, which returns an invisible copy of the return value, NULL in this case. This prevents it from being printed when the result of str() is not assigned.

```
Given that the length of the output of below_zero() changes for different input vectors, sapply() is not able to nicely convert the output of lapply() to a nicely formatted matrix. Instead, the output values of sapply() and lapply() are exactly the same, as shown by the TRUE output of identical().
```
abs(): Calculate the absolute value.
sum(): Calculate the sum of all the values in a data structure.
mean(): Calculate the arithmetic mean.
round(): Round the values to 0 decimal places by default. Try out ?round in the console for variations of round() and ways to change the number of digits to round to.
seq(): Generate sequences, by specifying the from, to, and by arguments.
rep(): Replicate elements of vectors and lists.
sort(): Sort a vector in ascending order. Works on numerics, but also on character strings and logicals.
rev(): Reverse the elements in a data structures for which reversal is defined.
str(): Display the structure of any R object.
append(): Merge vectors or lists.
is.*(): Check for the class of an R object.
as.*(): Convert an R object from one class to another.
unlist(): Flatten (possibly embedded) lists to produce a vector.
grepl(), which returns TRUE when a pattern is found in the corresponding character string.
grep(), which returns a vector of indices of the character strings that contains the pattern.
You can use the caret, ^, and the dollar sign, $ to match the content located in the start and end of a string, respectively. This could take us one step closer to a correct pattern for matching only the ".edu" email addresses from our list of emails. But there's more that can be added to make the pattern more robust:

@, because a valid email must contain an at-sign.
.*, which matches any character (.) zero or more times (*). Both the dot and the asterisk are metacharacters. You can use them to match any character between the at-sign and the ".edu" portion of an email address.
\\.edu$, to match the ".edu" part of the email at the end of the string. The \\ part escapes the dot: it tells R that you want to use the . as an actual character.

While grep() and grepl() were used to simply check whether a regular expression could be matched with a character vector, sub() and gsub() take it one step further: you can specify a replacement argument. If inside the character vector x, the regular expression pattern is found, the matching element(s) will be replaced with replacement.sub() only replaces the first match, whereas gsub() replaces all matches.
.*: A usual suspect! It can be read as "any character that is matched zero or more times".
\\s: Match a space. The "s" is normally a character, escaping it (\\) makes it a metacharacter.
[0-9]+: Match the numbers 0 to 9, at least once (+).
([0-9]+): The parentheses are used to make parts of the matching string available to define the replacement. The \\1 in the replacement argument of sub() gets set to the string that is captured by the regular expression [0-9]+.

The ([0-9]+) selects the entire number that comes before the word “nomination” in the string, and the entire match gets replaced by this number because of the \\1 that reference to the content inside the parentheses.

The ([0-9]+) selects the entire number that comes before the word “nomination” in the string, and the entire match gets replaced by this number because of the \\1 that reference to the content inside the parentheses.

In R, dates are represented by Date objects, while times are represented by POSIXct objects. Under the hood, however, these dates and times are simple numerical values. Date objects store the number of days since the 1st of January in 1970. POSIXct objects on the other hand, store the number of seconds since the 1st of January in 1970.
The 1st of January in 1970 is the common origin for representing times and dates in a wide range of programming languages. There is no particular reason for this; it is a simple convention. Of course, it's also possible to create dates and times before 1970; the corresponding numerical values are simply negative in this case.
%Y: 4-digit year (1982)
%y: 2-digit year (82)
%m: 2-digit month (01)
%d: 2-digit day of the month (13)
%A: weekday (Wednesday)
%a: abbreviated weekday (Wed)
%B: month (January)
%b: abbreviated month (Jan)
as.Date("1982-01-13")
as.Date("Jan-13-82", format = "%b-%d-%y")
as.Date("13 January, 1982", format = "%d %B, %Y")
Notice that the first line here did not need a format argument, because by default R matches your character string to the formats "%Y-%m-%d" or "%Y/%m/%d".

today <- Sys.Date()
format(Sys.Date(), format = "%d %B, %Y")
format(Sys.Date(), format = "Today is a %A!")

%H: hours as a decimal number (00-23)
%I: hours as a decimal number (01-12)
%M: minutes as a decimal number
%S: seconds as a decimal number
%T: shorthand notation for the typical format %H:%M:%S
%p: AM/PM indicator

CSV files can be imported with read_csv(). It's a wrapper function around read_delim() that handles all the details for you. For example, it will assume that the first row contains the column names.

read_tsv("potatoes.txt", skip = 6, n_max = 5, col_names = properties)


# Column names
properties <- c("area", "temp", "size", "storage", "method",
                "texture", "flavor", "moistness")

# Import all data, but force all columns to be character: potatoes_char
potatoes_char <- read_tsv("potatoes.txt", col_types = "cccccccc", col_names = properties)

# The collectors you will need to import the data
fac <- col_factor(levels = c("Beef", "Meat", "Poultry"))
int <- col_integer()

# Edit the col_types argument to import the data correctly: hotdogs_factor
hotdogs_factor <- read_tsv("hotdogs.txt",
                           col_names = c("type", "calories", "sodium"),
                           col_types = list(fac, int, int))

# Filter cars with 4, 6, 8 cylinders
common_cyl <- filter(cars, ncyl %in% c(4, 6, 8))


-- Convert the values in firstname to a max. of 16 characters
ALTER TABLE professors 
ALTER COLUMN firstname 
TYPE varchar(16)
USING SUBSTRING(firstname FROM 1 FOR 16)

alter table tablename
alter column columnname
drop set null or
set not null

add constraint somename unique(colname)

-- Make universities.university_shortname unique
ALTER table universities
ADD column university_shortname_unq UNIQUE(university_shortname);


importing data in R

dbListTables(con)
dbReadTable(con,<tablename>)
dbDicsonnect(con)


# Load the DBI package
library(DBI)

# Connect to the MySQL database: con
con <- dbConnect(RMySQL::MySQL(), 
                 dbname = "tweater", 
                 host = "courses.csrrinzqubik.us-east-1.rds.amazonaws.com", 
                 port = 3306,
                 user = "student",
                 password = "datacamp")

# Build a vector of table names: tables
tables <- as.vector(dbListTables(con))

# Display structure of tables
str(tables)


# Load the DBI package
library(DBI)

# Connect to the MySQL database: con
con <- dbConnect(RMySQL::MySQL(), 
                 dbname = "tweater", 
                 host = "courses.csrrinzqubik.us-east-1.rds.amazonaws.com", 
                 port = 3306,
                 user = "student",
                 password = "datacamp")

# Get table names
table_names <- dbListTables(con)

# Import all tables
tables <- lapply(table_names,dbReadTable , conn = con)

# Print out tables
tables
