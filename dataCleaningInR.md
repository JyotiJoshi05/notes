# Data Cleaning in R
### Steps of cleaning Data
- Exploring raw data
- Tidying data
- Preparing data for analysis
```
No one likes missing data, but it is dangerous to assume that it can simply be removed or replaced. Sometimes missing data tells us something important about whatever it is that we're measuring (i.e. the value of the variable that is missing may be related to - the reason it is missing). Such data is called Missing not at Random, or MNAR.
```
# View the first 6 rows of data
head(weather)

# View the last 6 rows of data
tail(weather)

# View a condensed summary of the data
str(weather)

### Exploring raw data
- Understand the structure of your data
- Look at your data
- Visualize your data

### Load the data
data <- read.csv("")

### View its class
class(data)

### View its dimensions
dim(data)

### Look at column names
names(data)

str(data) function can be passed any object

### library(dplyr)
glimpse(data)

### summary(data)
5 point summary of each column

Rows - Observations
Columns - Variables or Attributes
Each observation describes each person - observational units

### gather(data, key, value, ...)
Change columns to key value pairs
The most important function in tidyr is gather(). It should be used when you have columns that are not variables and you want to collapse them into key-value pairs.
The easiest way to visualize the effect of gather() is that it makes wide datasets long. 

### spread(data, key, value)
spread key-value pairs into columns

### separate()
The separate() function allows you to separate one column into multiple columns. Unless you tell it otherwise, it will attempt to separate on any character that is not a letter or number. You can also specify a specific separator using the sep argument.

### unite()
The opposite of separate() is unite(), which takes multiple columns and pastes them together. By default, the contents of the columns will be separated by underscores in the new column, but this behavior can be altered via the sep argument.

str_trim()
trim leading and trailing white space

str_pad()
pad with additional characters

str_detect()
detect a pattern

str_replace()
find and replace a pattern

### Find rows with no missing values
complete.cases(df)

### Find indices of NAs in Max.Gust.SpeedMPH
ind <- which(is.na(weather6$Max.Gust.SpeedMPH))

### Look at the full rows for records missing Max.Gust.SpeedMPH
weather6[ind, ]

### Find row with Max.Humidity of 1000
ind <- which(weather6$Max.Humidity == 1000)

### Look at the data for that day
weather6[ind, ]

### Data Exploration Alternatives
Excel 
Data Explorer
Tableau
SPSS
SAS